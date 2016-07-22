为什么 Redox ？
==========
一个自然的问题便是：为什么我们需要另一个操作系统吗？有很多在那里了。
答案是：你不知道。没有人需要一个操作系统。

为什么不贡献别的地方？ Linux呢？ BSD？ MINIX？
-------------------------------------------------- ---

### Linux
还有许多其他操作系统的，内核，无论缺乏贡献者，并在多个编码器的迫切需要。很多时候，这是一个很好的理由。在管理失败，缺乏资金，灵感，或创新，或一组有限的应用程序都导致项目萎缩，并最终失败。

所有这些有许多短塌，漏洞和糟糕的设计选择。 Redox 是不是也不会是完美的，但我们设法改善了其他操作系统。

Linux为例：

- 历史悠久： Old syscalls stay around forever, drivers for long-unbuyable hardware stay in the kernel as a mandatory part. While they can be disabled, running them in kernel space is unnecessary, and can be a source of system crashes, security issues, and unexpected bugs.
- 庞大的库:：To contribute, you must find a place to fit in to nearly _25 million lines of code_, in just the kernel. This is due to Linux's monolithic architecture.
- 非许可认证： Linux is licensed under GPL2, preventing the use of other free software licenses inside of the kernel. More on our use of the MIT X11-style license in [Why Free Software].
- 缺乏内存安全： Linux has had numerous issues with memory safety throughout time. C is a fine language, but for such a security critical system, C is difficult to use safely.

### BSD

这不是什么秘密，我们赞成BSD的是多了，比Linux（虽然我们大多数人仍然是Linux用户，由于种种原因）。这是由于某些安全功能，使一个更可靠的系统的建设，像[jails]和[ZFS]。

BSD是还没有应用：

- 它仍然有一个单一的内核。这意味着单个驱动可以崩溃，挂起，或者在最坏的情况下，导致对系统造成损害。
- 在内核中使用 C 使得它有可能写入内存安全问题的代码。

### MINIX

又是怎么回事MINIX？它的微内核设计是在 Redox 的项目有很大的影响，尤其是像[reliability]的原因。 MINIX是最符合 Redox 的理念。它有一个类似的设计，和一个类似的许可证。

- 使用 C - again, we would like drivers and the kernel to be written in Rust, to improve readability and organization, and to catch more potential safety errors. Compared to monolithic kernels, Minix is actually a very well-written and manageable code base, but it is still prone to memory unsafety bugs, for example. These classes of bugs can unfortunately be quite fatal, due to their unexpected nature.
- 缺少驱动程序支持 - MINIX does not work well on real hardware, partly due to having less focus on real hardware.
- 不太注重 “一切都是文件” - MINIX does focus less on "Everything is a File" than various other operating systems, like Plan9. We are particularly focused on this idiom, for creating a more uniform program infrastructure.

必要性
--------------------------

我们不得不承认，我们不喜欢写东西的想法，是我们自己的（没有发明这里综合征）。有在MINIX 3的源代码，我想做出改变，那么多，也许在 Rust 重写是很有道理的许多地方。

- 不同的VFS模型，基于URL，其中一个程序可以控制整个文件系统分段
- 不同的驱动程序模型，其中驱动程序像网络文件系统接口和音频：提供的功能
- 不同的文件系统，RedoxFS，与正在进行的ZFS实现
- Rust的主要是写入的用户空间
- Orbital，新的GUI

[Why Free Software]: why_free_software.html
[jails]: https://www.freebsd.org/doc/handbook/jails.html
[ZFS]: https://www.freebsd.org/doc/handbook/zfs.html
[reliability]: http://wiki.minix3.org/doku.php?id=www:documentation:reliability
