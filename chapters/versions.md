# 版本

Vulkan 工作在 [major, minor, patch](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions-versionnumbers) 版本系统上。目前，目前有2个次要版本已经发布(1.0和1.1)，它们彼此向后兼容。应用程序可以用[vkEnumerateInstanceVersion](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#vkEnumerateInstanceVersion) Vulkan实例支持哪个版本。还有一份[白皮书](https://www.lunarg.com/wp-content/uploads/2019/02/Vulkan-1.1-Compatibility-Statement_01_19.pdf) ，LunarG所作，关于怎样查询和检测支持的版本。在处理次要版本时，需要注意一些细微的事情。

## 实例和设备
重要的是要记住实例级版本和设备级版本之间是有区别的。加载器和实现可能支持不同的版本。

Vulkan规范中的[查询版本支持](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions-queryingversionsupport)一节详细介绍了如何在实例级和设备级查询受支持的版本。 

## 头(Header)
所有主要版本的Vulkan只有一个支持的头文件。这意味着不存在“Vulkan 1.0标头”，因为次要版本和补丁版本的标头是统一的。这不应该与生成1.0版[Vulkan Spec](./vulkan_spec.md)的能力相混淆，因为相同补丁版本的Vulkan Spec和标头是匹配的。一个例子是生成的1.0.42 Vulkan规范将与1.x.42头匹配。

强烈建议开发人员尽量跟上最新发布的头文件。Vulkan SDK有很多版本，它们都映射到已经打包的头文件版本。

## 扩展（Extensions）
Vulkan的次要版本之间，[一些扩展](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#versions-1.1)获得[提升](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-compatibility-promotions)到[核心版本](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions)。当目标是一个较新的小版本Vulkan时，应用程序将不需要在实例和设备创建时启用新升级的扩展。但是，如果应用程序希望保持向后兼容性，则需要启用扩展。

## 结构体和枚举（Structs and enums）
结构体和枚举依赖于正在使用的头文件，而不是被查询的实例或设备的版本。例如，结构体`VkPhysicalDeviceFeatures2`在Vulkan 1.1发布前，曾今是`VkPhysicalDeviceFeatures2KHR`。不管是Vulkan 1.x的什么版本，应用程序应该在代码中用`VkPhysicalDeviceFeatures2`，因为它匹配最新的头文件版本。对与在代码中已经存在`VkPhysicalDeviceFeatures2KHR`的应用程序，也不需要担心，因为Vulkan头文件中也给提升了的结构体和枚举取了别名（`typedef VkPhysicalDeviceFeatures2 VkPhysicalDeviceFeatures2KHR;`）。

使用最新命名的原因是Vulkan规范本身只会涉及到`VkPhysicalDeviceFeatures2`不管Vulkan规范生成的是什么版本。使用新的命名可以使快速地搜索到结构体使用的位置变得更容易。

## 函数（Functions）
由于函数用来沟通加载器和实现，在使用次要版本时需要更加小心。作为一个例子，让我们看看`vkGetPhysicalDeviceFeatures2KHR`，它从Vulkan 1.0升级到Vulkan 1.1，升级为`vkGetPhysicalDeviceFeatures2`。查看Vulkan头文件时，两者都声明了。

```
typedef void (VKAPI_PTR *PFN_vkGetPhysicalDeviceFeatures2)(VkPhysicalDevice physicalDevice, VkPhysicalDeviceFeatures2* pFeatures);
// ...
typedef void (VKAPI_PTR *PFN_vkGetPhysicalDeviceFeatures2KHR)(VkPhysicalDevice physicalDevice, VkPhysicalDeviceFeatures2* pFeatures);
```
主要的不同是当调用`vkGetInstanceProcAddr(instance, "vkGetPhysicalDeviceFeatures2");`时，一个Vulkan 1.0版本的实现可能不会注意`vkGetPhysicalDeviceFeatures2`的存在，然后`vkGetInstanceProcAddr`将会返回 `NULL`。在这种情况下要向后兼容Vulkan版本，应用程序应该查询`vkGetPhysicalDeviceFeatures2KHR`，因为一个1.1 Vulkan实现可能会在内部将函数直接指向`vkGetPhysicalDeviceFeatures2`函数指针。

> 请注意，`vkGetPhysicalDeviceFeatures2KHR` 函数只有在作为扩展支持的情况下才会在Vulkan 1.0实现中存在。

## 特性（Features）
在次要版本之间，一些特性位可能会被增加，删除，使之变为可选或强制性的。所有改变了的特性的细节在[核心修正](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#versions)部分中描述。

Vulkan规范中的[特性的要求](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#features-requirements)部分可以用来浏览跨小版本之间的实现需要的特性列表。


## 限制（Limits）
目前，所有版本的Vulkan都共享相同的最小/最大限制要求，但是任何更改都会在Vulkan规范的[限制的要求](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#limits-minmax)一节中列出。

## SPIR-V
每一个小版本的Vulkan对应一个版本的[必须支持的SPIR-V](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#spirvenv)。

- Vulkan 1.0 支持 SPIR-V 1.0
- Vulkan 1.1 支持 SPIR-V 1.3 and below

由应用程序来确保`VkShaderModule`中的spirv是对应的Vulkan版本的有效版本。
