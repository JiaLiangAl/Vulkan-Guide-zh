# 加载器（Loader）
加载器负责将应用程序映射到Vulkan层和Vulkan可安装客户端驱动程序(ICD)。

![loader_overview.png](../images/loader_overview.png)

任何人都可以创建他们自己的Vulkan加载器，只要他们遵循[加载器接口](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md)。也可以构建[引用加载器](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/BUILD.md)或者从[Vulkan SDK](https://vulkan.lunarg.com/sdk/home)获取指定平台的构建版本。

## 连接到加载器（Linking Against the Loader）
[Vulkan 头文件](https://github.com/KhronosGroup/Vulkan-Headers)只提供了Vulkan的函数原型。当构建Vulkan应用程序时，你必须将它连接到加载器，否则你将会得到一个未定义的Vulkan函数引用的错误信息。有两种方案连接到加载器，[直接地](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md#directly-linking-to-the-loader)和[非直接地](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md#indirectly-linking-to-the-loader)连接，这不能和“静态链接和动态链接”混淆。

- 在编译时[直接连接](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md#directly-linking-to-the-loader)
    - 需要有一个您的构建系统能够找得到的Vulkan加载器的构建版本（静态或者动态库）
    - 构建系统(Visual Studio, CMake, 等)有关于怎样连接到库的文档，可以尝试在网上搜索`(InsertBuildSystem) link to external library`。
- 在运行时[非直接连接](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md#indirectly-linking-to-the-loader)
    - 使用动态符号查找（通过像`dlsym`和`dlopen`的系统调用），应用程序可以初始化它自己的调试表。如果加载器未被找到，允许应用程序安全地失败。它还为应用程序调用Vulkan函数提供了最快的机制。
    - [Volk](https://github.com/zeux/volk/)是一个开源实现的元加载器帮助简化这个过程。

## 平台差异
每个平台可以设置它自己执行Vulkan加载器的规则

### Android
支持Vulkan的Android设备已经在操作系统中内置了一个[Vulkan 加载器](https://source.android.com/devices/graphics/implement-vulkan#vulkan_loader)。

Android NDK中[vulkan_wrapper.c/h](https://developer.android.com/ndk/guides/graphics/getting-started#using)用来非直接连接。这在一定程度上是必要的，因为不同的供应商和OEM设备可以使用不同的Vulkan加载程序。

### Linux
[Vulkan SDK](https://vulkan.lunarg.com/sdk/home)提供一个Linux预先构建的加载器。

Vulkan SDK 的[Getting Started](https://vulkan.lunarg.com/doc/sdk/latest/linux/getting_started.html)页解释了在Linux上如何找到加载器。

### MacOS
[Vulkan SDK](https://vulkan.lunarg.com/sdk/home)提供一个MacOS预先构建的加载器。

Vulkan SDK 的[Getting Started](https://vulkan.lunarg.com/doc/sdk/latest/mac/getting_started.html)页解释了在MacOS上如何找到加载器。

### Windows
[Vulkan SDK](https://vulkan.lunarg.com/sdk/home)提供一个Windows预先构建的加载器。

The [Vulkan SDK](https://vulkan.lunarg.com/sdk/home) provides a pre-built loader for Windows.

Vulkan SDK 的[Getting Started](https://vulkan.lunarg.com/doc/sdk/latest/windows/getting_started.html)页解释了在Windows上如何找到加载器。