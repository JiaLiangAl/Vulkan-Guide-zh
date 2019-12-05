# 内存分配
在Vulkan中管理设备的内存对一些开发者来说可能是比较新的事，了解一些基本知识是很重要的。

两个关于Vulkan内存管理的非常精彩的演讲，[Vulkan Dev Day Montreal](https://www.khronos.org/assets/uploads/developers/library/2018-vulkan-devday/03-Memory.pdf) ([video](https://www.youtube.com/watch?v=rXSdDE7NWmA))和[2018 Vulkanised](https://www.khronos.org/assets/uploads/developers/library/2018-vulkanised/03-Steven-Tovey-VulkanMemoryManagement_Vulkanised2018.pdf) ([video](https://www.youtube.com/watch?v=zSG6dPq57P8))是学习一些主要概念非常好的方式。

同样值得注意的是，管理内存并不容易，开发人员可能希望使用[Vulkan内存分配器](https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator)等库来提供帮助。

## 再分配（Sub-allocation）
在Vulkan中，Sub-allocation被认为是一种一流的方法。同样重要的是要意识到存在一个[maxMemoryAllocationCount](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#limits-maxMemoryAllocationCount)，它会创建一个应用程序可以同时使用的活动分配的数量限制。系统/驱动级别的内存分配和释放可能很慢，这也是再分配的另一个原由。Vulkan应用程序的目标应该是创建大量的分配，然后自己管理它们。

![memory_allocation_sub_allocation.png](../images/memory_allocation_sub_allocation.png)

## 传输（Transfer）
[VkPhysicalDeviceType](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#VkPhysicalDeviceType)声明两种主要不同类型的gpu，分别是独立的和集成的(也称为UMA(统一内存架构))。对于性能来说，理解这两者之间的区别是很重要的。

独立显卡包含它们自己设备上的专用内存。由于传输数据的物理速度限制，数据通过总线（如PCIe）传输，总线通常是一个瓶颈。一些物理设备会用一个`VK_QUEUE_TRANSFER_BIT`声明一个队列，它允许一个专用的队列来传输数据。通常的做法是创建一个 _staging buffer_ 来复制主机数据，然后通过命令缓冲区将数据复制到设备的本地内存中。

UMA系统在设备和主机之间共享内存，这是通过`VK_MEMORY_PROPERTY_DEVICE_LOCAL_BIT | VK_MEMORY_PROPERTY_HOST_VISIBLE_BIT`组合来声明的。这样做的缺点是系统内存必须与GPU共享，这就需要对内存压力保持谨慎。其主要优点是不需要创建 _staging buffer_ ，传输开销也大大减少了。

![memory_allocation_transfer.png](../images/memory_allocation_transfer.png)

## 惰性分配内存（Lazily Allocated Memory）
在基于块的架构(几乎所有的移动gpu)上，`LAZILY_ALLOCATED_BIT`内存类型不受实际内存的支持。它可以用于在块内存中保存的附件，例如子通道、深度缓冲区或多采样图像之间的G-buffer。这为将图像写入内存节省了一些重要的带宽开销。您可以在Khronos的教程[Render Passes](https://github.com/KhronosGroup/Vulkan-Samples/blob/master/samples/performance/render_passes/render_passes_tutorial.md) 和 [Subpasses](https://github.com/KhronosGroup/Vulkan-Samples/blob/master/samples/performance/render_subpasses/render_subpasses_tutorial.md)中找到更多信息。
