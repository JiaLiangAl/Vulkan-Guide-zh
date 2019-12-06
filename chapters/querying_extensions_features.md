# 查询，扩展和特性（Querying, Extensions, and Features）
一个Vulkan的主要特性是可以用来在多平台和设备上开发。为此，应用程序负责从每个物理设备查询信息，然后根据这些信息做出决策。

可以从物理设备中查询到的项
- 属性
- 特性
- 扩展
- 限制
- 格式

## 属性（Properties）
在Vulkan中有许多其他组件被标记为属性。术语“属性”是一个涵盖所有可查询的只读数据的术语。

## 扩展（Extensions）
扩展可能定义新的Vulkan函数，有些暴露可选的新特性，有些甚至中是暴露对SPIR-V操作的支持。既有实例扩展，也有设备扩展，所以注意确保去检查它是哪一种（可以在扩展定义的地方的“Extension Type”下找到）。

应用程序可以首先[查询物理设备](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-extensions)来检查是否支持该扩展。应用程序需要通过传递一个列表到`VkInstance`或者`VkDevice`来启用计划用到的扩展。一旦扩展被启用，所有新的原语(枚举、结构、函数等)现在都可以使用了。如果扩展没有被启用，使用任何该扩展的原语都是未定义行为。

## 特性（Features）
特性描述了并非所有实现都支持的功能。特性可以被[查询](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#vkGetPhysicalDeviceFeatures)，然后在创建`VkDevice`时启用。除了[列出所有特性](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#features)以外，由于更新的Vulkan版本或使用了扩展，一些特性是强制性的。

一种常见的技术是，一个扩展公开一个新的结构，这个结构可以通过`pNext`来传递，它增加了更多要查询的特性。

## 限制（Limits）
限制是与实现相关的最小值、最大值和应用程序可能需要知道的其他设备特征。除了[限制列表](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#limits)以外，有些限制还具有来自Vulkan实现的[要求的 最小/最大 值](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#limits-minmax)。

## 格式（Formats）
每个`VkBuffer`和`VkImage`要求来自Vulkan[VkFormat](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#formats-definition)列表中的一种格式。支持的格式可能有不同的实现，除了 [保证最少的格式特性集](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#features-required-format-support)。应用程序可以查询支持的格式属性。

每种格式都有一组`VkFormatFeatureFlagBits`，用于说明是否支持该格式。这些特征位将进一步分组以确定格式的使用方式。

> 例如：可以检查`VK_FORMAT_R8_UNORM`格式是否支持在使用`VK_IMAGE_TILING_LINEAR`的`tiling`参数创建图像时采样。
>
> 要做到这一点，查询`VK_FORMAT_R8_UNORM`的`linearTilingFeatures`标志，看是否为实现设置了`VK_FORMAT_FEATURE_SAMPLED_IMAGE_BIT`。

## 工具（Tools）
这里有少量工具来帮助以一种快速和可读的格式获取所有信息。

`vulkaninfo`是一个Windows,Linux和macOS的命令行工具，让您可以查看关于您GPU的关于以上所有可用的项。参考Vulkan SDK 中的[Vulkaninfo 文档](https://vulkan.lunarg.com/doc/sdk/latest/windows/vulkaninfo.html)

Sascha Willems 开发的[Vulkan 硬件功能查看器](https://play.google.com/store/apps/details?id=de.saschawillems.vulkancapsviewer&hl=en_US) app ，是一个显示支持Vulkan设备的所有细节的 Android app 。
