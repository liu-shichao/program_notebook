### 中文字库
默认方式不支持，超过了4M的数组，编译不通过，需要保存成字库的bin文件，然后通过esptool烧录到flash中才行，记录其中的几个关键步骤

```
1.修改 epd47 库中的 fontconvert.py 脚本文件，添加中文的unicode编码范围，以及中文符号的unicode编码范围
  intervals = [
    (32, 126),
    (0x4e00, 0x9fa5), #全部的中文
    (0xff01, 0xff5e), #中文标点

    # (160, 255),
    # (0x2500, 0x259F),
    # (0x2700, 0x27BF),
    # # powerline symbols
    # (0xE0A0, 0xE0A2),
    # (0xE0B0, 0xE0B3),
    # (0x1F600, 0x1F680),
]

2.执行脚本生成字库的头文件
  python fontconvert.py --compress demo 16 MiSans-Normal.ttf > font_all.h
其中MiSans是下载的小米字体

3.将生成的字库中的bitmap数组拷贝出来，用 c++ 程序写入2进制文件 data.bin 中
#include <iostream>
#include <fstream>
#include "bin.h"
int main(int argc, const char* argv[]) {
    std::ofstream outFile("data.bin", std::ios::out | std::ios::binary);
    outFile.write((char*)bitmap, 5841976);
    outFile.close();

    return 0;
}

其中bin.h
const uint8_t bitmap[5841976] = {
    0x78, 0x9C, 0x03, 0x00, 0x00, 0x00, 0x00, 0x01, 0x78, 0x9C, 0x73, 0x70, 0xF9, 0x78, 0x1F, 0x08,
    0xCF, 0x7F, 0x38, 0xFF, 0x61, 0x3F, 0x18, 0xAE, 0x7F, 0x00, 0x82, 0xF3, 0x2F, 0xCC, 0xBF, 0xD0,
    0x7F, ...........
}

4.修改 esp32 分区
需要修改esp32的分区表，复制C:\Users\xxx\AppData\Local\Arduino15\packages\esp32\hardware\esp32\2.0.11\tools\partitions 中的一个csv文件，重新命名，修改成自己需要的分区，如下

app15MB.csv

# Name,   Type, SubType, Offset,  Size, Flags
nvs,      data, nvs,     0x9000,  0x5000,
otadata,  data, ota,     0xe000,  0x2000,
app0,     app,  ota_0,   0x10000, 0x400000,
raw,0x50,0x50,0x410000,0xb00000,
coredump, data, coredump,0xFF0000,0x10000,
# to create/use ffat, see https://github.com/marcmerlin/esp32_fatfsimage,,,,

5.修改board文件
C:\Users\xxxx\AppData\Local\Arduino15\packages\esp32\hardware\esp32\2.0.11
增加如下内容
esp32.menu.PartitionScheme.app15MB=16M Flash (15MB APP)
esp32.menu.PartitionScheme.app15MB.build.partitions=app15MB
esp32.menu.PartitionScheme.app15MB.upload.maximum_size=16646144

6.清理arduino缓存
删除这个目录
C:\Users\xxxxx\AppData\Roaming\arduino-ide\Local Storage\leveldb
重启arduino就可以看到新添加的分区表了

4.将data.bin 烧录到esp32中
esptool -p com3 write_flash 0x410000 data.bin

5.修改font_all.h，去掉bitmap中的大部分内容，只留一个自己用来占位，这样就减少了程序的体积，能够编译通过了

6.修改epd47库，从flash中加载字库的bitmap

static void IRAM_ATTR draw_char(const GFXfont *font,
                                uint8_t *buffer,
                                int32_t *cursor_x,
                                int32_t cursor_y,
                                uint16_t buf_width,
                                uint16_t buf_height,
                                uint32_t cp,
                                const FontProperties *props)
{
    GFXglyph *glyph;
    get_glyph(font, cp, &glyph);

    if (!glyph)
    {
        get_glyph(font, props->fallback_glyph, &glyph);
    }

    if (!glyph)
    {
        return;
    }

    uint32_t offset = glyph->data_offset;
    uint8_t width = glyph->width;
    uint8_t height = glyph->height;
    int32_t left = glyph->left;

    int32_t byte_width = (width / 2 + width % 2);
    unsigned long bitmap_size = byte_width * height;
    uint8_t *bitmap =  bitmap = (uint8_t *)malloc(bitmap_size);
    if (font->compressed)
    {
        uint8_t *bitmap_compressed = (uint8_t *)malloc(glyph->compressed_size);
        const esp_partition_t * ep = esp_partition_find_first(ESP_PARTITION_TYPE_ANY, ESP_PARTITION_SUBTYPE_ANY, "raw");
        esp_err_t ret = esp_partition_read(ep, offset, bitmap_compressed, glyph->compressed_size);
        uncompress(bitmap, &bitmap_size, bitmap_compressed, glyph->compressed_size);
        free(bitmap_compressed);
    }
    else
    {
        bitmap = &font->bitmap[offset];
    }

    uint8_t color_lut[16];
    for (int32_t c = 0; c < 16; c++)
    {
        int32_t color_difference = (int32_t)props->fg_color - (int32_t)props->bg_color;
        color_lut[c] = max(0, min(15, props->bg_color + c * color_difference / 15));
    }

    for (int32_t y = 0; y < height; y++)
    {
        int32_t yy = cursor_y - glyph->top + y;
        if (yy < 0 || yy >= buf_height)
        {
            continue;
        }
        int32_t start_pos = *cursor_x + left;
        bool byte_complete = start_pos % 2;
        int32_t x = max(0, -start_pos);
        int32_t max_x = min(start_pos + width, buf_width * 2);
        for (int32_t xx = start_pos; xx < max_x; xx++)
        {
            uint32_t buf_pos = yy * buf_width + xx / 2;
            uint8_t old = buffer[buf_pos];
            uint8_t bm = bitmap[y * byte_width + x / 2];
            if ((x & 1) == 0)
            {
                bm = bm & 0xF;
            }
            else
            {
                bm = bm >> 4;
            }

            if ((xx & 1) == 0)
            {
                buffer[buf_pos] = (old & 0xF0) | color_lut[bm];
            }
            else
            {
                buffer[buf_pos] = (old & 0x0F) | (color_lut[bm] << 4);
            }
            byte_complete = !byte_complete;
            x++;
        }
    }
    free(bitmap);
    *cursor_x += glyph->advance_x;
}


```
