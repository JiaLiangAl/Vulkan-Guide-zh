# 线程（Threading）
Vulkan和OpenGL之间一个很大的不同点是，Vulkan不是限制在单线程中的状态机系统。在运行以实现应用程序中的线程之前，了解线程在Vulkan中的工作方式非常重要。

Vulkan规范[线程行为](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#fundamentals-threadingbehavior)详细地阐述了应用程序如何负责管理所有的 _外部同步的_ Vulkan元素。必须认识到，Vulkan中的多线程只提供了主机端扩展，因为与设备交互的任何东西仍然需要[正确地同步](./sychronization.md)

Vulkan实现不应该引入任何多线程，所以如果一个应用程序需要多cpu性能，那么这个应用程序将负责管理线程。


## 命令池（Command Pools）
[命令池](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#commandbuffers-pools)是一个允许跨多线程记录命令缓冲区的系统。单个命令池必须是 _外部同步的_ ;不能从多个线程同时访问它。通过在每个主机线程中使用单独的命令池，应用程序可以并行创建多个命令缓冲区，而不需要任何昂贵的锁

其思想是命令缓冲区可以记录在多个线程上，同时有一个相对较轻的线程处理提交。

![threading_command_buffers.png](../images/threading_command_buffers.png)

Khronos的[例子](https://github.com/KhronosGroup/Vulkan-Samples/tree/master/samples/performance/command_buffer_usage)和[教程](https://github.com/KhronosGroup/Vulkan-Samples/blob/master/samples/performance/command_buffer_usage/command_buffer_usage_tutorial.md)更详细地展示了如何并行地记录命令缓冲区。

## 描述符池（Descriptor Pools）

[描述符池](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#VkDescriptorPool)用来分配，释放，重置和更新描述符集。通过创建多个描述符池，每个应用程序宿主线程都能够同时管理每个描述符池中的描述符集。
