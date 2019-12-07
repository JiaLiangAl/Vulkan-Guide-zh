# 什么是 Vulkan ?

> Vulkan是新一代的图形和计算API，它提供了对现代gpu的高效、跨平台访问，这些gpu广泛应用于各种设备，从pc和控制台到移动电话和嵌入式平台。 

Vulkan不是一家公司，也不是一种语言，而是一种让开发者以跨平台和跨供应商的方式来为他们的现代GPU硬件编程的方式。Khronos集团是一个成员驱动的联盟，创建并维护Vulkan。

## Vulkan 的核心
在核心，Vulkan是一个[API 规范](https://www.khronos.org/registry/vulkan/#apispecs)，这是一个支持实现的硬件后续。公共规范是由[./xml/vk.xml](https://github.com/KhronosGroup/Vulkan-Docs/blob/master/xml/vk.xml) Vulkan规范仓库在[Vulkan- doc](https://github.com/KhronosGroup/Vulkan-Docs)中发现的官方公共副本中的Vulkan注册文件生成的。[XML方案文件](https://www.khronos.org/registry/vulkan/specs/1.1/registry.html)也是如此。

Khronos 组织，连同Vulkan规范一起发布了从[API注册表](https://www.khronos.org/registry/vulkan/#apiregistry)生成的[C99](http://www.open-std.org/jtc1/sc22/wg14/www/standards) [头文件](https://github.com/KhronosGroup/Vulkan-Headers/tree/master/include/vulkan)，开发人员可以使用这些头文件与Vulkan API进行对接。

对于那些可能不使用C代码的人，有各种各样的[language](https://github.com/KhronosGroup/Khronosdotorg/blob/master/api/vulkan/resources.md#language-bindings) [bindings](https://github.com/vinjn/awesome-vulkan#bindings)。


## Vulkan 和 OpenGL

Some developers might be aware of the other Khronos Group standard [OpenGL](https://www.khronos.org/opengl/) which is also a 3D Graphics API. Vulkan is not a direct replacement for OpenGL, but rather an explicit API that allows for more explicit control of the GPU.

Khronos' [Vulkan Samples](https://github.com/KhronosGroup/Vulkan-Samples) article on ["How does Vulkan compare to OpenGL ES? What should you expect when targeting Vulkan?](https://github.com/KhronosGroup/Vulkan-Samples/blob/master/samples/vulkan_basics.md) offers a more detailed comparison between the two APIs.

![what_is_vulkan_compared_to_gl.png](../images/what_is_vulkan_compared_to_gl.png)

Vulkan puts more work and responsibility into the application. Not every developer will want to make that extra investment, but those that do so correctly can find power and performance improvements.

![what_is_vulkan_decision.png](../images/what_is_vulkan_decision.png)

## Using helping libraries

While some developers may want to try using Vulkan with no help, it is common to use some lighter libraries in your development flow to help abstract some of the more tedious aspect of Vulkan. Here are some [libraries](https://github.com/KhronosGroup/Khronosdotorg/blob/master/api/vulkan/resources.md#libraries) to [help with development](https://github.com/vinjn/awesome-vulkan#libraries)

![what_is_vulkan_layer](../images/what_is_vulkan_layer.png)
