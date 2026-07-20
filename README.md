# 意疏的 AI 产品笔记

这里记录我在 AI 产品、Agent、RAG 和实际项目中的学习与实践。

我会把散落在不同平台的文章逐步整理成更适合长期阅读和维护的 Markdown 版本；文章配图则集中存放在公开的 [ai-product-assets](https://github.com/YiShu5/ai-product-assets) 仓库中，并使用稳定路径引用，避免第三方外链失效。

## 文章目录

| 发布时间 | 文章 | 主题 |
| --- | --- | --- |
| 2025-03-19 | [新手别怕！3 分钟学会扣子（Coze）基础智能体部署](articles/agent/2025/coze-agent-deployment-guide.md) | Coze、智能体、插件、发布 |
| 2026 | [做了 3 个月 AI 产品才明白：记忆分三层，最难的那层叫遗忘](articles/ai/2026/ai-memory-forgetting.md) | AI 产品、记忆、遗忘 |
| 2026 | [全面开源！商汤日日新SenseNova U1发布，迈向模型理解生成统一时代](articles/ai/2026/sensenova-u1-release.md) | SenseNova、多模态、开源模型 |
| 2026 | [我用 Claude Code + 魔珐星云 SDK，10 分钟做了一个会追问的 AI 家电导购](articles/ai/2026/mofa-ai-home-appliance-guide.md) | Claude Code、SDK、AI 导购 |
| 2026 | [《上下文引擎 + Runner 本地操作：基于 openJiuwen 的多轮代码调试智能体》](articles/ai/2026/openjiuwen-debug-agent.md) | openJiuwen、调试智能体、Agent |
| 2026 | [我给 Rokid 眼镜装了个泰酷辣，然后带它去了曼谷](articles/ai/2026/rokid-bangkok-agent.md) | Rokid、智能眼镜、旅行 Agent |
| 2026 | [灵感不再掉线：Rokid 智能眼镜，如何把音乐创作变成随身工作站？](articles/ai/2026/rokid-music-workstation.md) | Rokid、音乐创作、智能眼镜 |
| 2026 | [Claude Code 安装全流程：从零到真正用起来](articles/tools/2026/claude-code-installation.md) | Claude Code、安装、AI 编程 |
| 2026 | [小龙虾一篇讲透，从零到跑起来](articles/tools/2026/xiaolongxia-guide.md) | 工具、部署、教程 |
| 2025 | [《太会玩了！豆包·图像创作模型解锁多图融合，“破次元”趣味合照疯传全网》](articles/ai/2025/doubao-image-creation.md) | 豆包、图像创作、多图融合 |
| 2025 | [AI 总瞎输出？PromptPilot 让 Prompt 百发百中！新手秒上手，首月零元购](articles/ai/2025/promptpilot-review.md) | Prompt、PromptPilot、AI 工具 |
| 2025 | [一句话就能生成完整应用？CodeWave「智能生成应用」真机体验全流程](articles/ai/2025/codewave-app-generation.md) | CodeWave、AI 编程、应用生成 |
| 2025 | [豆包 Doubao-Seed-Code 深度测评：直接换掉 Claude Code！](articles/ai/2025/doubao-seed-code-review.md) | 豆包、Seed-Code、AI 编程 |
| 2025 | [【TextIn大模型加速器 + 火山引擎】当文档解析遇见Agent编排，跨国企业如何实现降本80%的数字化跃迁](articles/ai/2025/textin-volcengine-agent.md) | TextIn、火山引擎、Agent、文档解析 |
| 2025 | [从下载到运行：MySQL 详细安装配置完整教程](articles/database/2025/mysql-installation-guide.md) | MySQL、安装、配置 |
| 2025 | [母婴级 Claude Code 安装教程](articles/tools/2025/claude-code-installation-baby.md) | Claude Code、安装、教程 |
| 2025 | [2025必冲远程工具！网易UU远程：免费无套路，反内卷天花板](articles/tools/2025/netease-uu-remote-review.md) | 网易UU远程、远程控制、工具测评 |
| 2025 | [【MySQL基础】MySQL核心操作全解析](articles/database/2025/mysql-core-operations.md) | MySQL、数据库、SQL |
| 2025 | [CodeBuddy的安装教程](articles/tools/2025/codebuddy-installation.md) | CodeBuddy、安装、AI 编程 |
| 2025 | [Git的安装](articles/tools/2025/git-installation.md) | Git、安装、版本控制 |
| 2025 | [【C语言篇】srand函数的详细用法解析](articles/programming/2025/c-language-srand.md) | C 语言、随机数、srand |
| 2025 | [【C语言篇】猜数字游戏的实现教程](articles/programming/2025/c-language-number-guessing-game.md) | C 语言、项目实践、随机数 |
| 2025 | [【C语言篇】操作符详解](articles/programming/2025/c-language-operators.md) | C 语言、操作符、表达式 |
| 2025 | [5款常用C语言在线编辑器，总有一款适合你](articles/programming/2025/c-language-online-editors.md) | C 语言、在线编辑器、工具 |
| 2025 | [【C 语言篇】常考易错点大盘点：吃透这些，做题少踩坑](articles/programming/2025/c-language-common-pitfalls.md) | C 语言、易错点、学习笔记 |
| 2025 | [【C语言】解决VScode中文乱码问题](articles/programming/2025/vscode-c-chinese-encoding.md) | VS Code、C 语言、编码 |
| 2025 | [全面掌握 C++ 基础：关键特性与进化](articles/programming/2025/cpp-basics.md) | C++、基础语法、编程 |
| 2025 | [【Python】VScode配置Python教程](articles/programming/2025/vscode-python-setup.md) | Python、VS Code、环境配置 |
| 2025 | [【办公软件篇】一步步带你精通--办公神器--Word--如何修改论文](articles/office/2025/word-thesis-formatting.md) | Word、论文、办公软件 |
| 2025 | [华为云Flexus+DeepSeek征文 | DeepSeek-V3/R1 商用服务华为云开通指南及使用体验全解析](articles/ai/2025/huaweicloud-deepseek-guide.md) | DeepSeek、华为云、模型服务 |
| 2025 | [超干货！手把手教你如何在本地部署 DeepSeek，还能实现可视化对话，快速掌握，高效上手！](articles/ai/2025/deepseek-local-deployment.md) | DeepSeek、本地部署、可视化对话 |
| 2024 | [深入了解Markdown：高效笔记与博客写作的终极利器](articles/writing/2024/markdown-guide.md) | Markdown、写作、博客 |
| 2024 | [打造独特的博客封面：动态封面设置指南](articles/tools/2024/dynamic-blog-cover-guide.md) | 博客、动态封面、CSDN |
| 2024 | [丹摩 | SD3与ComfyUI的图像部署实战：从基础到高级的对比分析](articles/ai/2024/sd3-comfyui-deployment.md) | SD3、ComfyUI、图像生成 |
| 2024 | [丹摩 | Llama3.1：从安装到精通的全面对比指南，快速掌握零基础到专业技能的秘诀](articles/ai/2024/llama31-installation-guide.md) | Llama 3.1、大模型、部署 |
| 2024 | [【排序算法篇】---直接插入排序](articles/programming/2024/insertion-sort.md) | 算法、插入排序、Java |
| 2024-07-28 | [C语言新手小白详细教程（3）选择语句](articles/programming/2024/c-language-selection-statements.md) | C 语言、if、switch、分支结构 |
| 2024 | [C语言新手小白详细教程（4）循环语句](articles/programming/2024/c-language-loops.md) | C 语言、while、for、break、continue |
| 2024 | [C语言新手小白详细教程（5）数组](articles/programming/2024/c-language-arrays.md) | C 语言、一维数组、二维数组 |
| 2024 | [C语言新手小白详细教程（6）初步理解函数](articles/programming/2024/c-language-functions-introduction.md) | C 语言、函数、参数、返回值 |
| 2024 | [C语言新手小白详细教程（7）指针和指针变量](articles/programming/2024/c-language-pointers.md) | C 语言、指针、地址、解引用 |
| 2024 | [在Linux操作系统中进行C语言程序的编译与执行](articles/programming/2024/linux-compile-and-run-c.md) | Linux、GCC、C 语言、编译 |
| 2024 | [C语言新手小白详细教程（8）ASCll编码和字符串](articles/programming/2024/c-language-ascii-and-strings.md) | C 语言、ASCII、字符串 |
| 2024 | [【Linux篇】常用命令及操作技巧（基础篇）](articles/programming/2024/linux-basic-commands.md) | Linux、终端、文件操作、命令行 |
| 2024 | [【Linux篇】常用命令及操作技巧（进阶篇 - 上）](articles/programming/2024/linux-advanced-commands-part-1.md) | Linux、远程管理、SSH、用户权限 |
| 2024 | [【Linux篇】常用命令及操作技巧（进阶篇 - 下）](articles/programming/2024/linux-advanced-commands-part-2.md) | Linux、超级用户、权限管理 |
| 2024-07-07 | [C语言新手小白详细教程（2）变量与运算符](articles/programming/2024/c-language-variables-and-operators.md) | C 语言、数据类型、变量、运算符 |
| 2024-06-23 | [C语言新手小白详细教程（1）环境的搭建](articles/programming/2024/c-language-environment-setup.md) | C 语言、VS Code、MinGW |

## 关于我

- GitHub：[YiShu5](https://github.com/YiShu5)
- CSDN：[意疏](https://blog.csdn.net/2302_79751907)

## 版权说明

文章版权与转载规则以每篇文章文首的许可说明为准。引用或转载时，请保留作者信息和原文链接。
