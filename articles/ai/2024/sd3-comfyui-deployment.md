# 丹摩 | SD3与ComfyUI的图像部署实战：从基础到高级的对比分析

> 原文：[https://blog.csdn.net/2302_79751907/article/details/143836472](https://blog.csdn.net/2302_79751907/article/details/143836472)  
> 作者：意疏｜许可：CC BY-SA 4.0

## 丹摩征文活动 | SD3与ComfyUI的图像部署实战：从基础到高级的对比分析

### 背景介绍

Stability AI 推出的 Stable Diffusion 3（SD3）是一款开源的文本生成图像模型，带来了显著的技术突破。其在生成图像的质量、文本语义的理解、对复杂指令的响应以及计算资源的高效利用上均表现出色。

SD3的Medium版本配备了20亿参数，尽管体积小巧，但性能却不容小觑。这一版本可以在普通的个人电脑和笔记本电脑上顺畅运行，方便用户在本地设备上进行部署和操作。

在图像生成方面，SD3展现了出色的能力。无论是细节的刻画、色彩的呈现，还是光影效果的展现，SD3都能做到细致入微。用户只需输入简单的提示词，便可创造出具有动画或厚涂风格的图像，无需进一步的模型微调。

SD3在理解复杂自然语言指令方面也十分突出，能够解析空间结构、构建元素、动作姿态以及风格描述等复杂指令，展现出优于 Midjourney 的文本理解能力。

ComfyUI 是一款基于节点工作流的用户界面，专门用于操作Stable Diffusion模型，包括SD3。用户可以轻松从GitHub下载并安装这款工具。

ComfyUI 提供了直观的操作界面，简化了SD3模型的使用过程，甚至支持图像的批量生成与编辑，大大提高了工作效率和批处理的便捷性。通过ComfyUI，用户无需费心即可轻松掌控SD3模型的强大功能。

### 部署流程

通过丹摩平台，可以访问GPU云实例控制台，只需轻松点击“创建实例”按钮，即可开始创建新的GPU实例。

在实例创建页面，首先选择适合您需求的支付方式。短期使用者可选按需或按日计费，而长期用户则可选择包月套餐以节省成本。对于首次创建实例，建议采用按需计费，并配置1个GPU，选择NVIDIA-GeForce-RTX-4090。该GPU具备60GB内存和24GB显存，能够满足LLaMA3.1 8B版本对至少16GB显存的需求。

调整数据硬盘大小每个实例默认提供50GB存储，但考虑到FLUX.1模型较大的存储需求，建议将硬盘扩展至150GB，以确保充足的存储空间。这种配置将提升实例在处理复杂任务时的效率和稳定性。

选择一个合适的启动镜像。平台提供了多种镜像，其中预装了基础开发环境和框架。您可以通过简单的选择步骤，轻松配置所需的环境，比如直接选择包含PyTorch 2.4.0的镜像，这样做可以省去繁琐的手动安装过程。

为了确保您的账户安全，您需要创建一个新的密钥对，并为其命名。选择自动生成密钥，并确保将私钥文件下载保存到您的电脑上，以便日后能够安全地远程连接到您的服务器。

在密钥对生成完成后，将其选中并执行创建操作。稍作等待，您的实例将顺利启动并准备就绪。

### 登录实例

等待实例创建成功，在 GPU云实例 中查看实例信息。

平台提供了在线访问实例的 JupyterLab 入口，可以直接登录实例：

一旦您登录到服务器，您将自动进入/root/workspace文件夹。要通过SSH连接，您可以使用任何喜欢的客户端，如内置终端、Xshell或MobaXterm。在实例详情页面，所有连接信息一目了然，助您迅速配置并掌控服务器。

复制结果类似如下：

```
ssh -p 31729 root@gpu-s277r6fyqd.ssh.damodel.com
```

其中，gpu-s277r6fyqd.ssh.damodel.com 即主机host，31729 为端口号。

终端登录方式详见SSH登录与密钥对。

### 部署ComfyUI

在终端中执行以下命令克隆ComfyUI代码：

```
# github官方代码仓库
git clone https://github.com/comfyanonymous/ComfyUI.git
# gitCode-github加速计划代码仓库
git clone https://gitcode.com/gh_mirrors/co/ComfyUI.git
```

克隆完成后可看到如下目录：

终端进入/root/workspace/ComfyUI目录，执行以下命令，安装ComfyUI需要的依赖：

```
cd ComfyUI/
pip install -r requirements.txt --ignore-installed
```

执行以下命令，启动ComfyUI：

```
python main.py --listen
```

看到服务成功启动，说明ComfyUI部署成功！

### 部署SD3

从HF-mirror下载SD3模型：

```
pip install -U huggingface_hub

#设置环境变量
export HF_ENDPOINT=https://hf-mirror.com
#下载模型
huggingface-cli download --token hf_BbwgWIQLalWXUdHgvDGPDZpnLxo --resume-download stabilityai/stable-diffusion-3-medium --local-dir .
```

### 生成效果

### 实践心得

我最近体验了Stable Diffusion 3（SD3）和ComfyUI，这两款工具让我对图像生成有了全新的认识。SD3的图像控制精度和元素合成的强大功能，让我能够仅用几个关键词就细致地调整画面的每个细节和风格，这在以前是难以想象的。

ComfyUI的用户界面直观且易于操作，使得整个图像生成流程变得简单明了。从启动应用程序、导入模型、输入描述性文本、微调设置到最终输出图像，每一步都流畅自然，效率极高。特别是ComfyUI的批处理功能，极大地提高了我的工作效率，让我能够一次性处理多个任务。

在实际操作中，我深刻体会到了SD3和ComfyUI的便捷性。安装ComfyUI后，我能够直接从Hugging Face平台下载SD3模型，并将其放置在ComfyUI的模型文件夹中。通过ComfyUI的启动器，我可以轻松加载模型并开始生成图像，可以根据自己的需求调整各种参数，比如采样器、迭代步数和CFG比例，以优化图像的质量和风格。

这种工具的组合不仅简化了图像生成的过程，还让我能够探索更多的创意可能性。SD3和ComfyUI的结合，为我提供了一个强大的平台，让我能够将我的创意想法快速转化为视觉作品。这种体验不仅提高了我的工作效率，还激发了我的创造力，让我对未来的项目充满了期待。
