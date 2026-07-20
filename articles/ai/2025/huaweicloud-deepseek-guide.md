# 华为云Flexus+DeepSeek征文 | DeepSeek-V3/R1 商用服务华为云开通指南及使用体验全解析

> 原文：[https://blog.csdn.net/2302_79751907/article/details/148867501](https://blog.csdn.net/2302_79751907/article/details/148867501)  
> 作者：意疏｜许可：CC BY-SA 4.0

828 B2B企业节已经开幕，汇聚千余款华为云旗下热门数智产品，更带来满额赠、专属礼包、储值返券等重磅权益玩法，是中小企业和开发者上云的好时机，建议密切关注官方渠道，及时获取最新活动信息，采购最实惠的云产品和最新的大模型服务！」

### 前言：

想象一下，你现在为项目方案绞尽脑汁，急需 AI 强大的数据分析与创意支持；或是在海量数据中苦苦搜寻关键信息，渴望想有一个智能助手快速支持你。现在，华为云 Flexus 与 DeepSeek-V3/R1 商用服务，就是你的理想方案。无论是开通，还是如何高效使用，我都将为你全方位解析。

### 在华为云平台开通 DeepSeek-V3/R1 商用服务

### 一、帐号准备工作

- 注册登录与实名认证使用华为云账号登录，登录之后需要实名认证 进入实名认证验证身份证或银行卡，出现通过华为云实名认证就可以了。 我们首先进入华为云首页 点击左上角红框的控制台点击可用额度 目前看到总额度为0，我们点击充值（我这里充值10元） 这里可以看到 已经充值了10元并到账，现在准备工作都已完毕，我们可以正式开始了~

#### 正式登陆

我们验证完毕 返回华为云首页 点击红框 首先同意服务声明 之后点击左边的模型推理 下面的 在线推理 可以看到有 DeepSeek-V3/R1 服务 这里选择的是DeepSeek-R1，读者可自行选择 点击立即开通 静静等待约1-2分钟，系统自动完成服务部署，状态变为绿色的 “开通” 即表示开通成功。 获取API调用信息 在 “在线推理” 页面，找到已开通的DeepSeek-V3/R1服务，点击 “调用说明”。 这里需要记录下接口信息 方便调用 点击API Key管理 点击创建API 这里可以随便输入标签 以及描述（如果有特殊需求 可以根据您的需求来设置名称） 这里就可以看到密钥了 我们有了接口信息以及密钥 现在可以正式使用啦~

### 二、Rest API调用

我们点击模型推理 ->在线推理 我们获取API Key 和API地址之后 复制到代码中 这时我们把前面的API地址 和后面的API Key都输入到代码中 注意要输入你的地址。

```
# coding=utf-8
import requests
import json
 
url = "你的API地址" # API地址
api_key = "你的API Key" # 替换为你的API Key
 
headers = {
 'Content-Type': 'application/json',
 'Authorization': f'Bearer {api_key}'
}
 
data = {
 "model": "DeepSeek-R1", 
 "messages": [
 {"role": "system", "content": "你是一名AI助手"},
 {"role": "user", "content": "用Python实现快速排序"}
 ],
 "temperature": 0.6,
 "stream": False # 关闭流式输出
}
 
response = requests.post(url, headers=headers, json=data)
print(f"状态码: {response.status_code}")
print("响应结果:")
print(json.dumps(response.json(), indent=2, ensure_ascii=False))
```

输入结果

### 三、OpenAI SDK调用

需要先安装下环境pip install --upgrade "openai>=1.0" 之后复制并运行代码 代码：

```
# coding=utf-8

from openai import OpenAI

base_url = "https://api.modelarts-maas.com/v1" # API地址
api_key = "你的API Key" # 把yourApiKey替换成已获取的API Key

client = OpenAI(api_key=api_key, base_url=base_url)

response = client.chat.completions.create(
 model = "DeepSeek-R1", # 模型名称
 messages = [
 {"role": "system", "content": "你是一个资深的计算机博士"},
 {"role": "user", "content": "请写一个二分查找算法"},
 ],
 temperature = 1,
 stream = True
)

print(response.choices[0].message.content)
```

运行结果

### 四、REST API 和OpenAI SDK 对比测评

### 五、使用建议

#### 5.1✅ 使用 REST API 的建议：

- 适合跨语言开发：如果你使用的是非 Python 语言（如 JavaScript、Java、Go 等），REST API 更加通用。
- 适用于嵌入式或轻量系统：在不方便安装 SDK 的环境中（如前端应用、嵌入式设备）推荐使用。
- 更灵活可控：需要完全掌控请求细节或与其他 HTTP 服务打通时，REST API 提供更多自由度。

#### 5.2✅ 使用 OpenAI SDK 的建议：

- 推荐 Python 开发者使用：封装好函数接口，简化调用，极大提升开发效率。
- 适合快速原型开发：调试和集成速度快，适用于科研、测试和项目验证阶段。
- 自动管理连接和异常：相比手写 HTTP 请求，SDK 处理更健壮，减少出错可能。

### 六、常见问题

Q1: 如何安装Python包： A:可以参考这个链接 VScode中安装python包

Q2: 不实名可以用吗： A:不可以

Q2: 需要充值多少元： A:最好10元 或者比10元高

828 B2B企业节已经开幕，汇聚千余款华为云旗下热门数智产品，更带来满额赠、专属礼包、储值返券等重磅权益玩法，是中小企业和开发者上云的好时机，建议密切关注官方渠道，及时获取最新活动信息，采购最实惠的云产品和最新的大模型服务！

欢迎提问❤
