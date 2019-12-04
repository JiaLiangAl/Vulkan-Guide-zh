# Windows 系统集成 (WSI)
由于Vulkan API可以在不显示结果的情况下使用，所以WSI是通过使用[可选的Vulkan扩展](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#wsi)来提供的。大多数实现都包括WSI支持。WSI的设计是从核心的Vulkan API中抽象出每个平台的窗口机制。

![wsi_setup](../images/wsi_setup.png)

## Surface
`VkSurfaceKHR`对象是平台无关的，它的设计使得其余的Vulkan API可以将它用于所有WSI操作。它是使用` VK_KHR_surface `扩展来启用的。

每个支持Vulkan Surface的平台都有自己的方式来创建一个`VkSurfaceKHR`对象，这个对象来自上层的特定于平台的API。

- Android - [vkCreateAndroidSurfaceKHR](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateAndroidSurfaceKHR)
- Fuchsia - [vkCreateImagePipeSurfaceFUCHSIA](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateImagePipeSurfaceFUCHSIA)
- Google Games - [vkCreateStreamDescriptorSurfaceGGP](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateStreamDescriptorSurfaceGGP)
- iOS - [vkCreateIOSSurfaceMVK](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateIOSSurfaceMVK)
- macOS - [vkCreateMacOSSurfaceMVK](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateMacOSSurfaceMVK)
- Metal - [vkCreateMetalSurfaceEXT](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateMetalSurfaceEXT)
- VI - [vkCreateViSurfaceNN](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateViSurfaceNN)
- Wayland - [vkWaylandSurfaceCreateInfoKHR](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkWaylandSurfaceCreateInfoKHR)
- Windows - [vkCreateWin32SurfaceKHR](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateWin32SurfaceKHR)
- XCB - [vkCreateXcbSurfaceKHR](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateXcbSurfaceKHR)
- Xlib - [vkCreateXlibSurfaceKHR](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateXlibSurfaceKHR)
- Direct-to-Display - [vkCreateDisplayPlaneSurfaceKHR](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkCreateDisplayPlaneSurfaceKHR)

一旦创建了一个`VkSurfaceKHR`，就会有各种各样的方法[功能(capabilities)](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkGetPhysicalDeviceSurfaceCapabilitiesKHR), [格式(formats)](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkGetPhysicalDeviceSurfaceFormatsKHR), 和 [呈现模式(presentation modes)](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#vkGetPhysicalDeviceSurfacePresentModesKHR) 来查询。

## 交换链(Swapchain)

`VkSwapchainKHR`对象提供通过一组`VkImage`对象呈现渲染结果到表面(surface)的能力。交换链(swapchain)的类型[呈现模式(present modes)](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#VkPresentModeKHR)确定呈现引擎的实现方式。

![wsi_engine](../images/wsi_engine.png)

Khronos的[sample](https://github.com/KhronosGroup/Vulkan-Samples/tree/master/samples/performance/swapchain_images)和[tutorial](https://github.com/KhronosGroup/Vulkan-Samples/blob/master/samples/performance/swapchain_images/swapchain_images_tutorial.md)解释在创建swapchain和选择表示模式时需要考虑的不同方面。
