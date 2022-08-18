# 编译静态库，并创建demo，画圈，显示svg，并保存成png图片

静态库编译命令
```
bin/gn gen out/Static --args='is_official_build=true skia_use_system_harfbuzz=false skia_use_system_libwebp=false skia_use_gl=false skia_use_system_icu=false'
```

demo的cmake

```
cmake_minimum_required(VERSION 3.0.0)
project(demo VERSION 0.1.0)
set(CMAKE_CXX_STANDARD 17)
set(_src /home/liushichao/test/skia_demo/thirdparty/include/modules/svg/src)
add_executable(demo
    main.cpp
)

target_include_directories(
    ${PROJECT_NAME}
    PUBLIC
    "/home/liushichao/test/skia_demo/thirdparty/include/src/shaders"
    "thirdparty/include/src/core"
    "thirdparty/include/core"
    "thirdparty/include"
    "thirdparty"
)

target_link_libraries(
    ${PROJECT_NAME}
    "/home/liushichao/test/skia_demo/thirdparty/lib/libsvg.a"
    "/home/liushichao/test/skia_demo/thirdparty/lib/libskia.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libsktext.a"
    "/home/liushichao/test/skia_demo/thirdparty/lib/libskshaper.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libskottie.a"
    "/home/liushichao/test/skia_demo/thirdparty/lib/libskunicode.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libsksg.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libskresources.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libskparagraph.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libskcms.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libpiex.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libpathkit.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libparticles.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libharfbuzz.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libdng_sdk.a"
    # "/home/liushichao/test/skia_demo/thirdparty/lib/libcompression_utils_portable.a"
    pthread
    png
    z
    webp
    jpeg
    expat
    fontconfig
    freetype
)

```

demo 源码
```
#include <iostream>
#include "SkBitmapProcShader.h"

#include "SkCanvas.h"
#include "SkBitmap.h"
#include "SkTypeface.h"

///////////////////////////////////////////////////////////////////////////////

#include "SkImageEncoder.h"
#include "tools/ToolUtils.h"
// #include "SkImageDecoder.h"
// #include "SkImageEncoder.h"
// #include "SkRect.h"


#include "include/core/SkCanvas.h"
#include "include/core/SkStream.h"
#include "modules/svg/include/SkSVGDOM.h"
#include "modules/svg/include/SkSVGNode.h"
#include "src/core/SkOSFile.h"
#include "src/utils/SkOSPath.h"
#include "src/xml/SkDOM.h"




#define BG_COLOR    0xFFDDDDDD


void circle(SkCanvas* canvas, int width, bool aa) {
    SkPaint paint;

    paint.setAntiAlias(aa);
    if (width < 0) {
        paint.setStyle(SkPaint::kFill_Style);
    } else {
        paint.setStyle(SkPaint::kStroke_Style);
        paint.setStrokeWidth(SkIntToScalar(width));
    }
    canvas->drawCircle(100, 100, 90.0f, paint);
    // if ((false)) { // avoid bit rot, suppress warning
    //     test_circlebounds(canvas);
    // }
}

void drawSvg(SkCanvas* canvas, SkString fPath, int width, int height) {
        SkFILEStream svgStream(fPath.c_str());
    if (!svgStream.isValid()) {
        SkDebugf("file not found: \"%s\"\n", fPath.c_str());
        return;
    }

    auto fDom = SkSVGDOM::MakeFromStream(svgStream);
    if (fDom) {
        fDom->setContainerSize(SkSize::Make(width, height));
    }

    if (fDom) {
        fDom->render(canvas);
    }
}

// void onSizeChange() override {
//     if (fDom) {
//         fDom->setContainerSize(SkSize::Make(this->width(), this->height()));
//     }

//     this->INHERITED::onSizeChange();
// }

// SkString name() override { return fLabel; }


int main()
{

    std::cout << "hello." << std::endl;
    SkBitmap bm;
    bm.allocN32Pixels(300, 645);
    SkCanvas canvas(bm);
    // SkScalar s = SkIntToScalar(1024) / 1024;
    // canvas.scale(s, s);
    canvas.save();
    canvas.drawColor(BG_COLOR);
    circle(&canvas, 4, true);
    drawSvg(&canvas, SkString("/home/liushichao/test/skia_demo/123.svg"), 300, 200);
    canvas.restore();

    
    SkString str;
    str.printf("./slide_%zu.png", 1);
    ToolUtils::EncodeImageToFile(str.c_str(), bm, SkEncodedImageFormat::kPNG, 100);
    
    std::cout << str.c_str() << std::endl;
    // setBGColor(BG_COLOR);




    // const int w = 1080;
    // const int h = 1920;
    // /*准备目标图片和源图片*/
    // SkBitmap dst;
    // dst.allocPixels(SkImageInfo::Make(w, h, kN32_SkColorType, kPremul_SkAlphaType));
    // SkCanvas c(dst);

    // SkBitmap src;
    // SkImageDecoder::DecodeFile("test.jpg", &src);

    // /*各种绘制图片方法使用示例*/
    // {
    //     c.drawBitmap(src, 0, 0, NULL);
    // }

    // {
    //     c.drawSprite(src, 400, 400, NULL);
    // }
    // {
    //     SkRect dstR;
    //     r.set(29, 29, 100, 100);
    //     SkRect srcR;
    //     r.set(0,0,40,50);
    //     c.drawBitmapRectToRect(src, &srcR, dstR, NULL);
    // }
    // {
    //     SkMatrix m;
    //     m.setScale(1.4,4.3);
    //     c.drawBitmapMatrix(src, m, NULL);
    // }
    // {
    //     SkRect dstRect;
    //     dstRect.set(100,100,480,920);
    //     SkPaint paint;
    //     SkMatrix m;
    //     m.setScale(3.2, 4.1);
    //     SkShader* shader = CreateBitmapShader(src, SkShader::kRepeat_TileMode, SkShader::kRepeat_TileMode, m, NULL);
    //     paint.setShader(shader);
    //     SkSafeUnref(shader);
    //     c.drawRect(dstRect, paint);
    // }

    // /*输出图片*/
    // SkImageEncoder::EncodeFile("output.jpg", dst, SkImageEncoder::kJPEG_Type, 100);
    return 1;
}
```
