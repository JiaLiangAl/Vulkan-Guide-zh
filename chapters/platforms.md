# 平台

虽然Vulkan运行在许多平台上，但是每个平台在如何管理Vulkan方面都有细微的差异。

![platforms_overview.png](../images/platforms_overview.png)

## Android

Vulkan API[可用](https://developer.android.com/ndk/guides/graphics/getting-started)适用于任何API级别为24 (Android Nougat)的Android设备，但是并不是所有设备都有Vulkan驱动程序。

Android 使用它的[硬件抽象层(HAL)](https://source.android.com/devices/architecture/hal)在一个[预定义的路径](https://source.android.com/devices/graphics/implement-vulkan#driver_emun)中查找Vulkan驱动程序

所有运行API级别为29(Android Q)或以后的64位设备必须包括一个Vulkan 1.1 驱动程序。

## iOS

Vulkan本身并不支持iOS,但仍然可以作为[Vulkan 移植工具](./portability_initiative.md)的目标。

## Linux

Vulkan 在许多Linux发行版上被支持。

## MacOS

Vulkan本身并不支持MacOS，但仍然可以作为[Vulkan 移植工具](./portability_initiative.md)的目标。

## Nintendo Switch

Nintendo Switch 运行的是支持本地Vulkan的NVIDIA Tegra芯片组。

## Stadia

谷歌的Stadia运行在基于AMD的Linux机器上，Vulkan是必要的图形API。

## Windows

Vulkan支持Windows 7, Windows 8 和 Windows 10。

## Others

一些嵌入式系统通过允许显示[直接显示]来支持Vulkan (https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#display)。

