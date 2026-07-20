# 母婴级 Claude Code 安装教程

> 原文：[https://blog.csdn.net/2302_79751907/article/details/154980692](https://blog.csdn.net/2302_79751907/article/details/154980692)  
> 作者：意疏｜许可：CC BY-SA 4.0

### 我来介绍一下克劳德code的安装方式：

提示：这篇文章适合有一点点基础的同学，没有基础勿看！

首先我们需要安装一下node 这里我之前安装过 不在介绍。

我们输入：

```
node --version
```

```
npm --version
```

之后需要安装git ： 我之前的链接：git的安装

这里如果调用命令行来运行git显示不成功的话 那么就代表没有配置环境变量 我们需要配置环境变量

首先我的git在E盘（节省空间）

我们点击环境变量 ➡️ 用户变量 ➡️ PATH

我们新建 分别添加：

```
E:\Git\Git\bin
E:\Git\Git\cmd
```

然后点击 确定 ➡️ 确定 ➡️ 确定

之后打开命令提示符 输入：

```
git --version
```

⬆️ 已经成功看到git了

这时需要通过npm 来下载claude-code

```
npm install -g @anthropic-ai/claude-code
```

但我们会发现 下载是很慢的 ，这时候需要切换淘宝镜像

```
npm config set registry https://registry.npmmirror.com
```

```
npm install -g @anthropic-ai/claude-code
```

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

我们会发现 必须要开通claude的会员才可以用 这时我们可以调用k豆包模型的API来使用claude

我们进入：豆包 API

⬇️API Key管理

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

这时候点击Yes （一路Yes就可以）

输入/status

这时候就配置成功了
