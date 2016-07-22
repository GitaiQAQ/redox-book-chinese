探索
===============

从命令行启动 Redox 的图形界面 `orbital`

```sh
$ orbital
```

这应该把你带入轨道GUI如果你运行陷入了终端
`make qemu` 或 `make virtualbox`.

Sodium
------

Sodium 是 Redox 的 Vi-like 编辑器。 在菜单栏，找出 `Na` 的图标。 这个现在应该打开一个编辑器窗口。

默认 Sodium 的简短列表：

- `hjkl`: 导航。
- `ia`: 转到插入模式。
- `;`: 进入命令行模式。
- shift-space: 到正常模式。

对于更广泛的名单，写`; help`。

设置一个提醒/倒计时
----------------------------

为了证明 ANSI 支持，我们会玩弄花哨提醒。

打开终端仿真器。现在，写 `rem -s 10 -b` 。这会设置一个10秒。倒计时与进度条。

玩弄 Rusthello
-----------------------------

Rusthello 是一种先进的黑白棋AI， 由 [Enrico] 开发。它是高并发，所以这证明了 Redox 的多线程功能。它支持各种认可机构，如暴力破解，极大极小，局部优化和混合认可。

哦，让我们尝试一下！

```sh
# first we `cd` to the Rusthello directory
$ cd apps/rusthello
# now, run the binary file
$ ./main.bin
```

那么你会得到提示各种事情，如难度，AI 设置，等等。当做到这一点 ，Rusthello 交互开始你和 AI 或 AI 和 AI 之间的战斗。

探索 OrbTK
---------------

单击菜单栏中的OrbTK演示程序。现在，这将开辟的图形用户界面，显示了OrbTK目前支持的不同的部件。

[Enrico]: https://github.com/EGhiorzi
