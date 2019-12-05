# 开发工具

Vulkan生态系统由许多开发工具组成。这**不是**一个完整的列表，但对于许多开发人员来说，这是一个很好的起点。请继续做你自己的研究和寻找其他工具，因为开发生态系统比一个简单的markdown页面要大得多。

Khronos 提供的[Vulkan Samples](https://github.com/KhronosGroup/Vulkan-Samples)，这是一组代码和教程，演示了API的使用并解释了性能最佳实践的实现。

## Khronos 验证层
由于Vulkan不做任务错误检查，在开发时立即启用[Validation Layers](https://github.com/KhronosGroup/Vulkan-ValidationLayers) 来帮助捕获无效行为是非常重要的。虽然无效行为可能在一个实现上能正常工作，但在另一个实现上很可能失败。应用程序也不应该在应用程序中附带验证层，因为它们会显著降低性能，而且是为开发阶段设计的。

> Khronos 验证层以前由多个层组成，但是现已已经被[LunarG 的白皮书详解](https://www.lunarg.com/wp-content/uploads/2019/04/UberLayer_V3.pdf)统一了。



- **Android** - NDK附带的验证层和[关于如何使用它们的信息](https://developer.android.com/ndk/guides/graphics/validation-layer).
- **Linux** - [Vulkan SDK](https://vulkan.lunarg.com/sdk/home) 附带的验证层和如何在[Linux](https://vulkan.lunarg.com/doc/sdk/latest/linux/validation_layers.html)上使用的说明。
- **MacOS** - [Vulkan SDK](https://vulkan.lunarg.com/sdk/home) 附带的验证层和如何在[MacOS](https://vulkan.lunarg.com/doc/sdk/latest/mac/validation_layers.html)上使用的说明。
- **Windows** - [Vulkan SDK](https://vulkan.lunarg.com/sdk/home)附带的验证层和如何在[Windows](https://vulkan.lunarg.com/doc/sdk/latest/windows/validation_layers.html)上使用的说明。

## Vulkan 层
除了验证层之外，还有其他公共可用层可用于帮助开发。

- [API 日志](https://vulkan.lunarg.com/doc/sdk/latest/windows/api_dump_layer.html) - 记录API调用日志的 Vulkan SDK 层。
- [Arm PerfDoc layer](https://github.com/ARM-software/perfdoc) - 检查Vulkan应用程序在Arm Mali设备上的最佳实践。
- [LunarG 最佳实践层](https://vulkan.lunarg.com/doc/sdk/latest/windows/best_practices.html) - 突出潜在的性能问题，有问题的使用模式，常见的错误。
- [模型设备的属性](https://vulkan.lunarg.com/doc/sdk/latest/windows/device_simulation_layer.html) - 用于测试任何设备上的设备属性的Vulkan SDK层。
- [截屏](https://vulkan.lunarg.com/doc/sdk/latest/windows/screenshot_layer.html) - 将呈现的图像捕获为可视图像。
- [跟踪 FPS](https://vulkan.lunarg.com/doc/sdk/latest/windows/monitor_layer.html) - FPS 日志信息。


## 调试
调试在GPU中运行的东西可能相当困难，好在有工具可以提供帮助。

- [Arm Graphics Analyzer](https://developer.arm.com/tools-and-software/graphics-and-gaming/arm-mobile-studio/components/graphics-analyzer)
- [GAPID](https://github.com/google/gapid)
- [NVIDIA Nsight](https://developer.nvidia.com/nsight-graphics)
- [PVRCarbon](https://www.imgtec.com/developers/)
- [RenderDoc](https://renderdoc.org/)

## 分析

对于任何与GPU相关的东西，最好不要假设和配置。下面是一些已知的有助于开发的分析器。

- [AMD Radeon GPU Profiler](https://gpuopen.com/gaming-product/radeon-gpu-profiler-rgp/) - 用于AMD Radeon gpu的底层性能分析工具。
- [Arm Streamline Performance Analyzer](https://developer.arm.com/tools-and-software/graphics-and-gaming/arm-mobile-studio/components/streamline-performance-analyzer) - 使用Arm mobile Studio，为各种设备可视化移动游戏和应用程序的性能。
- [Intel(R) GPA](https://software.intel.com/en-us/gpa) - 英特尔的图形性能分析仪，支持捕获和分析多帧流的Vulkan应用程序。
- [OCAT](https://github.com/GPUOpen-Tools/OCAT) - 开放捕获和分析工具(OCAT)为D3D11、D3D12和Vulkan提供了FPS覆盖和性能度量。
- [PVRTune](https://www.imgtec.com/developers/)
- [Qualcomm Snapdragon Profiler](https://developer.qualcomm.com/software/snapdragon-profiler) - 针对Adreno GPU的分析工具。
