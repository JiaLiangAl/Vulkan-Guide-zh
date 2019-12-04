# 版本

Vulkan 工作在 [major, minor, patch](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions-versionnumbers) 版本系统上。目前，目前有2个次要版本已经发布(1.0和1.1)，它们彼此向后兼容。应用程序可以用[vkEnumerateInstanceVersion](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#vkEnumerateInstanceVersion) Vulkan实例支持哪个版本。还有一份[白皮书](https://www.lunarg.com/wp-content/uploads/2019/02/Vulkan-1.1-Compatibility-Statement_01_19.pdf) ，LunarG所作，关于怎样查询和检测支持的版本。在处理次要版本时，需要注意一些细微的事情。

## 实例和设备
重要的是要记住实例级版本和设备级版本之间是有区别的。加载器和实现可能支持不同的版本。

Vulkan规范中的[查询版本支持](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions-queryingversionsupport)一节详细介绍了如何在实例级和设备级查询受支持的版本。 

## 头(Header)

There is only one supported header for all major releases of Vulkan. This means that there is no such thing as "Vulkan 1.0 headers" as all headers for a minor and patch version are unified. This should not be confused with the ability to generate a 1.0 version of the [Vulkan Spec](./vulkan_spec.md), as the Vulkan Spec and header of the same patch version will match. An example would be that the generated 1.0.42 Vulkan Spec will match the 1.x.42 header.

It is highly recommended that developers try to keep up to date with the latest header files released. The Vulkan SDK comes in many versions which map to the header version it will have been packaged for.

## Extensions

Between minor versions of Vulkan, [some extensions](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#versions-1.1) get [promoted](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-compatibility-promotions) to the [core version](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions). When targeting a newer minor version of Vulkan, an application will not need to enable the newly promoted extensions at the instance and device creation. However, if an application wants to keep backward compatibility, it will need to enable the extensions.

## Structs and enums

Structs and enums are dependent on the header file being used and not the version of the instance or device queried. For example, the struct `VkPhysicalDeviceFeatures2` used to be `VkPhysicalDeviceFeatures2KHR` before Vulkan 1.1 was released. Regardless of the 1.x version of Vulkan being used, an application should use `VkPhysicalDeviceFeatures2` in its code as it matches the newest header version. For applications that did have `VkPhysicalDeviceFeatures2KHR` in the code, there is no need to worry as the Vulkan header also aliases any promoted structs and enums (`typedef VkPhysicalDeviceFeatures2 VkPhysicalDeviceFeatures2KHR;`).

The reason for using the newer naming is that the Vulkan Spec itself will only refer to `VkPhysicalDeviceFeatures2` regardless of what version of the Vulkan Spec is generated. Using the newer naming makes it easier to quickly search for where the structure is used.

## Functions

Since functions are used to interact with the loader and implementations, there needs to be a little more care when working between minor versions. As an example, let's look at `vkGetPhysicalDeviceFeatures2KHR` which was promoted to core as `vkGetPhysicalDeviceFeatures2` from Vulkan 1.0 to Vulkan 1.1. Looking at the Vulkan header both are declared.

```
typedef void (VKAPI_PTR *PFN_vkGetPhysicalDeviceFeatures2)(VkPhysicalDevice physicalDevice, VkPhysicalDeviceFeatures2* pFeatures);
// ...
typedef void (VKAPI_PTR *PFN_vkGetPhysicalDeviceFeatures2KHR)(VkPhysicalDevice physicalDevice, VkPhysicalDeviceFeatures2* pFeatures);
```

The main difference is when calling `vkGetInstanceProcAddr(instance, "vkGetPhysicalDeviceFeatures2");` a Vulkan 1.0 implementation may not be aware of `vkGetPhysicalDeviceFeatures2` existence and `vkGetInstanceProcAddr` will return `NULL`. To be backward compatible with Vulkan 1.0 in this situation, the application should query for `vkGetPhysicalDeviceFeatures2KHR` as a 1.1 Vulkan implementation will likely have the function directly pointed to the `vkGetPhysicalDeviceFeatures2` function pointer internally.

> Note that the `vkGetPhysicalDeviceFeatures2KHR` function will only exists in a Vulkan 1.0 implementation if it is supported as an extension.

## Features

Between minor versions, it is possible that some feature bits are added, removed, made optional, or made mandatory. All details of features that have changed are described in the [Core Revisions](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#versions) section.

The [Feature Requirements](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#features-requirements) section in the Vulkan Spec can be used to view the list of features that are required from implementations across minor versions.

## Limits

Currently, all versions of Vulkan share the same minimum/maximum limit requirements, but any changes would be listed in the [Limit Requirements](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#limits-minmax) section of the Vulkan Spec.

## SPIR-V

Every minor version of Vulkan maps to a version of [SPIR-V that must be supported](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#spirvenv).

- Vulkan 1.0 supports SPIR-V 1.0
- Vulkan 1.1 supports SPIR-V 1.3 and below

It is up to the application to make sure that the SPIR-V in `VkShaderModule` is of a valid version to the corresponding Vulkan version.