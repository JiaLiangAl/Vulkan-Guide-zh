# Vulkan 能做什么
Vulkan可以用来开发各种用途的应用程序。虽然Vulkan应用程序可以选择使用下面描述的功能的一个子集，但它的设计是为了让开发人员可以在一个API中使用所有功能。

> 注意：理解Vulkan是一个工具盒是很重要的，而且完成一项任务有多种方法。


## 图形(Graphics)
2D和3D图形是Vulkan API的主要用途。Vulkan被设备成允许开发者创建硬件加速图形应用程序。

> 注意：所有的Vulkan实现都要求支持图形，但是[WSI](./wsi.md)系统除外。

## 计算(Compute)

由于GPU 的并行特性，一种被称为[GPGPU](https://en.wikipedia.org/wiki/General-purpose_computing_on_graphics_processing_units)的编程风格可以用来利用GPU执行计算任务。Vulkan支持`VkQueues`, `VkPipelines`等计算变体，这些变体允许Vulkan用于一般计算。

> 注意：所有的Vulkan实现都要求支持计算。

## 射线追踪(Ray Tracing)

目前，Vulkan工作组正在研究如何使Vulkan成为一个用于光线追踪渲染的一流API。更多的信息在[Siggraph 2019](https://www.youtube.com/watch?v=_57aiwJISCI&feature=youtu.be&t=5220)被宣布。

> 注意：到目前为止，[NVIDIA vendor extension](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html#VK_NV_ray_tracing)公开了在Vulkan上射线跟踪的实现。

## 视频(Video)
目前，Vulkan工作组正在研究如何使Vulkan成为一个展示板载GPU视频编码/解码支持的一流API。更多的信息在 [Siggraph 2019](https://www.youtube.com/watch?v=_57aiwJISCI&feature=youtu.be&t=4948)被宣布。

>注意：到目前为止，还没有公开的支持视频的Vulkan API。

## 机器学习(Machine Learning)
目前，Vulkan工作组正在研究如何使Vulkan成为一个展示现在GPU的ML计算能力的一流API。更多的信息在[Siggraph 2019](https://www.youtube.com/watch?v=_57aiwJISCI&feature=youtu.be&t=5007)被宣布。

>注意：到目前为止，还没有公开的支持机器学习的Vulkan API。


## 安全危急(Safety Critical)
目前，Vulkan工作组正在研究如何使Vulkan可用于安全危急系统。

>注意：到目前为止，还没有公开的可用于安全危急系统的Vulkan API。

