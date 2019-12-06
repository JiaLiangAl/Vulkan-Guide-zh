# 同步（Synchronization）
同步是使用Vulkan最强大也是最复杂的部分之一。应用程序开发者现在负责使用各种[Vulkan同步原语](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#synchronization)管理同步。不恰当地使用同步会导致难以发现的bug，在GPU不必要地空闲的情况下，性能也会很差。

![synchronization_overview.png](../images/synchronization_overview.png)

## 整体策略（Overall strategies）
这里有个[样例集合](https://github.com/KhronosGroup/Vulkan-Docs/wiki/Synchronization-Examples)，是Khronos提供的关于如何使用一些同步原语。我们的目标是让GPU在这篇托拜厄斯·赫克托(Tobias Hector)的伟大演讲中所描述的那样:[第一部分幻灯片](https://www.khronos.org/assets/uploads/developers/library/2017-vulkan-devu-vancouver/009%20-%20Synchronization%20-%20Keeping%20Your%20Device%20Fed.pdf) ([视频](https://www.youtube.com/watch?v=YkJ4hKCPjm0))和[第二部分幻灯片](https://www.khronos.org/assets/uploads/developers/library/2018-vulkanised/06-Keeping%20Your%20Device%20Fed%20v4_Vulkanised2018.pdf) ([视频](https://www.youtube.com/watch?v=5GDg4OxkSEc))。

## 管道屏障（Pipeline Barriers）
[管道屏障](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#synchronization-pipeline-barriers)控制在执行命令缓冲区时哪些管道阶段需要等待前面的管道阶段。

![synchronization_pipeline_barrieres.png](../images/synchronization_pipeline_barrieres.png)

虽然管道屏障一开始可能很难理解，但有许多伟大的Khronos演讲和其他资源在这个主题上更深入。

- [Vulkanised 2018 -  低层次的管道屏障之谜](https://www.khronos.org/assets/uploads/developers/library/2018-vulkanised/05-The%20low-level%20mysteries%20of%20pipeline%20barriers_Vulkanised2018.pdf) ([视频](https://www.youtube.com/watch?v=e0ySJ9Qzvrs))
- [Vulkanised 2019 - 长寿和优化](https://www.khronos.org/assets/uploads/developers/library/2019-vulkanised/02_Live%20Long%20And%20Optimise-May19.pdf)  ([视频](https://www.youtube.com/watch?v=ch6161wvME8&t=463s)) Pipeline Analysis starting slide 12
- [Vulkan 屏障详解](https://gpuopen.com/vulkan-barriers-explained/) 博客
- [另一个解释Vulkan同步的博客](http://themaister.net/blog/2019/08/14/yet-another-blog-explaining-vulkan-synchronization/)
