Schemes
=======

Schemes 是原生的对应于 URL。网址被 Schemes 打开，然后可将 Schemes 打开，以产生一个资源。

Schemes 被命名为使得所述内核是能够唯一地识别它们。此名称在URL中的 `scheme` 的一部分使用。

Schemes 是文件系统的推广。应当指出的是 schemes 不一定代表正常的文件;它们往往是一个 "虚拟文件" (即，一个抽象的与在其上定义的某些操作单元).


整个 Redox 方案的整个生态系统，因为它们是一个强大的抽象用作主要通信原码。随着方案 Redox 能有一个统一的 I/O 接口。

Schemes 既可以定义在用户空间与内核空间，但是应当可能的在用户空间。

Scheme operations
-----------------

What makes a scheme a scheme? Scheme operations!

一个 scheme 仅仅是一个数据结构上定义某些功能：

1. `open` - 打开 scheme. `open` 最初用于开始与 scheme 沟通; 它是一个可选的方法，并且将默认为返回 `ENOENT`.

2. `mkdir` - 创建新的子结构。注意，该名称是有点误导（它甚至可能在将来被重新命名），因为在许多方案 `mkdir` 不会创建 `directory`, 而是进行某种形式的子创作的。

可选的方法包括：

1. `unlink` - 除去一个链路（即从一个子结构到另一个的结合）。

2. `link` - 添加一个链接。
