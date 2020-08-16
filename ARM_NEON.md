### NEON

是arm cortex-A系列中的一种128位的SIMD(single instruction, multiple data)扩展结构

### cortex的三个系列

cortex-A: application，主要是偏高端应用的处理器

cortex-R: realtimek，用在执行实时性高的场景中

cortex-M: MicroController, 一般用作微型控制器

### arm的架构(详细的参见：https://blog.csdn.net/qq_38880380/article/details/79486016)

ARMv1,ARMv2,ARMv3,ARMv4,ARMV5,ARMv6,ARMv6-M

从v7开始分A/R/M系列了
ARMv7-A, ARMv7-R, ARMv7-M

ARMv8-A, ARMv8-R, ARMv8-M

### android使用NEON

参见：https://developer.android.com/ndk/guides/cpu-arm-neon

### FPU

FPU(float point unit): 浮点运算单元，原来与cpu一样是一个单独的处理器，在486之后，英特尔将fpu集成在了cpu之内。
