# 丹摩 | Llama3.1：从安装到精通的全面对比指南，快速掌握零基础到专业技能的秘诀

> 原文：[https://blog.csdn.net/2302_79751907/article/details/143836344](https://blog.csdn.net/2302_79751907/article/details/143836344)  
> 作者：意疏｜许可：CC BY-SA 4.0

## 丹摩征文活动 | Llama3.1：从安装到精通的全面对比指南，快速掌握零基础到专业技能的秘诀

### 背景介绍

最近有听说开源大型语言模型（LLM）领域正迎来一场创新浪潮，众多引人瞩目的模型如雨后春笋般涌现，包括LLaMA、Alpaca以及国内的ChatGLM、BaiChuan和InternLM等。这些模型为开发者提供了在本地环境中部署和定制的强大工具，助力他们创造出具有独特价值的应用程序。

2024年7月23日，Meta公司宣布推出Llama 3.1系列模型，这标志着开源模型领域的一个重要进展。特别是Llama 3.1 405B模型，它以4050亿参数和128K Tokens的上下文长度，成为Meta迄今为止最庞大的模型。在训练过程中，该模型处理了超过15万亿的Tokens，并动用了1.6万个H100 GPU，展现了前所未有的规模。

这些新模型的推出不仅带来了新的机遇，也带来了挑战，比如如何针对特定场景优化模型，以及如何确保模型的可解释性和安全性。

### 丹摩部署实例

在本次部署中，将利用丹摩平台的强大功能。开始前，请访问丹摩控制台并启动一个新的GPU云实例。

进入创建页面后，首先在实例配置中选择付费类型，一般短期需求可以选择按量付费或者包日，长期需求可以选择包月套餐。

在创建实例时，推荐选择按需支付模式，并配备一块NVIDIA GeForce RTX 4090 GPU。这款显卡拥有60GB内存和24GB显存，能够应对多种计算任务。其高性能特别适合需要强大计算能力的应用场景。RTX 4090的出色性能和灵活的按需付费选项使得用户可以无忧探索新项目，而不必担心硬件限制。

平台提供多种基础镜像，便于用户快速启动应用。这些镜像预装了必要的环境和工具，用户可根据需求轻松选择。建议选择安装PyTorch框架，并使用其2.4.0版本，以确保兼容性和性能。

为了确保安全登录，请创建一个密钥对，自定义其名称，选择自动生成，并将生成的私钥下载到本地计算机。请将文件后缀修改为.pem，以便后续连接使用。

一旦密钥对创建完毕，选择新生成的密钥对，点击“立即创建”按钮。稍等片刻，系统便会成功启动，准备好让您进行下一步操作。

### 登录实例

在实例完全启动后，前往 GPU 云实例界面以查看详细的实例信息。这样可以确保一切配置正确无误，方便后续使用。

平台提供了可以直接登录实例的 JupyterLab 在线入口，使您能够轻松访问和管理实例，提升整体使用体验。

连接到服务器后，您一般会进入到 /root/workspace 目录，要通过SSH访问，您需准备以下信息，了解路径和信息，将有助于您有效管理和操作服务器资源，确保数据的安全和使用的便捷。在实例界面查看并获取主机名及端口信息。

复制结果类似如下：

```
ssh -p 31729 root@gpu-s277r6fyqd.ssh.damodel.com
```

其中，gpu-s277r6fyqd.ssh.damodel.com 即主机host，31729 为端口号。

终端登录方式详见SSH登录与密钥对。

### 部署Llama3.1

在 DAMODEL 示例中，已预装了 conda 24.5.0 版本。您可以轻松使用 conda 创建新环境，简化了环境管理的步骤，提升工作效率。

```
conda create -n llama3 python=3.12
```

环境创建好后，使用如下命令切换到新创建的环境：

```
conda activate llama3
```

继续安装部署LLama3.1需要的依赖：

```
pip install langchain==0.1.15
pip install streamlit==1.36.0
pip install transformers==4.44.0
pip install accelerate==0.32.1
```

安装好后，下载 Llama-3.1-8B 模型，平台已预制Llama-3.1-8B-Instruct模型，执行以下命令即可内网高速下载：

```
wget http://file.s3/damodel-openfile/Llama3/Llama-3.1-8B-Instruct.tar
```

下载完成后解压缩/Llama-3.1-8B-Instruct.tar

```
tar -xf Llama-3.1-8B-Instruct.tar
```

### 实践教程

模型下载好后，准备加载模型及启动Web服务等工作，新建 llamaBot.py 文件并在其中输入以下内容：

```
from transformers import AutoTokenizer, AutoModelForCausalLM
import torch
import streamlit as st

# 创建一个标题和一个副标题
st.title("💬 LLaMA3.1 Chatbot")
st.caption("🚀 A streamlit chatbot powered by Self-LLM")

# 定义模型路径
mode_name_or_path = '/root/workspace/Llama-3.1-8B-Instruct'

# 定义一个函数，用于获取模型和tokenizer
@st.cache_resource
def get_model():
 # 从预训练的模型中获取tokenizer
 tokenizer = AutoTokenizer.from_pretrained(mode_name_or_path, trust_remote_code=True)
 tokenizer.pad_token = tokenizer.eos_token
 # 从预训练的模型中获取模型，并设置模型参数
 model = AutoModelForCausalLM.from_pretrained(mode_name_or_path, torch_dtype=torch.bfloat16).cuda()
 
 return tokenizer, model

# 加载LLaMA3的model和tokenizer
tokenizer, model = get_model()

# 如果session_state中没有"messages"，则创建一个包含默认消息的列表
if "messages" not in st.session_state:
 st.session_state["messages"] = []

# 遍历session_state中的所有消息，并显示在聊天界面上
for msg in st.session_state.messages:
 st.chat_message(msg["role"]).write(msg["content"])

# 如果用户在聊天输入框中输入了内容，则执行以下操作
if prompt := st.chat_input():
 
 # 在聊天界面上显示用户的输入
 st.chat_message("user").write(prompt)
 
 # 将用户输入添加到session_state中的messages列表中
 st.session_state.messages.append({"role": "user", "content": prompt})

 # 将对话输入模型，获得返回
 input_ids = tokenizer.apply_chat_template(st.session_state["messages"],tokenize=False,add_generation_prompt=True)
 model_inputs = tokenizer([input_ids], return_tensors="pt").to('cuda')
 generated_ids = model.generate(model_inputs.input_ids,max_new_tokens=512)
 generated_ids = [
 output_ids[len(input_ids):] for input_ids, output_ids in zip(model_inputs.input_ids, generated_ids)
 ]
 response = tokenizer.batch_decode(generated_ids, skip_special_tokens=True)[0]

 # 将模型的输出添加到session_state中的messages列表中
 st.session_state.messages.append({"role": "assistant", "content": response})
 # 在聊天界面上显示模型的输出
 st.chat_message("assistant").write(response)
 print(st.session_state)
```

在终端中运行以下命令，启动 streamlit 服务，server.port 可以更换端口：

```
streamlit run llamaBot.py --server.address 0.0.0.0 --server.port 1024
```

需注意服务地址务必指定位0.0.0.0，否则无法通过浏览器访问

接下来我们需要通过丹摩平台提供的端口映射能力，把内网端口映射到公网；

进入GPU 云实例页面，点击操作-更多-访问控制：

点击添加端口，添加streamlit服务对应端口：

添加成功后，通过访问链接即即可打开LLaMA3.1 Chatbot交互界面，并与其对话：
