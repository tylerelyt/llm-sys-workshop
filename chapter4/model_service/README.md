<a id="lesson-1-getting-started-with-open-source-llms"></a>

# 模型调用与生成基础

从服务请求、本地生成和输入包装三个角度理解模型。以下实验各有独立入口：调用 MaaS 不需要下载本地权重，本地生成也不需要服务凭据。

<a id="setup-and-execution"></a>

| 练习 | 运行前提 | 主要观察 |
| --- | --- | --- |
| [模型接口与 Session](SESSION.md) | Python 与兼容 OpenAI 的服务 | 消息、用量，以及应用保存与回传的历史 |
| [Token 与生成预算](TOKENS.md) | Python、本地模型依赖与权重 | 标记化、逐 Token 预测和输出停止位置 |
| [Completion 与 Chat 输入](CHAT.md) | 支持聊天模板的本地模型 | 原始文本、角色消息与编码后的输入 |

第一次调用模型从 Session 开始；理解 NTP 与 Token 时进入本地生成；研究模型输入形式时查看 Chat 模板。各练习说明分别提供命令、可修改位置与观察点。

<a id="next-steps"></a>

## 把模型输入带入应用

用[文档问答](../../chapter6/vector_qa/README.md)追踪资料进入请求的位置，用[对话历史](../../chapter8/conversation_memory/README.md)研究窗口和摘要；模型与接口的原理及参考阅读见[主题目录](../README.md)。

<a id="file-descriptions"></a>

<details>
<summary>其他示例：本地历史、检索与 Flask 多服务</summary>

以下程序各自展示不同的调用方式。在 `chapter4/model_service` 目录、同一套本地模型配置下运行：

```bash
python example3.py
python example4.py
```

`example3.py` 从输入历史找回订单号，修改首条消息中的 `12345` 后重跑，检查它是否跟随新事实。`example4.py` 在没有配置 Google Custom Search 时使用固定教学片段；真实检索路径及服务要求见该脚本的参数和[模型配置](../../README-DEEPSEEK.md)。

Flask 示例使用独立的专家服务与协调者，配置同一份 `OPENAI_*` 变量后，在三个终端从本目录分别启动：

```bash
python agent_a.py
```

```bash
python agent_b.py
```

```bash
python agent_c.py
```

保持服务运行，再向协调者发送请求：

```bash
curl http://127.0.0.1:5002/integrate \
  -H 'Content-Type: application/json' \
  -d '{"task":"先调用 ai_expert 询问 AI 助教收集哪些字段，再调用 law_expert 询问隐私告知，最后汇总两方建议。"}'
```

查看专家服务是否真的收到请求，再核对协调者的回答。端口由 `WORKSHOP_AI_PORT`、`WORKSHOP_LAW_PORT` 和 `WORKSHOP_COORDINATOR_PORT` 设置；在三个终端中保持一致。

这组服务使用 `common.py` 提供的公共函数，与前面的 Session 实验独立运行。

</details>

[主题目录](../README.md) · [全部练习](../../README.md#练习索引)
