# Completion 与 Chat 输入

查看原始文本续写和角色消息两种输入，理解聊天模板如何把消息变成 Token，以及输入形式与模型训练方式的关系。

## 独立运行

使用 Python 3.11 或 3.12；本练习加载本地权重，不需要先运行 Session 或 Token 实验。

```bash
python -m pip install -r chapter4/model_service/requirements.txt
cd chapter4/model_service
export WORKSHOP_LOCAL_MODEL=Qwen/Qwen2.5-0.5B-Instruct
python example2.py
```

首次运行需要下载模型，已有权重时可将变量设为本地路径。模型需支持聊天模板；模型与依赖说明见[模型基础实验](README.md)。

## 跟踪输入包装

在 [example2.py](example2.py) 中依次找到 `messages`、`apply_chat_template`、编码输入和生成结果。对照终端打印的角色消息与模板文本，指出用户内容之外还添加了哪些边界标记。

保持模型与原有诗歌任务不变，只在本地副本中将编码对象从 `prompt` 换成 `instruction`，比较输入 Token 与生成结果。两种路径分别是角色消息经模板包装、原始任务文本直接续写；保留同一任务才有可比性。

Chat 接口接收角色消息，传统 Completion 接口接收文本起点；是否经过基础预训练、指令或对话后训练是模型属性，包装输入不会更新权重。本例复用同一指令模型来观察输入形式，没有比较两个不同训练阶段的模型；MaaS 是否同时开放两种接口，取决于服务支持。

[模型接口与 Session](SESSION.md) · [Token 与生成预算](TOKENS.md) · [全部练习](../../README.md#练习索引)
