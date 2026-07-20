# Claude Code 安装全流程：从零到真正用起来

> 原文：[https://blog.csdn.net/2302_79751907/article/details/157250313](https://blog.csdn.net/2302_79751907/article/details/157250313)  
> 作者：意疏｜许可：CC BY-SA 4.0

很多人的 AI 用法，卡在“问一句、等一句”。 直到我把 Claude Code 拉进终端，才发现很多事情根本不该自己做。

---

### 🟧 先说说 Claude Code 是什么

Claude Code（简称 CC）是一个运行在终端里的 AI 助手。

它不只是聊天工具，而是真的能帮你干活的助手。

我用它：

- 整理文档、批量重命名文件
- 分析数据、拆分 Excel 表格
- 写代码、调试 Bug

---

### 第一步：装好工具

我们先把工具装好。

跟着步骤来，每一步我都会告诉你怎么确认成功了。~

---

#### 准备三个小工具

先说一句实话。 这一步看起来多，但真正需要你动手的只有一次。 后面所有使用，都是“装完就不再管”的状态。

你需要三个"工具"：

- 魔法工具 emm
- Node.js（一个让程序跑起来的环境）
- Git

安装 Node.js：

去 https://nodejs.org 下载，点绿色的"Get Node.js"按钮。之后根据自己系统下载 Node.js

安装完成后，打开终端（后面会用到），输入：

```
node --version
```

如果出现类似 v24.4.1 的版本号，就说明装好了。

**MAC **可以通过 Homebrew 安装 Node.js（若未安装 Homebrew，可先运行 ：

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

打开终端，运行命令安装 Node.js：

```
brew install nodejs
```

之后输入 node --version可以查看版本，显示版本则表示安装成功。

安装 Git（仅 Windows）：

去 https://git-scm.com/download/win 下载，一直点击"下一步"就可以了。

右键鼠标会看到下图出现两个：Git GUI Here和Git Bash Here

- Git GUI Here是可视化操作工具
- Git Bash Here是Git配套的控制台

在 Git Bash 终端里输入 git –version 查看 git 版本，如图所示，说明 Git 安装成功。

---

#### 安装 Claude Code

现在要用到"终端"了。

什么是终端？

- Windows 电脑：按键盘上的 Win + R，输入 cmd，回车。
- Mac 电脑：按 Command + 空格，输入"终端"，回车。

打开终端后，复制下面这行字，粘贴进去，回车：

```
npm install -g @anthropic-ai/claude-code
```

然后等它自己跑，会出现一堆英文在滚动。

这一步你重点看两个地方：

- 有没有报错
- 是否成功显示版本号

我们可以通过claude --version查看版本

这里会有一个问题了，国内无法访问克劳德code

我们需要设置一下代理模式：（这里需要特殊途径） 我们加入一下代理端口：

```
setx HTTP_PROXY http://127.0.0.1:XXXX 注意：这里是我的端口号 需要根据自身情况来定
setx HTTPS_PROXY http://127.0.0.1:XXXX
```

```
setx ALL_PROXY http://127.0.0.1:XXXX
```

已经配置成功⬇️

我们来检查一下是否能用了：

```
echo %HTTP_PROXY%
echo %HTTPS_PROXY%
```

这时我们输入claude：

我们会发现 必须要开通claude的会员才可以用 这时我们可以调用豆包模型的API来使用claude

---

Claude Code 通常需要翻墙工具和付费订阅，成本太高了 我们这里需要

#### 配置"大脑"（Kimi k2）

Claude Code 是个工具，但它需要一个"大脑"来思考。

这里我们用 Kimi k2，月之暗面出品的模型。

为什么选它？

- 国内的，稳定
- 便宜，新用户有免费额度
- ⬇️API Key管理

我们现在把API 配置到环境变量中去 当然也可以直接使用

控制中心➡️ 编辑系统环境变量➡️环境变量➡️ 新建

```
ANTHROPIC_BASE_URL：https://ark.cn-beijing.volces.com/api/coding
ANTHROPIC_AUTH_TOKEN：你的API。
ANTHROPIC_MODEL: doubao-seed-code-preview-latest。
```

❕注意环境变量设置完 要点击三个确定 不然无法接入API （下面接入API方法 接入别的也是这个流程）

在终端测试环境变量：

```
setx ANTHROPIC_AUTH_TOKEN ARK_API_KEY
setx ANTHROPIC_BASE_URL https://ark.cn-beijing.volces.com/api/coding
setx ANTHROPIC_MODEL doubao-seed-code-preview-latest
```

检查环境变量是否生效

```
echo %ANTHROPIC_AUTH_TOKEN%
echo %ANTHROPIC_BASE_URL%
echo %ANTHROPIC_MODEL%
```

我们可以开始使用啦~

我们在终端输入

```
claude
```

等待一会就会出现：

---

#### 启动 Claude Code

所有准备工作都做完了。

到这一步，Claude Code 就已经可以正常进入工作状态了。

这时候点击Yes （一路Yes就可以）

输入/status

这时候就配置成功了

在终端里，输入：

```
claude
```

几秒后，你会看到 Claude Code 启动了。

试着跟它打个招呼：

```
你好，请介绍一下自己
```

恭喜，你的 AI 助手正式上岗了。
