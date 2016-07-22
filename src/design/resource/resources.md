Resources
=========

资源被 schemes 打开。你可以理解它们像 schemes 供应商和客户之间建立的连接。

资源与 schemes 紧密连接，有时和 schemes 纠缠在一起。在 schemes 与资源之间的不同是细微而重要的。

资源操作
-------------------

资源可以被定义为与在其上定义的下列方法的数据类型：

1. `read` - 读N个字节为参数提供一个缓冲。默认为 `EBADF`
2. `write` - 写缓冲器到资源。默认为 `EBADF`.
3. `seek` - 查询资源。移动 “游标” 而无需编写。许多资源不支持此操作。默认为 `EBADF`.
4. `close` - 关闭资源，潜在地解除锁定。默认为 `EBADF`.

> TODO add F-operations.

资源类型
-----------------

有两种类型的资源：

1. File-like 资源。这些表现很像文件。他们的行为以阻塞的方式; 读取和写入 "buffer-like"。
2. Socket-like 资源。 这些行为类似于套接字。他们的行为在非阻塞的方式;读取和写入更多的 "stream-like".

> TODO Expand on this.
