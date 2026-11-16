# 预训练语言模型基础

理解模型每次接收什么、怎样生成，以及应用怎样使用 MaaS 提供的能力。

## 从一次请求开始

| 想观察的机制 | 独立练习 | 运行条件 |
| --- | --- | --- |
| MaaS 怎样提供能力、Session 怎样保留状态 | [模型接口与 Session](model_service/SESSION.md) | 兼容 OpenAI 的聊天服务 |
| 标记化、NTP 与输出预算 | [Token 与生成预算](model_service/TOKENS.md) | 本地模型依赖与权重 |
| 文本续写与角色消息如何进入模型 | [Completion 与 Chat 输入](model_service/CHAT.md) | 支持聊天模板的本地模型 |

先比较实际消息、Token 或输入模板，再阅读对应原理；每次保持任务与模型不变，只改变一个输入条件。服务调用、本地生成和模型的训练方式分别理解，各练习不依赖前一项的结果文件。

## 把理解带入系统

为自己的应用画出一次请求：资料从哪里进入、历史存在哪里、哪些信息需要随下一次请求发送。把这份图带入[文档问答](../chapter6/vector_qa/README.md)，观察检索原文怎样加入输入；再看[对话历史管理](../chapter8/conversation_memory/README.md)，研究上下文增长后的取舍。

结合专栏继续学习标记化、自监督、RNN、注意力与 Transformer，理解接口背后的模型机制。

## 参考阅读

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762)：结合专栏理解自注意力、位置编码与 Transformer 结构。
- [BERT：深度双向 Transformer 预训练](https://arxiv.org/abs/1810.04805)：对照自回归生成，理解不同预训练目标与上下文使用方式。
- [语言模型是无监督多任务学习器](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)：理解语言建模目标怎样承载多种任务，并回到实验检查任务文本怎样进入输入。
- [PagedAttention：大语言模型服务的高效内存管理](https://arxiv.org/abs/2309.06180)：理解服务端 KV Cache 管理，与应用保存的 Session 历史区分开来。
- [FlashAttention-2](https://arxiv.org/abs/2307.08691)：从注意力计算的并行与内存访问理解推理基础设施的优化层次。

[学习地图](../README.md#学习地图) · [模型配置](../README-DEEPSEEK.md#setup)
