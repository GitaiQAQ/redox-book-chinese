URLs
====

URL _itself_ 是 Redox 的设计中比较没意思的（但很重要）的概念。有趣的部分是它代表什么。

The URL
-------

总之，一个URL是一个资源的标识符。它们包含两个部分：

1. scheme 的一部分。这代表了“接收器”，即有什么计划将处理（F）OPEN 调用。这可以是任意 UTF-8 字符串，并且通常仅仅是你的协议的名称。

2. 参考部分。这代表了URL，即什么URL是指“有效载荷”。考虑`file`，作为一个例子。以 `file:` 的 URL 只是有一个参考这是一个文件的路径。基准可以是任意字节串。解析，解释和参考的存储留给scheme因为这个原因，它是不要求是一个树形结构。

因此，一个URL的字符串表示的样子：

```
[scheme]:[reference]
```

例如：

```
file:/path/to/myfile
```

注意，`//`不是必需的，以方便使用。

Opening a URL
-------------

URLs 可以被打开，yielding _schemes_, 其可被资源打开，其可以被读，写和（对于某些资源）seeked（有这些后述的详细操作）。

出于兼容性考虑，我们用类似于Rust 标准库文件API来打开 URLs：

```rust
use std::fs::OpenOptions;
use std::io::prelude::*;


fn main() {
    // Let's read from a TCP stream
    let tcp = OpenOptions::new()
                .read(true) // readable
                .write(true) // writable
                .open("tcp:0.0.0.0");
}
```

> TODO: Maybe do something with the tcp stream. Ping-pong?

> TODO: 该术语可能是对读者有所混淆。
