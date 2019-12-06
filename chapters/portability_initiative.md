# 可移植性倡议（Portability Initiative）
[Vulkan可移植性倡议](https://www.khronos.org/vulkan/portability-initiative)是Khronos集团内部的一项工作，旨在开发资源来定义和发展Vulkan功能的[子集](https://github.com/KhronosGroup/Vulkan-Portability)，这些功能可以在所有主要平台的本机性能级别上普遍可用，包括那些目前没有由Vulkan本机驱动程序提供服务的平台。简而言之，这个计划是为了让Vulkan在不支持API的平台上也能运行（例如 MacOS和iOS）。

![portability_initiative_overview.png](../images/portability_initiative_overview.png)

## MacOS 和 iOS 工具

请参阅新闻稿了解更多关于[macOS和iOS支持的信息](https://www.khronos.org/news/press/vulkan-applications-enabled-on-apple-platforms)。

![portability_initiative_macos.png](../images/portability_initiative_macos.png)

## gfx-rs
Mozilla 现在正在帮助驱动[gfx-rs portability](https://github.com/gfx-rs/portability)使用[gfx-hal](https://gfx-rs.github.io/2017/07/24/low-level.html)作为一种与其他各种api交互的方法。

![portability_initiative_gfxrs.png](../images/portability_initiative_gfxrs.png)


## 翻译层（Translation Layer）
有些项目的目标是获取另一个API并将其映射到Vulkan。翻译层负责接收另一个API(例如OpenGL)并将其映射到等价的Vulkan调用。重要的是要认识到，翻译层只是翻译，不一定实现Vulkan。
- [ANGLE](https://github.com/google/angle)项目是一个例子，OpenGL到Vulkan的翻译层。[SIGGRAPH 2019 Presentation](https://www.youtube.com/watch?v=1fU4w2ZGxH4&feature=youtu.be&t=10822)
- [DXVK](https://github.com/doitsujin/dxvk)项目是一个例子，Direct3D 10/11 到Vulkan的翻译层。
