# 什么是 SPIR-V
[SPIR-V](https://www.khronos.org/registry/spir-v/)是图形着色器阶段和计算内核的二进制中间表示。用Vulkan,您仍然可以用一种高级的语言写着色器脚本，如GLSL或者HLSL,但SPIR-V二进制文件是需要的，当使用[vkCreateShaderModule](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#vkCreateShaderModule)时。Vulkan SDK有一个非常好的[白皮书](https://www.khronos.org/registry/spir-v/papers/WhitePaper.pdf)，介绍了SPIR-V及其优点，并对其表示进行了高级描述。还有两个来自Vulkan DevDay 2016的精彩Khronos演讲[这里](https://www.khronos.org/assets/uploads/developers/library/2016-vulkan-devday-uk/3-Intro-to-spir-v-shaders.pdf)和[这里](https://www.khronos.org/assets/uploads/developers/library/2016-vulkan-devday-uk/4-Using-spir-v-with-spirv-cross.pdf)
([二者的视频](https://www.youtube.com/watch?v=XRpVwdduzgU))。

![what_is_spirv_overview.png](../images/what_is_spirv_overview.png)

## SPIR-V 接口和功能
Vulkan有一整个部分定义了[Vulkan接口和SPIR-V着色器](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#interfaces)。当着色器一起编译时，大多数与SPIR-V接口有效的用法发生在管道创建过程中。SPIR-V有许多能力，因为它有其他目标，而不仅仅是Vulkan。要查看Vulkan所支持的功能，可以参考[Appendix](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#spirvenv-capabilities)。一些Vulkan中的扩展和特性仅仅是被设计用来检查一些SPIR-V功能是否被支持。

## 编译器（Compilers）

### glslang

[glslang](https://github.com/KhronosGroup/glslang)是Khronos 作为GLSL 和 ESSL的参数前端，以及样本SPIR-V生成器。其中包含一个独立的`glslangValidator`工具，用来从GLSL和ESSL创建SPIR-V。

### Shaderc
一个Google托管的，关于Vulkan着色器编译的工具，库和测试的集合。它包含将核心功能封装在[glslang](https://github.com/KhronosGroup/glslang)和[SPIRV-Tools](https://github.com/KhronosGroup/SPIRV-Tools)中的`glslc`，Shaderc也包含将核心功能封装在[SPIRV-Cross](https://github.com/KhronosGroup/SPIRV-Cross)和[SPIRV-Tools](https://github.com/KhronosGroup/SPIRV-Tools)中的`spvc`。

Shaderc 将这两个工具都构建为一个独立的命令行工具([glslc](https://github.com/google/shaderc/tree/master/glslc)和[spvc](https://github.com/google/shaderc/tree/master/spvc))，以及一个链接到([libshaderc](https://github.com/google/shaderc/tree/master/libshaderc)和[libshaderc_spvc](https://github.com/google/shaderc/tree/master/libshaderc_spvc))的库。

### DXC
[DirectXShaderCompiler](https://github.com/microsoft/DirectXShaderCompiler)也支持[将HLSL转换到SPIR-V](https://github.com/Microsoft/DirectXShaderCompiler/wiki/SPIR%E2%80%90V-CodeGen
).

### Clspv
[Clspv](https://github.com/google/clspv)是OpenCL C的一个子集到SPIR-V的一个原型编译器，用作Vulkan计算着色器。

## 工具和生态（Tools and Ecosystem）
有一个丰富的工具生态系统可以利用SPIR-V。[Vulkan SDK 概述了](https://vulkan.lunarg.com/doc/sdk/latest/windows/spirv_toolchain.html)所有为开发人员构建和打包的SPIR-V工具。

### SPIRV-Tools
Khronos的[SPIRV-Tools](https://github.com/KhronosGroup/SPIRV-Tools) 项目提交了C和C++ API和命令行工具来处理SPIR-V模块。此工具集包含

- 汇编 (`spirv-as`)
- 反汇编 (`spirv-dis`)
- 验证器 (`spirv-val`)
- 链接器 (`spirv-link`)
- 优化器 (`spirv-opt`)
    - LunarG 写了一个[白皮书](https://www.lunarg.com/wp-content/uploads/2018/06/SPIR-V-Shader-Legalization-and-Size-Reduction-Using-spirv-opt_v1.2.pdf) 关于 `spriv-opt`
- 减速机 (`spirv-reduce`)
- 控制流 dumper (`spirv-cfg`)

### SPIRV-Cross
Khronos 的[SPIRV-Cross](https://github.com/KhronosGroup/SPIRV-Cross)项目是在SPIR-V上执行反射和将SPIR-V 反汇编回高级语言的实用工具和库。更多细节，SPIR-V Cross的主要开发者[Hans Kristian](https://github.com/Themaister),给出了两个关于如何创建一个像SPIR-V这样的工具的精彩的演讲：[2018 Vulkanised](https://www.khronos.org/assets/uploads/developers/library/2018-vulkanised/04-SPIRVCross_Vulkanised2018.pdf) ([video](https://www.youtube.com/watch?v=T5Va6hSGx44)) 和 [2019 Vulkanised](https://www.khronos.org/assets/uploads/developers/library/2019-vulkanised/04-SPIRV-Cross-May19.pdf) ([video](https://www.youtube.com/watch?v=lv-fh_oFJUc))

![what_is_spirv_spriv_cross.png](../images/what_is_spirv_spriv_cross.png)

### SPIRV-LLVM
Khronos 的[SPIRV-LLVM](https://github.com/KhronosGroup/SPIRV-LLVM)项目是一个支持SPIR-V的LLVM 框架。它打算包含LLVM和SPIR-V之间的双向转换器。它还可以作为面向SPIR-V的基于llvm的前端编译器的基础。
