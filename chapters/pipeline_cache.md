# 管道缓存
管道缓存是一种通过[VkPipelineCache](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#VkPipelineCache)对象重用已经创建的管道的技术。管道的创建会有某些开销 —— 比如在被创建时，它必须编译着色色器。管道缓存大的优点在于管道的状态可以保存到文件，以便在应用程序运行之间使用，从而消除了创建过程中一些开销很大的部分。有一个关于管道缓存的精彩演讲来自[SIGGRAPH 2016](https://www.khronos.org/assets/uploads/developers/library/2016-siggraph/3D-BOF-SIGGRAPH_Jul16.pdf)([video](https://www.youtube.com/watch?v=owuJRPKIUAg&t=1045s))，从第140页开始。

![pipeline_cache_cache.png](../images/pipeline_cache_cache.png)

虽然管道缓存是一个重要的工具，但重要的是为它们创建一个健壮的系统，Arseny Kapoulkine在他的[博客](https://zeux.io/2019/07/17/serializing-pipeline-cache/)中谈到了这一点。

为了演示性能提升并查看管道缓存的参考实现，Khronos提供了一个[示例](https://github.com/KhronosGroup/Vulkan-Samples/tree/master/samples/performance/pipeline_cache)和[教程](https://github.com/KhronosGroup/Vulkan-Samples/blob/master/samples/performance/pipeline_cache/pipeline_cache_tutorial.md)。

