# 层(Layers)
层是增强Vulkan系统的可选组件。它们可以在从应用程序到硬件的过程中拦截、评估和修改现有的Vulkan函数。可以使用[vkEnumerateInstanceLayerProperties](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#vkEnumerateInstanceLayerProperties).从应用程序查询层的属性。

## 使用层
层被打包为共享库，由加载程序动态加载并插入到它和应用程序之间。使用层需要做的两件事是二进制文件的位置和启用哪些层。要使用的层可以由应用程序显式启用，也可以通过告诉加载程序使用它们而隐式启用。关于隐式和显式层的更多细节可以在[加载器和层接口](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md#implicit-vs-explicit-layers)中找到。

[Vulkan SDK](https://vulkan.lunarg.com/sdk/home) 包含一个[层配置文档](https://vulkan.lunarg.com/doc/sdk/latest/windows/layer_configuration.html)，它非常具体地描述了如何在每个平台上发现和配置层。

## Vulkan 配置工具
Windows、Linux和macOS上的开发人员可以使用Vulkan配置器vkconfig来启用显式层和禁用隐式层，以及从图形用户界面更改层设置。有关使用Vulkan配置器的更多信息，请参见Vulkan SDK中的[Vulkan配置器文档](https://vulkan.lunarg.com/doc/sdk/latest/windows/vkconfig.html)。

## 设备层弃用
曾经有实例层和设备层，但是设备层在Vulkan的早期就被[已弃用](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-layers-devicelayerdeprecation)，应该避免。

## 创建层
任何人都可以创建一个层，只要它遵循关于加载器和层如何同意互相通信[加载器和层之间的接口](https://github.com/KhronosGroup/Vulkan-Loader/blob/master/loader/LoaderAndLayerInterface.md#loader-and-layer-interface)。

Vulkan也提供了一个[层工厂](https://vulkan.lunarg.com/doc/sdk/latest/windows/layer_factory.html)库，来帮助开发新的层([视频呈现](https://www.youtube.com/watch?v=gVT7nyXz6M8&t=5m22s))。层工厂隐藏了大量的 加载器-层 接口，层样板文件、设置和初始化，以及层开发的复杂性。在开发应用程序期间，能够轻松地创建一个层来帮助调试您的应用程序是非常有用的。更多信息，请参考[Vulkan SDK](https://vulkan.lunarg.com/sdk/home)中的[Vulkan 层工厂文档](https://vulkan.lunarg.com/doc/sdk/latest/windows/layer_factory.html)

## 平台变化

加载层的方式在加载器和平台之间隐式地变化。

### Android
对于Android P (Android 9 / API level 28)，如果设备处于可调试状态，如`getprop ro.debuggable`[返回1](http://androidxref.com/9.0.0_r3/xref/frameworks/native/vulkan/libvulkan/layers_extensions.cpp#454)，那么加载器将在[/data/local/debug/vulkan](http://androidxref.com/9.0.0_r3/xref/frameworks/native/vulkan/libvulkan/layers_extensions.cpp#67)中查找。

从Android P (Android 9 / API level 28)开始，隐式层可以被[pushed using ADB](https://developer.android.com/ndk/guides/graphics/validation-layer#vl-adb)，如果应用程序是在调试模式下构建。

除了上面的选项外，没有其他方法可以使用隐式层。

### Linux
[Vulkan SDK](https://vulkan.lunarg.com/doc/sdk/latest/linux/layer_configuration.html)解释了如何在Linux上使用隐式层

### MacOS
[Vulkan SDK](https://vulkan.lunarg.com/doc/sdk/latest/mac/layer_configuration.html)解释了如何在MacOS上使用隐式层

### Windows
[Vulkan SDK](https://vulkan.lunarg.com/doc/sdk/latest/windows/layer_configuration.html)解释了如何在Windows上使用隐式层
