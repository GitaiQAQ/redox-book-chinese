微内核
============

Redox 的内核是微内核。 微内核在他们的设计中脱颖而出是由于在内核空间提供最小的抽象。 微内核侧重用户空间，不同与集成式内核侧重内核空间。

微内核的基本理念是任何组件，它*可以* 并且*应该*在用户空间运行。内核空间应该只被用于最本质的组件（例如，系统调用，过程分离，资源管理，IPC，线程管理，等等）。

内核的主要任务是充当沟通和流程分离的媒介。内核应提供最少抽象在硬件（即，它可以并且应该在用户模式下运行的驱动程序）。

微内核比集成式内核更安全，不容易崩溃。这是由于驱动程序和其他抽象是特权较少，所以不能做到对系统造成损害。此外，微内核是非常容易维护，由于其代码量小，这可能会减少在内核bug数量。

至于别的，微内核做也有缺点。我们将在后面讨论这些。

相对于集成式内核
-------------------------

集成式内核提供比微内核更大量的抽象。

![例证]

上图([from Wikimedia], by Wooptoo, License: Public domain) 显示了它们的区别。

> TODO

当前的状态的说明
---------------------------

Redox 有 ~16,000 行内核代码。为了对比 Minix 的 ~6,000 行。

我们想 Redox 部分移动到用户空间以获得一个更小的内核。

[例证]: https://upload.wikimedia.org/wikipedia/commons/6/67/OS-structure.svg
[from Wikimedia]: https://commons.wikimedia.org/wiki/File:OS-structure.svg