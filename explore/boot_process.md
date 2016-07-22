# 引导过程

## 引导程序
要执行的第一个代码是 `kernel/asm/bootsector.asm` 引导扇区。这将加载从第一个分区的引导程序。在 Redox, 引导程序认定在地址 0x100000 处为内核并完全加载它。它还初始化内存映射和 VESA 显示模式，因为这些靠可一旦控制被切换到内，就核不能容易地访问 BIOS 函数。

## 内核
内核通过中断表中输入，伴随 0xFF 中断。该中断仅在引导程序可用。通过利用这种方法，所有的内核条目可以包含到单个功能， `kernel` 功能，在 `kernel/main.rs` 发现, 作为在 `kernel.bin` 文件的入口点.

在此阶段，内核副本存储器映射出低存储器的，设置了一个初始页映射，分配环境目的，在 `kernel/env/mod.rs`, 限定，并且开始初始化嵌入在驱动程序和方案内核。该方法将打印出的内核的信息，如以下内容：

```
Redox 32 bits
  * text=101000:151000 rodata=151000:1A4000
  * data=1A4000:1A5000 bss=1A5000:1A6000
 + PS/2
   + Keyboard
     - Reset FA, AA
     - Set defaults FA
     - Enable streaming FA
   + PS/2 Mouse
     - Reset FA, AA
     - Set defaults FA
     - Enable streaming FA
 + IDE on 0, 0, 0, 0, C120, IRQ: 0
   + Primary on: C120, 1F0, 3F4, IRQ E
     + Master: Status: 58 Serial: QM00001 Firmware: 2.0.0 Model: QEMUHARDDISK 48-bit LBA Size: 128 MB
     + Slave: Status: 0
   + Secondary on: C128, 170, 374, IRQ F
     + Master: Status: 41 Error: 2
     + Slave: Status: 0
```

初始化内核中的结构，驱动程序和方案后，由内核催生了第一个用户空间进程是`init` 进程， 更具体的 `initfs:/bin/init` 进程.

## Init
Redox 具有多级 init 进程，设计为允许磁盘驱动器的模块化和可配置的方式装载。这通常称为初始化虚拟盘。

### Ramdisk Init
Ramdisk 的 init 访问根文件系统，然后转移控制权到用户空间，加载驱动。
这是与内核作为内核部分图像链接和加载的引导程序文件系统。你可以看到在 `init` 进程 `crates/init/main.rs`看到相关代码。

Ramdisk 的初始化加载，默认情况下，文件 `/etc/init.rc`，`initfs/etc/init.rc`。该文件目前拥有的内容：

```
echo ############################
echo ##  Redox OS is booting   ##
echo ############################
echo

# Load the filesystem driver
initfs:/bin/redoxfsd disk:/0

# Start the filesystem init
cd file:/
init
```

因此，它是很容易修改 Redox 加载不同的文件系统作为根，或者在进出虚拟盘的移动过程和驱动程序。

### 文件系统初始化
如上述所示，虚拟盘初始化具有装载和启动文件系统初始化的工作。默认情况下，这将意味着一个新的init进程将催生加载一个新的配置文件，现在在 `filesystem/etc/init.rc`根文件系统。该文件目前拥有的内容：

```
echo ############################
echo ##  Redox OS has booted   ##
echo ##  Press enter to login  ##
echo ############################
echo

# Login process, handles debug console
login
```

修改此文件允许直接引导到 GUI。例如，我们可以用 `login` 代替 `orbital`.

## 登录
初始化过程已经设置了驱动和守护程序后，就可以对用户登录到系统。一个简单的登录程序正在使用的，它的来源可以在 `crates/login/main.rs`

登录程序接受一个用户名，目前可以使用任何用户名，打印 `/etc/motd` 文件，然后执行 `sh`. 。该文件可以配置打印任何消息，它在文件系统 `filesystem/etc/motd` 目前拥有的内容：

```
############################
##  Welcome to Redox OS   ##
##  For GUI: Run orbital  ##
############################
```

At this point, the user will now be able to access the [Shell](./explore/shell.html)
