# 编译静态库，并创建demo，画圈，显示svg，并保存成png图片

静态库编译命令
```
bin/gn gen out/Static --args='is_official_build=true skia_use_system_harfbuzz=false skia_use_system_libwebp=false skia_use_gl=false skia_use_system_icu=false'
ninja -C out/Static
```

查看编译参数
```
bin/gn args out/Static --list
```

参数列表
```
ar
    Current value (from the default) = "ar"
      From //gn/BUILDCONFIG.gn:20

cc
    Current value (from the default) = "cc"
      From //gn/BUILDCONFIG.gn:21

cc_wrapper
    Current value (from the default) = ""
      From //gn/toolchain/BUILD.gn:38

clang_win
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:30

clang_win_version
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:31

current_cpu
    Current value (from the default) = ""
      (Internally set; try `gn help current_cpu`.)

current_os
    Current value (from the default) = ""
      (Internally set; try `gn help current_os`.)

cxx
    Current value (from the default) = "c++"
      From //gn/BUILDCONFIG.gn:22

dlsymutil_pool_depth
    Current value (from the default) = 4
      From //gn/toolchain/BUILD.gn:45

    dsymutil seems to kill the machine when too many processes are run in
    parallel, so we need to use a pool to limit the concurrency when passing
    large -j to Ninja (e.g. Goma build). Unfortunately this is also one of the
    slowest steps in a build, so we don't want to limit too much. Use the number
    of CPUs as a default.

extra_asmflags
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:14

extra_cflags
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:15

extra_cflags_c
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:16

extra_cflags_cc
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:17

extra_ldflags
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:18

host_ar
    Current value (from the default) = "ar"
      From //gn/toolchain/BUILD.gn:9

host_cc
    Current value (from the default) = "cc"
      From //gn/toolchain/BUILD.gn:10

host_cpu
    Current value (from the default) = "x64"
      (Internally set; try `gn help host_cpu`.)

host_cxx
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:11

host_link
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:54

host_os
    Current value (from the default) = "linux"
      (Internally set; try `gn help host_os`.)

ios_min_target
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:33

ios_use_simulator
    Current value (from the default) = false
      From //gn/BUILDCONFIG.gn:35

is_component_build
    Current value (from the default) = false
      From //gn/BUILDCONFIG.gn:12

is_debug
    Current value (from the default) = false
      From //gn/BUILDCONFIG.gn:38

is_official_build
    Current value = true
      From //out/Static/args.gn:1
    Overridden from the default = false
      From //gn/BUILDCONFIG.gn:11

link_pool_depth
    Current value (from the default) = -1
      From //gn/toolchain/BUILD.gn:50

    Too many linkers running at once causes issues for some builders. Allow
    such builders to limit the number of concurrent link steps.
    link_pool_depth < 0 means no pool, 0 means cpu count, > 0 sets pool size.

malloc
    Current value (from the default) = ""
      From //gn/skia/BUILD.gn:20

ndk
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:13

ndk_api
    Current value (from the default) = 21
      From //gn/BUILDCONFIG.gn:16

    Android 5.0, Lollipop

paragraph_bench_enabled
    Current value (from the default) = false
      From //modules/skparagraph/BUILD.gn:10

paragraph_gms_enabled
    Current value (from the default) = true
      From //modules/skparagraph/BUILD.gn:8

paragraph_tests_enabled
    Current value (from the default) = true
      From //modules/skparagraph/BUILD.gn:9

sanitize
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:18

skia_android_serial
    Current value (from the default) = ""
      From //gn/skia.gni:12

skia_build_for_debugger
    Current value (from the default) = false
      From //gn/skia.gni:138

skia_build_fuzzers
    Current value (from the default) = false
      From //gn/skia.gni:105

skia_canvaskit_enable_alias_font
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:6

skia_canvaskit_enable_canvas_bindings
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:7

skia_canvaskit_enable_debugger
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:8

skia_canvaskit_enable_effects_deserialization
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:9

skia_canvaskit_enable_embedded_font
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:10

skia_canvaskit_enable_font
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:11

skia_canvaskit_enable_matrix_helper
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:12

skia_canvaskit_enable_paragraph
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:19

skia_canvaskit_enable_particles
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:13

skia_canvaskit_enable_pathops
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:14

skia_canvaskit_enable_rt_shader
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:15

skia_canvaskit_enable_skottie
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:16

skia_canvaskit_enable_skp_serialization
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:17

skia_canvaskit_enable_sksl_trace
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:18

skia_canvaskit_enable_webgl
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:25

skia_canvaskit_enable_webgpu
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:24

skia_canvaskit_force_tracing
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:21

skia_canvaskit_include_viewer
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:20

skia_canvaskit_legacy_draw_vertices_blend_mode
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:23

skia_canvaskit_profile_build
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:22

skia_compare_vm_vs_rp
    Current value (from the default) = false
      From //gn/skia.gni:83

skia_compile_modules
    Current value (from the default) = false
      From //gn/skia.gni:13

skia_compile_sksl_tests
    Current value (from the default) = false
      From //gn/skia.gni:14

skia_disable_vma_stl_shared_mutex
    Current value (from the default) = false
      From //gn/skia.gni:34

skia_emsdk_dir
    Current value (from the default) = "/home/liushichao/skia/third_party/externals/emsdk"
      From //gn/toolchain/wasm.gni:12

    The location of an activated emsdk. We default to the one brought in by
    DEPS and bin/activate-emsdk.

skia_enable_android_utils
    Current value (from the default) = false
      From //gn/skia.gni:16

skia_enable_api_available_macro
    Current value (from the default) = true
      From //gn/skia.gni:15

skia_enable_direct3d_debug_layer
    Current value (from the default) = false
      From //gn/skia.gni:133

skia_enable_discrete_gpu
    Current value (from the default) = true
      From //gn/skia.gni:18

skia_enable_flutter_defines
    Current value (from the default) = false
      From //gn/skia.gni:19

skia_enable_fontmgr_FontConfigInterface
    Current value (from the default) = true
      From //gn/skia.gni:126

skia_enable_fontmgr_android
    Current value (from the default) = true
      From //gn/skia.gni:118

skia_enable_fontmgr_custom_directory
    Current value (from the default) = true
      From //gn/skia.gni:120

skia_enable_fontmgr_custom_embedded
    Current value (from the default) = true
      From //gn/skia.gni:121

skia_enable_fontmgr_custom_empty
    Current value (from the default) = true
      From //gn/skia.gni:122

skia_enable_fontmgr_empty
    Current value (from the default) = false
      From //gn/skia.gni:20

skia_enable_fontmgr_fontconfig
    Current value (from the default) = true
      From //gn/skia.gni:123

skia_enable_fontmgr_fuchsia
    Current value (from the default) = false
      From //gn/skia.gni:21

skia_enable_fontmgr_win
    Current value (from the default) = false
      From //gn/skia.gni:22

skia_enable_fontmgr_win_gdi
    Current value (from the default) = false
      From //gn/skia.gni:124

skia_enable_gpu
    Current value (from the default) = true
      From //gn/skia.gni:23

skia_enable_gpu_debug_layers
    Current value (from the default) = false
      From //gn/skia.gni:33

skia_enable_graphite
    Current value (from the default) = false
      From //gn/skia.gni:75

skia_enable_metal_debug_info
    Current value (from the default) = false
      From //gn/skia.gni:134

skia_enable_particles
    Current value (from the default) = true
      From //modules/particles/BUILD.gn:7

skia_enable_pdf
    Current value (from the default) = true
      From //gn/skia.gni:24

skia_enable_precompile
    Current value (from the default) = true
      From //gn/skia.gni:27

skia_enable_skgpu_v1
    Current value (from the default) = true
      From //gn/skia.gni:17

skia_enable_skottie
    Current value (from the default) = true
      From //gn/skia.gni:25

skia_enable_skparagraph
    Current value (from the default) = true
      From //modules/skparagraph/BUILD.gn:7

skia_enable_skshaper
    Current value (from the default) = true
      From //modules/skshaper/skshaper.gni:20

skia_enable_sksl
    Current value (from the default) = true
      From //gn/skia.gni:28

skia_enable_sksl_tracing
    Current value (from the default) = false
      From //gn/skia.gni:29

skia_enable_sktext
    Current value (from the default) = true
      From //experimental/sktext/BUILD.gn:7

skia_enable_skvm_jit_when_possible
    Current value (from the default) = false
      From //gn/skia.gni:30

skia_enable_spirv_validation
    Current value (from the default) = false
      From //gn/skia.gni:127

skia_enable_svg
    Current value (from the default) = true
      From //gn/skia.gni:31

skia_enable_tools
    Current value (from the default) = false
      From //gn/skia.gni:32

skia_enable_vulkan_debug_layers
    Current value (from the default) = false
      From //gn/skia.gni:132

skia_enable_winuwp
    Current value (from the default) = false
      From //gn/skia.gni:35

skia_fontmgr_factory
    Current value (from the default) = ":fontmgr_fontconfig_factory"
      From //gn/skia.gni:152

skia_generate_workarounds
    Current value (from the default) = false
      From //gn/skia.gni:36

skia_gl_standard
    Current value (from the default) = ""
      From //gn/skia.gni:94

skia_include_multiframe_procs
    Current value (from the default) = false
      From //gn/skia.gni:37

skia_lex
    Current value (from the default) = false
      From //gn/skia.gni:38

skia_libgifcodec_path
    Current value (from the default) = "third_party/externals/libgifcodec"
      From //gn/skia.gni:39

skia_pdf_subset_harfbuzz
    Current value (from the default) = true
      From //gn/skia.gni:114

skia_system_freetype2_include_path
    Current value (from the default) = "/usr/include/freetype2"
      From //third_party/freetype2/BUILD.gn:11

skia_system_freetype2_lib
    Current value (from the default) = "freetype"
      From //third_party/freetype2/BUILD.gn:12

skia_tools_require_resources
    Current value (from the default) = false
      From //gn/skia.gni:40

skia_update_fuchsia_sdk
    Current value (from the default) = false
      From //gn/skia.gni:41

skia_use_angle
    Current value (from the default) = false
      From //gn/skia.gni:42

skia_use_dawn
    Current value (from the default) = false
      From //gn/skia.gni:43

skia_use_direct3d
    Current value (from the default) = false
      From //gn/skia.gni:44

skia_use_dng_sdk
    Current value (from the default) = true
      From //gn/skia.gni:129

skia_use_egl
    Current value (from the default) = false
      From //gn/skia.gni:45

skia_use_expat
    Current value (from the default) = true
      From //gn/skia.gni:46

skia_use_ffmpeg
    Current value (from the default) = false
      From //gn/skia.gni:47

skia_use_fixed_gamma_text
    Current value (from the default) = false
      From //gn/skia.gni:48

skia_use_fontconfig
    Current value (from the default) = true
      From //gn/skia.gni:49

skia_use_fonthost_mac
    Current value (from the default) = false
      From //gn/skia.gni:50

skia_use_freetype
    Current value (from the default) = true
      From //gn/skia.gni:51

skia_use_freetype_svg
    Current value (from the default) = true
      From //third_party/freetype2/BUILD.gn:14

skia_use_freetype_woff2
    Current value (from the default) = false
      From //third_party/freetype2/BUILD.gn:13

skia_use_gl
    Current value = false
      From //out/Static/args.gn:4
    Overridden from the default = true
      From //gn/skia.gni:53

skia_use_harfbuzz
    Current value (from the default) = true
      From //gn/skia.gni:52

skia_use_icu
    Current value (from the default) = true
      From //gn/skia.gni:54

skia_use_libavif
    Current value (from the default) = false
      From //gn/skia.gni:55

skia_use_libfuzzer_defaults
    Current value (from the default) = true
      From //gn/skia.gni:106

skia_use_libgifcodec
    Current value (from the default) = true
      From //gn/skia.gni:130

skia_use_libheif
    Current value (from the default) = false
      From //gn/skia.gni:56

skia_use_libjpeg_turbo_decode
    Current value (from the default) = true
      From //gn/skia.gni:57

skia_use_libjpeg_turbo_encode
    Current value (from the default) = true
      From //gn/skia.gni:58

skia_use_libjxl_decode
    Current value (from the default) = false
      From //gn/skia.gni:59

skia_use_libpng_decode
    Current value (from the default) = true
      From //gn/skia.gni:60

skia_use_libpng_encode
    Current value (from the default) = true
      From //gn/skia.gni:61

skia_use_libwebp_decode
    Current value (from the default) = true
      From //gn/skia.gni:62

skia_use_libwebp_encode
    Current value (from the default) = true
      From //gn/skia.gni:63

skia_use_lua
    Current value (from the default) = false
      From //gn/skia.gni:64

skia_use_metal
    Current value (from the default) = false
      From //gn/skia.gni:65

skia_use_ndk_images
    Current value (from the default) = false
      From //gn/skia.gni:66

skia_use_perfetto
    Current value (from the default) = true
      From //gn/skia.gni:67

skia_use_piex
    Current value (from the default) = true
      From //gn/skia.gni:68

skia_use_runtime_icu
    Current value (from the default) = false
      From //modules/skunicode/BUILD.gn:10

skia_use_sfml
    Current value (from the default) = false
      From //gn/skia.gni:69

skia_use_sfntly
    Current value (from the default) = true
      From //gn/skia.gni:131

skia_use_system_expat
    Current value (from the default) = true
      From //third_party/expat/BUILD.gn:7

skia_use_system_freetype2
    Current value (from the default) = true
      From //third_party/freetype2/BUILD.gn:9

skia_use_system_harfbuzz
    Current value = false
      From //out/Static/args.gn:2
    Overridden from the default = true
      From //third_party/harfbuzz/BUILD.gn:10

skia_use_system_icu
    Current value = false
      From //out/Static/args.gn:5
    Overridden from the default = true
      From //third_party/icu/BUILD.gn:11

skia_use_system_libjpeg_turbo
    Current value (from the default) = true
      From //third_party/libjpeg-turbo/BUILD.gn:7

skia_use_system_libpng
    Current value (from the default) = true
      From //third_party/libpng/BUILD.gn:7

skia_use_system_libwebp
    Current value = false
      From //out/Static/args.gn:3
    Overridden from the default = true
      From //third_party/libwebp/BUILD.gn:7

skia_use_system_zlib
    Current value (from the default) = true
      From //third_party/zlib/BUILD.gn:7

skia_use_vma
    Current value (from the default) = false
      From //gn/skia.gni:135

skia_use_vulkan
    Current value (from the default) = false
      From //gn/skia.gni:102

skia_use_webgl
    Current value (from the default) = false
      From //gn/skia.gni:70

skia_use_webgpu
    Current value (from the default) = false
      From //gn/skia.gni:71

skia_use_wuffs
    Current value (from the default) = false
      From //gn/skia.gni:72

skia_use_x11
    Current value (from the default) = true
      From //gn/skia.gni:73

skia_use_xps
    Current value (from the default) = true
      From //gn/skia.gni:74

skia_use_zlib
    Current value (from the default) = true
      From //gn/skia.gni:76

skia_vulkan_memory_allocator_dir
    Current value (from the default) = "//third_party/externals/vulkanmemoryallocator"
      From //gn/skia.gni:137

target_ar
    Current value (from the default) = "ar"
      From //gn/toolchain/BUILD.gn:33

target_cc
    Current value (from the default) = "cc"
      From //gn/toolchain/BUILD.gn:34

target_cpu
    Current value (from the default) = ""
      (Internally set; try `gn help target_cpu`.)

target_cxx
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:35

target_link
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:55

target_os
    Current value (from the default) = ""
      (Internally set; try `gn help target_os`.)

text_bench_enabled
    Current value (from the default) = false
      From //experimental/sktext/BUILD.gn:10

text_gms_enabled
    Current value (from the default) = true
      From //experimental/sktext/BUILD.gn:8

text_tests_enabled
    Current value (from the default) = true
      From //experimental/sktext/BUILD.gn:9

third_party_isystem
    Current value (from the default) = true
      From //third_party/third_party.gni:7

werror
    Current value (from the default) = false
      From //gn/skia/BUILD.gn:21

win_sdk
    Current value (from the default) = "C:/Program Files (x86)/Windows Kits/10"
      From //gn/BUILDCONFIG.gn:24

win_sdk_version
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:25

win_toolchain_version
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:28

win_vc
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:27

xcode_sysroot
    Current value (from the default) = ""
      From //gn/skia/BUILD.gn:22
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


### 动态库编译

```
bin/gn gen out/Shared --args='is_official_build=true is_component_build=true skia_enable_svg=true skia_use_system_harfbuzz=false skia_use_system_libwebp=false skia_use_gl=false skia_use_system_icu=false'
ninja -C out/Static
```

```
ar
    Current value (from the default) = "ar"
      From //gn/BUILDCONFIG.gn:20

cc
    Current value (from the default) = "cc"
      From //gn/BUILDCONFIG.gn:21

cc_wrapper
    Current value (from the default) = ""
      From //gn/toolchain/BUILD.gn:38

clang_win
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:30

clang_win_version
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:31

current_cpu
    Current value (from the default) = ""
      (Internally set; try `gn help current_cpu`.)

current_os
    Current value (from the default) = ""
      (Internally set; try `gn help current_os`.)

cxx
    Current value (from the default) = "c++"
      From //gn/BUILDCONFIG.gn:22

dlsymutil_pool_depth
    Current value (from the default) = 4
      From //gn/toolchain/BUILD.gn:45

    dsymutil seems to kill the machine when too many processes are run in
    parallel, so we need to use a pool to limit the concurrency when passing
    large -j to Ninja (e.g. Goma build). Unfortunately this is also one of the
    slowest steps in a build, so we don't want to limit too much. Use the number
    of CPUs as a default.

extra_asmflags
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:14

extra_cflags
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:15

extra_cflags_c
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:16

extra_cflags_cc
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:17

extra_ldflags
    Current value (from the default) = []
      From //gn/skia/BUILD.gn:18

host_ar
    Current value (from the default) = "ar"
      From //gn/toolchain/BUILD.gn:9

host_cc
    Current value (from the default) = "cc"
      From //gn/toolchain/BUILD.gn:10

host_cpu
    Current value (from the default) = "x64"
      (Internally set; try `gn help host_cpu`.)

host_cxx
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:11

host_link
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:54

host_os
    Current value (from the default) = "linux"
      (Internally set; try `gn help host_os`.)

ios_min_target
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:33

ios_use_simulator
    Current value (from the default) = false
      From //gn/BUILDCONFIG.gn:35

is_component_build
    Current value = true
      From //out/Shared/args.gn:2
    Overridden from the default = false
      From //gn/BUILDCONFIG.gn:12

is_debug
    Current value (from the default) = false
      From //gn/BUILDCONFIG.gn:38

is_official_build
    Current value = true
      From //out/Shared/args.gn:1
    Overridden from the default = false
      From //gn/BUILDCONFIG.gn:11

link_pool_depth
    Current value (from the default) = -1
      From //gn/toolchain/BUILD.gn:50

    Too many linkers running at once causes issues for some builders. Allow
    such builders to limit the number of concurrent link steps.
    link_pool_depth < 0 means no pool, 0 means cpu count, > 0 sets pool size.

malloc
    Current value (from the default) = ""
      From //gn/skia/BUILD.gn:20

ndk
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:13

ndk_api
    Current value (from the default) = 21
      From //gn/BUILDCONFIG.gn:16

    Android 5.0, Lollipop

paragraph_bench_enabled
    Current value (from the default) = false
      From //modules/skparagraph/BUILD.gn:10

paragraph_gms_enabled
    Current value (from the default) = true
      From //modules/skparagraph/BUILD.gn:8

paragraph_tests_enabled
    Current value (from the default) = true
      From //modules/skparagraph/BUILD.gn:9

sanitize
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:18

skia_android_serial
    Current value (from the default) = ""
      From //gn/skia.gni:12

skia_build_for_debugger
    Current value (from the default) = false
      From //gn/skia.gni:138

skia_build_fuzzers
    Current value (from the default) = false
      From //gn/skia.gni:105

skia_canvaskit_enable_alias_font
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:6

skia_canvaskit_enable_canvas_bindings
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:7

skia_canvaskit_enable_debugger
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:8

skia_canvaskit_enable_effects_deserialization
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:9

skia_canvaskit_enable_embedded_font
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:10

skia_canvaskit_enable_font
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:11

skia_canvaskit_enable_matrix_helper
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:12

skia_canvaskit_enable_paragraph
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:19

skia_canvaskit_enable_particles
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:13

skia_canvaskit_enable_pathops
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:14

skia_canvaskit_enable_rt_shader
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:15

skia_canvaskit_enable_skottie
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:16

skia_canvaskit_enable_skp_serialization
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:17

skia_canvaskit_enable_sksl_trace
    Current value (from the default) = true
      From //modules/canvaskit/canvaskit.gni:18

skia_canvaskit_enable_webgl
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:25

skia_canvaskit_enable_webgpu
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:24

skia_canvaskit_force_tracing
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:21

skia_canvaskit_include_viewer
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:20

skia_canvaskit_legacy_draw_vertices_blend_mode
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:23

skia_canvaskit_profile_build
    Current value (from the default) = false
      From //modules/canvaskit/canvaskit.gni:22

skia_compare_vm_vs_rp
    Current value (from the default) = false
      From //gn/skia.gni:83

skia_compile_modules
    Current value (from the default) = false
      From //gn/skia.gni:13

skia_compile_sksl_tests
    Current value (from the default) = false
      From //gn/skia.gni:14

skia_disable_vma_stl_shared_mutex
    Current value (from the default) = false
      From //gn/skia.gni:34

skia_emsdk_dir
    Current value (from the default) = "/home/liushichao/skia/third_party/externals/emsdk"
      From //gn/toolchain/wasm.gni:12

    The location of an activated emsdk. We default to the one brought in by
    DEPS and bin/activate-emsdk.

skia_enable_android_utils
    Current value (from the default) = false
      From //gn/skia.gni:16

skia_enable_api_available_macro
    Current value (from the default) = true
      From //gn/skia.gni:15

skia_enable_direct3d_debug_layer
    Current value (from the default) = false
      From //gn/skia.gni:133

skia_enable_discrete_gpu
    Current value (from the default) = true
      From //gn/skia.gni:18

skia_enable_flutter_defines
    Current value (from the default) = false
      From //gn/skia.gni:19

skia_enable_fontmgr_FontConfigInterface
    Current value (from the default) = true
      From //gn/skia.gni:126

skia_enable_fontmgr_android
    Current value (from the default) = true
      From //gn/skia.gni:118

skia_enable_fontmgr_custom_directory
    Current value (from the default) = true
      From //gn/skia.gni:120

skia_enable_fontmgr_custom_embedded
    Current value (from the default) = true
      From //gn/skia.gni:121

skia_enable_fontmgr_custom_empty
    Current value (from the default) = true
      From //gn/skia.gni:122

skia_enable_fontmgr_empty
    Current value (from the default) = false
      From //gn/skia.gni:20

skia_enable_fontmgr_fontconfig
    Current value (from the default) = true
      From //gn/skia.gni:123

skia_enable_fontmgr_fuchsia
    Current value (from the default) = false
      From //gn/skia.gni:21

skia_enable_fontmgr_win
    Current value (from the default) = false
      From //gn/skia.gni:22

skia_enable_fontmgr_win_gdi
    Current value (from the default) = false
      From //gn/skia.gni:124

skia_enable_gpu
    Current value (from the default) = true
      From //gn/skia.gni:23

skia_enable_gpu_debug_layers
    Current value (from the default) = false
      From //gn/skia.gni:33

skia_enable_graphite
    Current value (from the default) = false
      From //gn/skia.gni:75

skia_enable_metal_debug_info
    Current value (from the default) = false
      From //gn/skia.gni:134

skia_enable_particles
    Current value (from the default) = true
      From //modules/particles/BUILD.gn:7

skia_enable_pdf
    Current value (from the default) = true
      From //gn/skia.gni:24

skia_enable_precompile
    Current value (from the default) = true
      From //gn/skia.gni:27

skia_enable_skgpu_v1
    Current value (from the default) = true
      From //gn/skia.gni:17

skia_enable_skottie
    Current value (from the default) = true
      From //gn/skia.gni:25

skia_enable_skparagraph
    Current value (from the default) = true
      From //modules/skparagraph/BUILD.gn:7

skia_enable_skshaper
    Current value (from the default) = true
      From //modules/skshaper/skshaper.gni:20

skia_enable_sksl
    Current value (from the default) = true
      From //gn/skia.gni:28

skia_enable_sksl_tracing
    Current value (from the default) = false
      From //gn/skia.gni:29

skia_enable_sktext
    Current value (from the default) = true
      From //experimental/sktext/BUILD.gn:7

skia_enable_skvm_jit_when_possible
    Current value (from the default) = false
      From //gn/skia.gni:30

skia_enable_spirv_validation
    Current value (from the default) = false
      From //gn/skia.gni:127

skia_enable_svg
    Current value = true
      From //out/Shared/args.gn:3
    Overridden from the default = false
      From //gn/skia.gni:31

skia_enable_tools
    Current value (from the default) = false
      From //gn/skia.gni:32

skia_enable_vulkan_debug_layers
    Current value (from the default) = false
      From //gn/skia.gni:132

skia_enable_winuwp
    Current value (from the default) = false
      From //gn/skia.gni:35

skia_fontmgr_factory
    Current value (from the default) = ":fontmgr_fontconfig_factory"
      From //gn/skia.gni:152

skia_generate_workarounds
    Current value (from the default) = false
      From //gn/skia.gni:36

skia_gl_standard
    Current value (from the default) = ""
      From //gn/skia.gni:94

skia_include_multiframe_procs
    Current value (from the default) = false
      From //gn/skia.gni:37

skia_lex
    Current value (from the default) = false
      From //gn/skia.gni:38

skia_libgifcodec_path
    Current value (from the default) = "third_party/externals/libgifcodec"
      From //gn/skia.gni:39

skia_pdf_subset_harfbuzz
    Current value (from the default) = true
      From //gn/skia.gni:114

skia_system_freetype2_include_path
    Current value (from the default) = "/usr/include/freetype2"
      From //third_party/freetype2/BUILD.gn:11

skia_system_freetype2_lib
    Current value (from the default) = "freetype"
      From //third_party/freetype2/BUILD.gn:12

skia_tools_require_resources
    Current value (from the default) = false
      From //gn/skia.gni:40

skia_update_fuchsia_sdk
    Current value (from the default) = false
      From //gn/skia.gni:41

skia_use_angle
    Current value (from the default) = false
      From //gn/skia.gni:42

skia_use_dawn
    Current value (from the default) = false
      From //gn/skia.gni:43

skia_use_direct3d
    Current value (from the default) = false
      From //gn/skia.gni:44

skia_use_dng_sdk
    Current value (from the default) = true
      From //gn/skia.gni:129

skia_use_egl
    Current value (from the default) = false
      From //gn/skia.gni:45

skia_use_expat
    Current value (from the default) = true
      From //gn/skia.gni:46

skia_use_ffmpeg
    Current value (from the default) = false
      From //gn/skia.gni:47

skia_use_fixed_gamma_text
    Current value (from the default) = false
      From //gn/skia.gni:48

skia_use_fontconfig
    Current value (from the default) = true
      From //gn/skia.gni:49

skia_use_fonthost_mac
    Current value (from the default) = false
      From //gn/skia.gni:50

skia_use_freetype
    Current value (from the default) = true
      From //gn/skia.gni:51

skia_use_freetype_svg
    Current value (from the default) = true
      From //third_party/freetype2/BUILD.gn:14

skia_use_freetype_woff2
    Current value (from the default) = false
      From //third_party/freetype2/BUILD.gn:13

skia_use_gl
    Current value = false
      From //out/Shared/args.gn:6
    Overridden from the default = true
      From //gn/skia.gni:53

skia_use_harfbuzz
    Current value (from the default) = true
      From //gn/skia.gni:52

skia_use_icu
    Current value (from the default) = true
      From //gn/skia.gni:54

skia_use_libavif
    Current value (from the default) = false
      From //gn/skia.gni:55

skia_use_libfuzzer_defaults
    Current value (from the default) = true
      From //gn/skia.gni:106

skia_use_libgifcodec
    Current value (from the default) = true
      From //gn/skia.gni:130

skia_use_libheif
    Current value (from the default) = false
      From //gn/skia.gni:56

skia_use_libjpeg_turbo_decode
    Current value (from the default) = true
      From //gn/skia.gni:57

skia_use_libjpeg_turbo_encode
    Current value (from the default) = true
      From //gn/skia.gni:58

skia_use_libjxl_decode
    Current value (from the default) = false
      From //gn/skia.gni:59

skia_use_libpng_decode
    Current value (from the default) = true
      From //gn/skia.gni:60

skia_use_libpng_encode
    Current value (from the default) = true
      From //gn/skia.gni:61

skia_use_libwebp_decode
    Current value (from the default) = true
      From //gn/skia.gni:62

skia_use_libwebp_encode
    Current value (from the default) = true
      From //gn/skia.gni:63

skia_use_lua
    Current value (from the default) = false
      From //gn/skia.gni:64

skia_use_metal
    Current value (from the default) = false
      From //gn/skia.gni:65

skia_use_ndk_images
    Current value (from the default) = false
      From //gn/skia.gni:66

skia_use_perfetto
    Current value (from the default) = true
      From //gn/skia.gni:67

skia_use_piex
    Current value (from the default) = true
      From //gn/skia.gni:68

skia_use_runtime_icu
    Current value (from the default) = false
      From //modules/skunicode/BUILD.gn:10

skia_use_sfml
    Current value (from the default) = false
      From //gn/skia.gni:69

skia_use_sfntly
    Current value (from the default) = true
      From //gn/skia.gni:131

skia_use_system_expat
    Current value (from the default) = true
      From //third_party/expat/BUILD.gn:7

skia_use_system_freetype2
    Current value (from the default) = true
      From //third_party/freetype2/BUILD.gn:9

skia_use_system_harfbuzz
    Current value = false
      From //out/Shared/args.gn:4
    Overridden from the default = true
      From //third_party/harfbuzz/BUILD.gn:10

skia_use_system_icu
    Current value = false
      From //out/Shared/args.gn:7
    Overridden from the default = true
      From //third_party/icu/BUILD.gn:11

skia_use_system_libjpeg_turbo
    Current value (from the default) = true
      From //third_party/libjpeg-turbo/BUILD.gn:7

skia_use_system_libpng
    Current value (from the default) = true
      From //third_party/libpng/BUILD.gn:7

skia_use_system_libwebp
    Current value = false
      From //out/Shared/args.gn:5
    Overridden from the default = true
      From //third_party/libwebp/BUILD.gn:7

skia_use_system_zlib
    Current value (from the default) = true
      From //third_party/zlib/BUILD.gn:7

skia_use_vma
    Current value (from the default) = false
      From //gn/skia.gni:135

skia_use_vulkan
    Current value (from the default) = false
      From //gn/skia.gni:102

skia_use_webgl
    Current value (from the default) = false
      From //gn/skia.gni:70

skia_use_webgpu
    Current value (from the default) = false
      From //gn/skia.gni:71

skia_use_wuffs
    Current value (from the default) = false
      From //gn/skia.gni:72

skia_use_x11
    Current value (from the default) = true
      From //gn/skia.gni:73

skia_use_xps
    Current value (from the default) = true
      From //gn/skia.gni:74

skia_use_zlib
    Current value (from the default) = true
      From //gn/skia.gni:76

skia_vulkan_memory_allocator_dir
    Current value (from the default) = "//third_party/externals/vulkanmemoryallocator"
      From //gn/skia.gni:137

target_ar
    Current value (from the default) = "ar"
      From //gn/toolchain/BUILD.gn:33

target_cc
    Current value (from the default) = "cc"
      From //gn/toolchain/BUILD.gn:34

target_cpu
    Current value (from the default) = ""
      (Internally set; try `gn help target_cpu`.)

target_cxx
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:35

target_link
    Current value (from the default) = "c++"
      From //gn/toolchain/BUILD.gn:55

target_os
    Current value (from the default) = ""
      (Internally set; try `gn help target_os`.)

text_bench_enabled
    Current value (from the default) = false
      From //experimental/sktext/BUILD.gn:10

text_gms_enabled
    Current value (from the default) = true
      From //experimental/sktext/BUILD.gn:8

text_tests_enabled
    Current value (from the default) = true
      From //experimental/sktext/BUILD.gn:9

third_party_isystem
    Current value (from the default) = true
      From //third_party/third_party.gni:7

werror
    Current value (from the default) = false
      From //gn/skia/BUILD.gn:21

win_sdk
    Current value (from the default) = "C:/Program Files (x86)/Windows Kits/10"
      From //gn/BUILDCONFIG.gn:24

win_sdk_version
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:25

win_toolchain_version
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:28

win_vc
    Current value (from the default) = ""
      From //gn/BUILDCONFIG.gn:27

xcode_sysroot
    Current value (from the default) = ""
      From //gn/skia/BUILD.gn:22
```

```

 
 c++ -o libsvg2.so -fPIC -shared obj/modules/svg/src/libsvg.SkSVGAttribute.o obj/modules/svg/src/libsvg.SkSVGAttributeParser.o obj/modules/svg/src/libsvg.SkSVGCircle.o obj/modules/svg/src/libsvg.SkSVGClipPath.o obj/modules/svg/src/libsvg.SkSVGContainer.o obj/modules/svg/src/libsvg.SkSVGDOM.o obj/modules/svg/src/libsvg.SkSVGEllipse.o obj/modules/svg/src/libsvg.SkSVGFe.o obj/modules/svg/src/libsvg.SkSVGFeBlend.o obj/modules/svg/src/libsvg.SkSVGFeColorMatrix.o obj/modules/svg/src/libsvg.SkSVGFeComposite.o obj/modules/svg/src/libsvg.SkSVGFeDisplacementMap.o obj/modules/svg/src/libsvg.SkSVGFeFlood.o obj/modules/svg/src/libsvg.SkSVGFeGaussianBlur.o obj/modules/svg/src/libsvg.SkSVGFeImage.o obj/modules/svg/src/libsvg.SkSVGFeLightSource.o obj/modules/svg/src/libsvg.SkSVGFeLighting.o obj/modules/svg/src/libsvg.SkSVGFeMorphology.o obj/modules/svg/src/libsvg.SkSVGFeOffset.o obj/modules/svg/src/libsvg.SkSVGFeTurbulence.o obj/modules/svg/src/libsvg.SkSVGFilter.o obj/modules/svg/src/libsvg.SkSVGFilterContext.o obj/modules/svg/src/libsvg.SkSVGGradient.o obj/modules/svg/src/libsvg.SkSVGImage.o obj/modules/svg/src/libsvg.SkSVGLine.o obj/modules/svg/src/libsvg.SkSVGLinearGradient.o obj/modules/svg/src/libsvg.SkSVGMask.o obj/modules/svg/src/libsvg.SkSVGNode.o obj/modules/svg/src/libsvg.SkSVGOpenTypeSVGDecoder.o obj/modules/svg/src/libsvg.SkSVGPath.o obj/modules/svg/src/libsvg.SkSVGPattern.o obj/modules/svg/src/libsvg.SkSVGPoly.o obj/modules/svg/src/libsvg.SkSVGRadialGradient.o obj/modules/svg/src/libsvg.SkSVGRect.o obj/modules/svg/src/libsvg.SkSVGRenderContext.o obj/modules/svg/src/libsvg.SkSVGSVG.o obj/modules/svg/src/libsvg.SkSVGShape.o obj/modules/svg/src/libsvg.SkSVGStop.o obj/modules/svg/src/libsvg.SkSVGText.o obj/modules/svg/src/libsvg.SkSVGTransformableNode.o obj/modules/svg/src/libsvg.SkSVGUse.o obj/modules/svg/src/libsvg.SkSVGValue.o ./libskia.so ./libskresources.a ./libskshaper.so -lpthread -lfontconfig -std=c++17
```
