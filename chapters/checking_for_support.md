# 检查 Vulkan 支持

Vulkan 要求一个[Vulkan 加载器](./loader.md)和一个Vulkan驱动程序(也被引用为 _Vulkan Implementation_ )。驱动程序的作用是将Vulkan API 调用翻译成一个合法的Vulkan实现。最通常的例子就是一个GPU供应商发布一个驱动程序来在物理GPU上运行Vulkan。应该指出的是，一个完全以软件为基础的Vulkan实现是有可能的，虽然性能的影响将是非常明显的。

当检测Vulkan支持的时候，区分 _platform support_ 和 _device support_ 的不同是重要的。

## 平台支持

首先要做的是检查你的[平台](./platforms.md)是否支持Vulkan。每个平台使用不同的机制来管理[Vulkan加载器](./loader.md)的实现方式。然后，加载程序负责确定Vulkan驱动程序是否正确地暴露出来。

### Android
获取Vulkan信息的一种简单的方式是运行Sascha Willems开发的app[Vulkan 硬件功能查看器](https://play.google.com/store/apps/details?id=de.saschawillems.vulkancapsviewer&hl=en_US)。这个app不仅会显示是否支持Vulkan，而且还有设备提供的所有功能。

### Linux

获取[Vulkan SDK](https://vulkan.lunarg.com/sdk/home#linux)，运行[vulkaninfo](https://vulkan.lunarg.com/doc/sdk/latest/linux/vulkaninfo.html)可执行程序可以容易的检查Vulkan支持和设备提供的所有功能。

### MacOS

获取[Vulkan SDK](https://vulkan.lunarg.com/sdk/home#mac)，运行[vulkaninfo](https://vulkan.lunarg.com/doc/sdk/latest/mac/vulkaninfo.html)可执行程序可以容易的检查Vulkan支持和设备提供的所有功能。

### Windows

获取 [Vulkan SDK](https://vulkan.lunarg.com/sdk/home#windows) ，运行 [vulkaninfo.exe](https://vulkan.lunarg.com/doc/sdk/latest/windows/vulkaninfo.html) 可执行程序可以容易的检查Vulkan支持和设备提供的所有功能。

## 设备支持

因为平台支持Vulkan，并不意味着设备也支持。对于设备支持，需要确保能够使用完全实现Vulkan的Vulkan驱动程序。Vulkan驱动程序有几个不同的变体。

### 硬件实现


针对GPU硬件的驱动程序是Vulkan实现中最常见的情况。重要的是要理解，虽然某个GPU可能有运行Vulkan的物理能力，但它仍然需要一个驱动程序来控制它。驱动程序负责以最有效的方式将Vulkan调用映射到硬件。

驱动程序，像其他软件一样，都是更新的，这意味着同一物理设备和平台的驱动程序可以有多种变体。有一个由Sascha Willems开发和维护的[Vulkan数据库](https://vulkan.gpuinfo.org/)，它是所记录的Vulkan实现细节的最大集合(请注意，物理设备或平台不在Vulkan数据库中并不意味着它不存在)。

### 空设备

术语“空驱动程序”是指任何接受Vulkan API调用但不使用它们做任何事情的驱动程序。这对于测试与驱动程序的交互是很常见的，而不需要任何工作实现的支持。这也用于为还没有工作实现的新特性创建[CTS测试](./vulkan_cts.md)。

### 软件实现

创建一个只运行在CPU上的Vulkan 实现是可能的。如果需要测试与硬件无关的Vulkan，但与null驱动程序不同的是，它还输出有效的结果，那么这是非常有用的。

[SwiftShader](https://github.com/google/swiftshader) 就是一个基于CPU实现的例子。

## 检查 Vulkan 的方式

### VIA (Vulkan Installation Analyzer)

包含在 [Vulkan SDK](https://vulkan.lunarg.com/sdk/home) 中的是一个用于检查计算机上的Vulkan安装的实用程序。它支持Windows, Linux, 和 macOS。VIA 可以:
 - 确定您系统上Vulkan组件的状态
 - 验证您的Vulkan加载程序和驱动程序是否安装正确
 - 以提交bug时可以用作附件的形式捕获系统状态

更多信息，请参照[SDK关于VIA的文档](https://vulkan.lunarg.com/doc/sdk/latest/windows/via.html)。

### Hello 实例创建

检查Vulkan跨平台支持的一个简单方法是创建一个简单的"Hello World" Vulkan应用程序。函数`vkCreateInstance`用于创建Vulkan实例，也是编写有效的Vulkan应用程序的最短方法。

Vulkan SDK 提供了一个可以使用的最小的[vkCreateInstance](https://vulkan.lunarg.com/doc/view/latest/windows/tutorial/html/01-init_instance.html)例子`01-init_instance.cpp`。
