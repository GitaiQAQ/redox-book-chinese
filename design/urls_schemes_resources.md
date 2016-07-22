URLs, Schemes, and Resources
============================

这是最重要的 Redox 选择设计选择之一。这三个基本概念都非常纠结。

“一切都在一个URL”是什么意思？
--------------------------------------

“一切都是一个URL” 是 “一切是一个文件”的推广，允许更广泛地使用这种统一的界面方。

这些可用于在 “non-patchworky" 方式有效调节系统。

这个词是相当具误导性，因为 URLs 是方案和资源描述的仅仅是标识。因此，在这个意义上说“一切都是 Schemes，以 URLs 标识”更准确，但也不是很吸引人的。

那么，它是如何从文件中有什么不同？
----------------------------------

你能想到的 URLs 和隔离虚拟文件系统，它可以任意地结构化的（它们不必须是树状）和由程序任意定义。此外， "files" 不必表现 file-like! 更多关于这一点。

它开辟了很多可能性。
> [... TODO]

虚拟文件系统的想法是不是一个新的。如果你是一个Linux的计算机上，你应该尝试`cd`为`/ proc`，看看在那里发生了什么事情。

Redox 扩展了这一理念，更强大。

> TODO