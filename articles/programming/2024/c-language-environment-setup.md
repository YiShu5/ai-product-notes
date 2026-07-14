# C语言新手小白详细教程（1）环境的搭建

> 作者：意疏
>
> 首次发布：2024-06-23
>
> 更新日期：2024-07-28
>
> 原文：[CSDN](https://blog.csdn.net/2302_79751907/article/details/139897834)
>
> 许可：本文遵循 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.zh-hans) 协议。本文由作者从 CSDN 同步并整理。

## 序

这是一篇面向初学者的 C 语言环境搭建教程。我会尽量使用通俗的表达，把每一步写清楚；如果你已经安装了其他编辑器和 C 编译器，可以直接跳到最后的测试环节。

本文使用的组合是：

- [Visual Studio Code](https://code.visualstudio.com/)
- [MinGW 编译器](https://sourceforge.net/projects/mingw/)

## 1. 安装 VS Code

我推荐使用 VS Code：它拥有丰富的插件生态，可以提供语法高亮、代码补全和调试支持；同时支持 Windows、macOS 和 Linux。

进入 [VS Code 官网](https://code.visualstudio.com/) 后，下载适合自己系统的版本。以下截图以 Windows 为例。

![下载 VS Code](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/01-vscode-download.png)

运行安装程序。

![VS Code 安装向导](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/02-vscode-setup.png)

建议勾选图中的两个选项，方便之后从右键菜单打开文件或目录。

![选择 VS Code 安装选项](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/03-vscode-options.png)

选择一个方便找到的安装目录。

![选择 VS Code 安装目录](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/04-vscode-directory.png)

点击“安装”。

![安装 VS Code](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/05-vscode-install.png)

安装完成后点击“完成”。

![完成 VS Code 安装](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/06-vscode-finish.png)

此时 VS Code 已经可以编辑代码，但还需要安装编译器才能编译和运行 C 程序。

## 2. 安装 MinGW 编译器

进入 [MinGW 官方下载页](https://sourceforge.net/projects/mingw/)，点击“Files”。

![进入 MinGW Files 页面](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/07-mingw-files.png)

选择对应的安装包版本并下载。

![下载 MinGW](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/08-mingw-download.png)

如果下载较慢，可以尝试切换下载镜像。

![切换 MinGW 下载镜像](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/09-mingw-mirror.png)

例如可以选择离自己网络环境较近的镜像源。

![选择 MinGW 下载镜像](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/10-mingw-mirror-select.png)

下载完成后解压安装包。

![解压 MinGW 安装包](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/11-mingw-extract.png)

解压后可以看到 MinGW 文件夹。

![MinGW 解压后的文件夹](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/12-mingw-folder.png)

进入 `bin` 目录，确认其中包含 `gcc.exe` 或 `g++.exe`。

![MinGW bin 目录](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/13-mingw-bin.png)

复制这个 `bin` 目录的完整路径。

![复制 MinGW bin 路径](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/14-mingw-bin-path.png)

### 配置环境变量

在“此电脑”中打开“属性”。

![打开系统属性](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/15-system-properties.png)

进入“高级系统设置”。

![进入高级系统设置](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/16-advanced-settings.png)

点击“环境变量”。

![打开环境变量](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/17-environment-variables.png)

在系统变量中找到 `Path`。

![选择 Path 变量](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/18-path-variable.png)

点击“新建”，粘贴刚才复制的 `bin` 路径。

![添加 MinGW bin 路径](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/19-add-path.png)

确认路径无误后，依次点击“确定”保存。

![确认环境变量设置](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/20-confirm-path.png)

至此，MinGW 的环境变量就配置完成了。

## 3. 配置 VS Code

为了方便写 C 语言代码，可以在 VS Code 扩展市场中安装插件。

如果需要中文界面，可以安装中文语言包。

![安装 VS Code 中文语言包](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/21-vscode-language-pack.png)

然后安装微软提供的 C/C++ 扩展。

![安装 C/C++ 扩展](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/22-vscode-cpp-extension.png)

## 4. 编写并运行第一个 C 程序

在 VS Code 中新建一个文本文件。

![新建文本文件](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/23-new-file.png)

将文件保存为 `.c` 后缀，例如 `test.c`。

![保存 C 文件](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/24-save-c-file.png)

输入下面的代码：

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world!\\n");
    return 0;
}
```

![编写 Hello World 程序](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/25-hello-world-code.png)

打开终端，进入 `test.c` 所在目录后，运行：

```powershell
gcc .\\test.c
.\\a.exe
```

如果终端输出 `Hello, world!`，说明环境已经可以正常使用。

![终端输出 Hello World](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-environment-setup/26-terminal-output.png)

## 结语

至此，VS Code 和 MinGW 的 C 语言开发环境已经搭建完成。下一篇将开始学习 C 语言的基本用法。

> 我是意疏，下次见！
