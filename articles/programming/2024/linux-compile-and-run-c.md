# 在Linux操作系统中进行C语言程序的编译与执行

> 原文：[在Linux操作系统中进行C语言程序的编译与执行](https://blog.csdn.net/2302_79751907/article/details/141528889)  
> 作者：意疏｜许可：CC BY-SA 4.0

这篇记录在 Linux 终端中安装编辑器与 GCC、创建 C 源文件、编译并运行程序的基础流程。

## 安装工具

以 Debian/Ubuntu 为例：

```bash
sudo apt update
sudo apt install gcc vim
```

安装后可确认 GCC 是否可用：

```bash
gcc --version
```

## 创建并编辑源文件

```bash
mkdir -p ~/c-demo
cd ~/c-demo
vim hello.c
```

写入：

```c
#include <stdio.h>

int main(void) {
    printf("Hello, Linux!\n");
    return 0;
}
```

## 编译与运行

```bash
gcc hello.c -o hello
./hello
```

`gcc hello.c -o hello` 会把源文件编译为名为 `hello` 的可执行文件；`./hello` 表示执行当前目录下的该文件。若编译出现报错，应优先根据终端给出的文件名、行号和错误信息定位语法问题。

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
