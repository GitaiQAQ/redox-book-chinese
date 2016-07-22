# GUI

Redox 的桌面环境， 被称为 Orbital, 是由一组在用户空间运行的程序提供：

## Programs
以下是提供 GUI 服务命令行实用程序

### orbital
Orbital 显示器和窗口管理器设置： 方案，管理的显示，并且对窗口创建处理请求，重绘和事件轮询

### launcher
它可以扫描在 `/apps/` 目录下的应用，并提供以下服务的启动多用途程序：

#### Called Without Arguments
显示的图标为每个应用程序任务栏

#### Called With Arguments
在匹配程序打开文件的应用程序选择器
- 如果一个应用程序发现匹配时，它将被自动打开
- 如果找到一个以上的应用程序，选择器将显示

## Applications
以下是可以在 `/apps/` 目录下找到 GUI 工具。

## Calculator
它提供的功能类似于 `calc` 程序的计算器

## Editor
一个简单的编辑器类似记事本

## File Browser
显示图标，名称，大小和细节的文件的文件浏览器。在单击时，它使用`launcher`命令来打开文件

## Image Viewer
一个简单的图像浏览器

## Pixelcannon
三维渲染器，可用于基准的 Orbital 桌面。

## Sodium
A vi-like editor that provides syntax highlighting

## Terminal Emulator
An ANSI terminal emulator that launches `sh` by default.
