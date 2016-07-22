准备构建
====================

哇！你说得那么远，一路到这里。恭喜！现在，我们得 Redox.

_如果你懒，和Linux或Mac系统的计算机上。那么，你是今天的赢家！只要运行该脚本的引导，它不生成准备为您提供：_

```sh
$ curl -sf https://raw.githubusercontent.com/redox-os/redox/master/bootstrap.sh -o bootstrap.sh && bash -e bootstrap.sh
```

哦，你不懒？好了，那么接下来的部分是为你！

Cloning the repository
----------------------
 
 ```sh
 $ git clone https://github.com/redox-os/redox.git && cd redox && git submodule update --init
 ```
 
 Give it a while. Redox is big.
 

手动安装编译依赖
------------------------------------------


我假设你有一个包管理器，你知道如何使用（如果没有，你必须手动安装编译依赖）。我们需要以下DEPS：`make`（可能已经安装），`nasm`（汇编，我们在构建过程中使用），`qemu`（硬件仿真器，我们将使用如果你想真实运行的氧化还原。硬件，你应该阅读`fun`章）:)

```
$ [your package manager] install make nasm qemu
```

而接下来的步骤是不_required_，建议。如果你已经有了一个有效的 Rust 夜间安装，您可以跳过此步骤：

我们将使用`rustup`来管理我们的 Rust 版本：

```sh
$ curl https://sh.rustup.rs -sSf | sh
```

Rustup 将安装 `stable` 版本。要运行 Redox, 您必须安装 `nightly` 版本，就像这样：

```sh
$ rustup toolchain install nightly
$ rustup override set nightly
```
