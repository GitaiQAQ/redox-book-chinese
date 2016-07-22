微内核的缺点
=============================

性能
-----------

任何现代操作系统需要基本的安全机制，如虚拟化和内存分割。 此外任何方法（包括内核）有其自己的堆栈并存储在寄存器中的变量。 在 [Context switch]，每一个系统调用被调用或任何其他的进程间通信（IPC）完成的时间，有些任务必须做，其中包括：

* 保存调用者寄存器，尤其是程序计数器 (调用者: 过程调用或者 IPC)
* 重编程 [MMU] 的页表 (亦称 [TLB])
* 把 CPU 投入另一种模式 (内核模式，用户模式)
* 恢复被调用者寄存器 (被调用者: 系统调用的过程调用或者 IPC)

这些都不是本质上的微内核慢，但微内核必需频繁地执行这些操作而受到影响。许多的系统功能是由用户空间进程执行，需要额外的 Context switch。

集成式核心和微内核之间的性能差异已经随着时间的推移被边缘化，使他们的性能相媲美。这部分是由于其可更容易优化小的表面积。

不幸的是，Redox 还没有应用。我们仍然有相对较慢的内核，因为没有太多的时间来优化它。

[Context switch]: https://en.wikipedia.org/wiki/Context_switch
[MMU]: https://en.wikipedia.org/wiki/Memory_management_unit
[TLB]: https://en.wikipedia.org/wiki/Translation_lookaside_buffer
