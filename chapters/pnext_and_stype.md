# pNext 和 sType
刚接触Vulkan的人会开始注意到Vulkan规范中的`pNext`和`sType`变量。

`void* pNext`用于通过在结构之间创建一个链表来扩展Vulkan规范。Vulkan规范中[pNext 有效的用法](https://www.khronos.org/registry/vulkan/specs/1.1/html/vkspec.html#fundamentals-validusage-pNext)这一节深入的解释了`pNext`的两种不同变体。`VkStructureType sType`用于加载器、层，和实现来知道`pNext`传递了什么类型的结构。`pNext`主要用于处理暴露新结构的扩展。

一个展示`pNext` 用法的例子：

```
// An example with two structures, "a" and "b"
// These structs have members you'd find in real Vulkan structures
typedef struct VkA {
    VkStructureType sType;
    void* pNext;
    uint32_t value;
} VkA;

typedef struct VkB {
    VkStructureType sType;
    void* pNext;
    uint32_t value;
} VkB;

// A Vulkan Function that takes struct "a" as an argument
// This function is in charge of populating the values
void vkGetValue(VkA* pA);

// Define "a" and "b" and set their sType
struct VkB b = {};
b.sType = VK_STRUCTURE_TYPE_B;

struct VkA a = {};
a.sType = VK_STRUCTURE_TYPE_A;

// Set the pNext pointer from "a" to "b"
a.pNext = (void*)&b;

// Pass "a" to the function
vkGetValue(&a);

// Use the values which were both set from vkGetValue()
printf("VkA value = %u \n", a.value);
printf("VkB value = %u \n", b.value);
```
