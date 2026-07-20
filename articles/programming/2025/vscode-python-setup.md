# 【Python】VScode配置Python教程

> 原文：[https://blog.csdn.net/2302_79751907/article/details/148872313](https://blog.csdn.net/2302_79751907/article/details/148872313)  
> 作者：意疏｜许可：CC BY-SA 4.0

---

## 【Python】VScode配置Python教程

前言： 当「Python 编程潜力」遇上「VSCode 开发神器」，会点燃怎样的效率革命？试想这样的场景：你想用 Python 实现创意代码，却困于开发环境的繁琐配置；面对 VSCode 的强大功能，却不知如何让它成为 Python 编程的最佳拍档。现在，一套系统化的配置方案，就能让 VSCode 从「通用编辑器」变身「Python 专属开发舱」—— 智能补全代码、精准调试程序，甚至一键解决中文输出乱码难题！今天，就带大家拆解 Python 在 VSCode 中的环境搭建全流程，看看如何让这对黄金组合从「安装启动」到「高效编码」一气呵成，让代码创作从此告别环境困扰，开启丝滑编程体验。

作者今天格式化了电脑 想用VScode 链接Python结果用不了python 故而出现了这篇文章。

### 下载Python

我们首先要下载Python解释器

- 官网
- 下载页面（Python）

本次以Python 3.9.12-Windows-installer(64-bit)为例子

进入Python

我们往下翻 下载的是这个 中文版：

英文版： 我们下载好之后 点击安装 注意勾选下 添加环境变量 这就代表Python安装成功了 我们现在可以点击Close把它关闭掉

### 安装插件

我们在VScode中 搜索python插件 点击安装 之后可以创建一个demo.py文件 来试着运行下py

### 解决乱码

上面是可以运行的 但是下面输出的是乱码 什么意思的 我们看看 我这里参考了yue佬的 解决vscode中python中文输出乱码问题

点击右上角的那个标志 找到python这列，将后面的 python -u，改为set PYTHONIOENCODING=UTF8 && python -u，之后保存

### 彻底运行

完美解决哈哈哈~

### vscode安装python库

我们点运行之后 提示没有这个模块怎么办呢？

点击运行按钮，运行demo.py文件，从而在Terminal（终端）中得到Python的安装路径； 在Terminal中进入Python安装目录下的Scripts文件夹：输入cd+空格+Python3.7.2的安装路径+\Scripts\；要注意在复制Python的安装路径时不要复制python.exe 代码：cd C:/Users/97034/AppData/Local/Programs/Python/Python39\Scripts\ 确定之后若Terminal（终端）直接出现了文件夹Scripts的路径，则输入：“.\pip install 需要安装库名"，（例如：.\pip install requests），回车后等待安装成功即可； 这里可以看到成功了，我们安装别的库 也是这样

那么我想这就是【Python】VScode配置Python教程的全部内容了~欢迎提问

---

意气风发，漫卷疏狂学习是成长的阶梯，每一次的积累都将成为未来的助力。我希望通过持续的学习，不断汲取新知识，来改变自己的命运，并将成长的过程记录在我的博客中。如果我的博客能给您带来启发，如果您喜欢我的博客内容，请不吝点赞、评论和收藏，也欢迎您关注我的博客。 您的支持是我前行的动力。听说点赞会增加自己的运气，希望您每一天都能充满活力！愿您每一天都快乐，也欢迎您常来我的博客。我叫意疏，希望我们一起成长，共同进步。 我是意疏 下次见！
