# Vulkan 规范（Vulkan Specification）
Vulkan规范(通常称为 _Vulkan Spec_ )是关于Vulkan API如何工作的官方描述，并最终用于确定什么是和不是有效的Vulkan用法。乍一看，Vulkan规范似乎是一个非常巨大的文本块，但它通常是开发时最有用的选项。

> 尽早并经常参考Vulkan规范。

## Vulkan 规范变化
Vulkan规范可以为任何版本和任何扩展排列构建。Khronos组托管[Vulkan Spec注册表](https://www.khronos.org/registry/vulkan/specs/)，其中包含一些大多数开发人员认为足够的公开可用的变体。任何人都可以从[Vulkan-Docs](https://github.com/KhronosGroup/Vulkan-Docs/blob/master/BUILD.adoc)构建自己的Vulkan规范变体。

在构建Vulkan规范时，要传递要为哪个版本的Vulkan构建以及要包含哪些扩展。一个没有任何扩展的Vulkan规范也称为[核心版](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#extendingvulkan-coreversions),因为它是实现Vulkan所需支持的最小数量，为了[一致性](./vulkan_cts.md)。

## Vulkan 规范格式
Vulkan 规范可以以不同的格式构建。

### HTML 分块格式
由于Vulkan规范的大小，当您访问默认的`index.html`页时，块版本是默认的。

例如：[https://www.khronos.org/registry/vulkan/specs/1.1/html/](https://www.khronos.org/registry/vulkan/specs/1.1/html/)

预构建的HTML分块格式Vulkan规范
- Vulkan SDK与该规范的分块版本一起打包，每个Vulkan SDK版本都包含相应的spec版本。见最近的Vulkan SDK的[分块的规范](https://vulkan.lunarg.com/doc/sdk/latest/windows/chunked_spec/index.html)
- [Vulkan 1.0 规范](https://www.khronos.org/registry/vulkan/specs/1.0/html/)
- [Vulkan 1.0 规范与扩展 ](https://www.khronos.org/registry/vulkan/specs/1.0-extensions/html/)
- [Vulkan 1.0 规范与WSI扩展](https://www.khronos.org/registry/vulkan/specs/1.0-wsi_extensions/html/)
- [Vulkan 1.1 规范](https://www.khronos.org/registry/vulkan/specs/1.1/html/)
- [Vulkan 1.1 规范与扩展 ](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/)
- [Vulkan 1.1 规范与KHR扩展](https://www.khronos.org/registry/vulkan/specs/1.1-khr-extensions/html/)

### HTML 完整版
如果你想查看整个Vulkan规范的HTML格式，你只需要查看`vkspec.html`文件。

例如： https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html

预构建的HTML完整版Vulkan规范
- Vulkan SDK与Vulkan规范打包在一起，作为与Vulkan SDK版本对应的版本的HTML。见最近的Vulkan SDK的[HTML 版本的规范](https://vulkan.lunarg.com/doc/sdk/latest/windows/vkspec.html)。（注意：加载慢，完整HTML版本的优点是其搜索功能）。
- [Vulkan 1.0 规范](https://www.khronos.org/registry/vulkan/specs/1.0/html/vkspec.html)
- [Vulkan 1.0 规范与扩展 ](https://www.khronos.org/registry/vulkan/specs/1.0-extensions/html/vkspec.html)
- [Vulkan 1.0 规范规范与WSI扩展](https://www.khronos.org/registry/vulkan/specs/1.0-wsi_extensions/html/vkspec.html)
- [Vulkan 1.1 规范](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html)
- [Vulkan 1.1 规范与扩展](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/html/vkspec.html)
- [Vulkan 1.1 规范与KHR扩展](https://www.khronos.org/registry/vulkan/specs/1.1-khr-extensions/html/vkspec.html)

### PDF
访问`pdf/vkspec.pdf`文件浏览PDF格式版本。

例如: https://www.khronos.org/registry/vulkan/specs/1.1/pdf/vkspec.pdf

预构建的PDF版Vulkan规范
- [Vulkan 1.0 规范](https://www.khronos.org/registry/vulkan/specs/1.0/pdf/vkspec.pdf)
- [Vulkan 1.0 规范与扩展 ](https://www.khronos.org/registry/vulkan/specs/1.0-extensions/pdf/vkspec.pdf)
- [Vulkan 1.0 规范与WSI扩展](https://www.khronos.org/registry/vulkan/specs/1.0-wsi_extensions/pdf/vkspec.pdf)
- [Vulkan 1.1 规范](https://www.khronos.org/registry/vulkan/specs/1.1/pdf/vkspec.pdf)
- [Vulkan 1.1 规范规范与扩展 ](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/pdf/vkspec.pdf)
- [Vulkan 1.1 规范与KHR扩展](https://www.khronos.org/registry/vulkan/specs/1.1-khr-extensions/pdf/vkspec.pdf)

### 手册页
Khronos 组织目前只托管最新的1.1版本规范，包括也有扩展的手册，在[在线注册](https://www.khronos.org/registry/vulkan/specs/1.1-extensions/man/html/)上。

Vulkan对应SDK版本的手册页也可以在每个Vulkan SDK中找到。见最近的Vulkan SDK[主页](https://vulkan.lunarg.com/doc/sdk/latest/windows/apispec.html).
