例子
===========

理论已经足够了！时间的一个例子。

我们将实现持有的矢量的方案，当你编写时增加元素，并当你阅读时弹出他们。让我们把它叫做 `vec:`.

Let's get going:

代码
--------

因此，首先我们需要导入的事情，我们需要：

```rust
use system::scheme::Scheme;
use system::error::{Error, Result, ENOENT, EBADF, EINVAL};
use std::cmp::min;
```

我们从定义我们的方案结构，这将实行`Scheme`特质并保持计划的状态下启动。

```rust
struct VecScheme {
    vec: Vec<u8>,
}

impl VecScheme {
    fn new() -> VecScheme {
        VecScheme {
            vec: Vec::new(),
        }
    }
}
```

首先我们实现的`open()`。让它接受的引用，这将是向量的初始含量。

请注意，我们忽略了`flags`和`mode`。

```rust
impl Scheme for VecScheme {
    fn open(&mut self, path: &str, _flags: usize, _mode: usize) -> Result<usize> {
        self.vec = path.as_bytes().to_owned();
        Result::Ok(path.len())
    }
```

所以，现在我们执行读取

```rust
    fn read(&mut self, _: usize, buf: &mut [u8]) -> Result<usize> {
        let res = min(buf.len(), self.vec.len());

        for b in buf {
            *b = if let Some(x) = self.vec.pop() {
                x
            } else {
                break;
            }
        }

        Result::Ok(res)
    }
```

现在，我们将添加`write`，这只会增加到向量：

```rust
    fn write(&mut self, _: usize, buf: &[u8]) -> Result<usize> {
        for &i in buf {
            self.vec.push(i);
        }

        Result::Ok(buf.len())
    }
}
```

需要注意的是当调用它们时，离开了缺少的方法导致的错误。

最后，我们需要`main`功能：

```rust
fn main() {
   use system::scheme::Packet;

   let mut scheme = VecScheme::new();
   // Create the handler
   let mut socket = File::create(":vec").unwrap();
   loop {
       let mut packet = Packet::default();
       while socket.read(&mut packet).unwrap() == size_of::<Packet>() {
           scheme.handle(&mut packet);
           socket.write(&packet).unwrap();
       }
   }
}
```

Now, go ahead and test it!

Exercise for the reader
------------------------

Write a scheme that can run `Brainfuck` code.
