# 符号推理方法

研究怎样组织求解过程，以及增加推理步骤和模型调用是否值得。

先了解[模型请求与生成预算](../chapter4/model_service/README.md)。结合专栏学习状态空间、CoT、搜索、自一致性与语言控制器，再用实验区分模型的输出策略和程序的外部调度。

## 组织与核对求解过程

| 练习 | 实验问题 |
| --- | --- |
| [CoT 提示](cot_workflows/PROMPTING.md) | 单次请求中的求解提示改变了什么？ |
| [多轮上下文传递](cot_workflows/CONTEXT.md) | 原任务和中间结果怎样进入下一轮？ |
| [角色与任务交接](cot_workflows/HANDOFF.md) | 分工后，边界条件是否保留到实际代码？ |
| [检查点与停止条件](cot_workflows/CHECKPOINTS.md) | 模型怎样评议候选，程序何时停止？ |
| [自一致性](self_consistency/README.md) | 多个回答达成一致时是否真的正确，格式失败和弃权怎样影响结果？ |

先写出可独立计算的参考答案，再比较单次与多次求解。保持题目和模型一致，记录调用次数与耗时；一次投票成功不足以说明一种策略普遍更好。

## 进入实际工作流

把方法用于自己的任务时，先定义怎样判定正确，再比较新增步骤是否带来收益。需要确定的数学结果时，使用[计算工具](../chapter8/calculator_agent/README.md)；步骤与约束明确时，对照[顺序工作流](../chapter9/sequential_planning/README.md)；需要根据外部结果选择下一步时，进入[工具循环](../chapter8/manual_tool_loop/README.md)。

## 参考阅读

- [CoT：思维链提示激发大模型推理能力](https://arxiv.org/abs/2201.11903)：理解少样本推理示例的作用，对照提示与任务交接实验。
- [大语言模型是零样本推理器](https://arxiv.org/abs/2205.11916)：比较不提供求解示例时的提示策略，并用独立答案检查结果。
- [Self-Consistency：通过多路径采样改善推理](https://arxiv.org/abs/2203.11171)：对照采样、答案归一化与投票，检查额外调用怎样影响正确性和弃权。
- [Tree of Thoughts：审慎求解问题](https://arxiv.org/abs/2305.10601)：结合专栏理解显式搜索、分支评估与回溯，比较它与单次生成、多次投票的控制方式。

[学习地图](../README.md#学习地图) · [模型配置](../README-DEEPSEEK.md#setup)
