# 什么是JS

一种脚本语言，可以用来创建动态更新的内容，控制多媒体，制作图像动画，还有很多

API内建于web浏览器中，一套代码组件，分为：

- 浏览器API
- 第三方API

JavaScript 是轻量级解释型语言。浏览器接受到 JavaScript 代码，并以代码自身的文本格式运行它。技术上，几乎所有 JavaScript 转换器都运用了一种叫做**即时编译**（just-in-time compiling）的技术；当 JavaScript 源代码被执行时，它会被编译成二进制的格式，使代码运行速度更快。尽管如此，JavaScript 仍然是一门解释型语言，因为编译过程发生在代码运行中，而非之前。

## async 和 defer

上述的脚本阻塞问题实际有两种解决方案——`async` 和 `defer`。我们来依次讲解。

浏览器遇到 `async` 脚本时不会阻塞页面渲染，而是直接下载然后运行。但是，一旦下载完成，脚本就会执行，从而阻止页面渲染。脚本的运行次序无法控制。当页面的脚本之间彼此独立，且不依赖于本页面的其他任何脚本时，`async` 是最理想的选择。

使用 `defer` 属性加载的脚本将按照它们在页面上出现的顺序加载。在页面内容全部加载完毕之前，脚本不会运行，如果脚本依赖于 DOM 的存在（例如，脚本修改了页面上的一个或多个元素），这一点非常有用。

以下是不同脚本加载方法的可视化表示，以及这对页面意味着什么：

  ![三种脚本加载方法的工作原理：默认情况下，在获取和执行 JavaScript 时，解析过程被阻塞。使用 async 时，解析暂停，仅执行。使用 defer 时，解析不会暂停，但在解析完所有其他内容后才开始执行](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/What_is_JavaScript/async-defer.jpg)

https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/What_is_JavaScript/async-defer.jpg

## 变量

变量是一个用来存值的容器