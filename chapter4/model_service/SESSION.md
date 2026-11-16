# 模型接口与 Session

通过同一模型的三次请求，区分 MaaS 提供的生成能力和应用维护的对话状态；观察消息、回答、Token 用量与请求耗时。

## 先运行 Session 实验

客服刚确认过工单号，下一次请求却可能回答不知道。本实验向同一模型发送三组消息，检查事实是否真的进入当前输入。

准备 Python 3.11 或 3.12，按[模型配置](../../README-DEEPSEEK.md#setup)填写 `OPENAI_BASE_URL`、`OPENAI_MODEL` 和 `OPENAI_API_KEY`。从仓库根目录运行：

```bash
python -m pip install 'openai>=2,<3'
python chapter4/model_service/maas_session.py --output /tmp/session-baseline.json
```

每次运行发起三次 Chat Completions 请求。依次查看终端打印的服务地址、模型、消息、回答和用量：

| 请求 | 应用发送了什么 | 要检查什么 |
| --- | --- | --- |
| A | 告知本次工单号 | 模型怎样回答，应用保存了哪些消息 |
| B | 在独立消息列表中直接询问工单号 | 输入没有事实时，是否按指令回答“资料不足” |
| C | 回传 A 的消息，再问相同问题 | 工单号来自本轮输入的哪条消息 |

`maas_session.py` 中的 `saved` 与 `independent` 是程序维护的消息列表，每次请求都显式传给服务。Session 在应用侧保存状态，重启脚本会重新建立这些列表。服务端推理缓存与这份对话历史承担不同职责。

`--output` 保存实际消息快照、回答、服务报告的 Token 用量与每次请求耗时。程序还核对 B 是否拒绝猜测、C 是否使用当前工单号；检查失败会返回非零状态。这项检查只针对本例事实，不能替代其他任务的质量评估。

## 改变工单号，检查信息来自哪里

保持模型和追问不变，只改变本次事实：

```bash
python chapter4/model_service/maas_session.py \
  --reference WS-9102 --output /tmp/session-new-reference.json
```

运行前先预测 B、C 的回答，再对照两次请求。检查 C 是否使用新的工单号，B 是否仍说明资料不足。沿 [ask](maas_session.py) 找到历史写入和请求发送的位置，说明状态由谁保存。

## 继续学习

用[本地 Token 实验](TOKENS.md)查看标记化和输出预算，用[Completion 与 Chat 输入](CHAT.md)理解聊天消息的包装；再进入[对话历史管理](../../chapter8/conversation_memory/README.md)，比较窗口与摘要。

[模型基础](../README.md) · [全部练习](../../README.md#练习索引)
