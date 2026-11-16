<a id="lesson-4-advanced-reasoning-with-llms"></a>

# CoT 与推理编排

单次提示、多轮上下文、角色分工和检查点分别改变求解过程的不同部分。以下实验各自使用已有输入与独立脚本，不依赖前一项的输出文件。

<a id="file-descriptions"></a>

| 练习 | 固定什么、改变什么 | 主要实现 |
| --- | --- | --- |
| [CoT 提示](PROMPTING.md) | 固定算式与模型，只改变求解提示 | [example1.py](example1.py) |
| [多轮上下文传递](CONTEXT.md) | 固定预算任务，只改变中间结果的传递 | [example2.py](example2.py) |
| [角色与任务交接](HANDOFF.md) | 固定读数与分工，只改变提醒阈值 | [example3.py](example3.py) |
| [检查点与停止条件](CHECKPOINTS.md) | 固定耗材任务，只注入一处错误候选 | [example4.py](example4.py) |

<a id="setup-and-execution"></a>

## 运行与比较

各入口分别提供依赖、命令与观察方法。先独立算出对应任务的参考值，再预测修改后的结果；从实际提示与执行流程解释变化，不能用回答变长或模型自评代替判断。

CoT 提示作用于一次生成，多轮编排由程序重新组织上下文；检查点由模型给出评议、程序执行继续或停止。需要比较多次采样与投票时，进入[自一致性](../self_consistency/README.md)。

<a id="next-steps"></a>

## 继续构建系统

步骤固定时对照[顺序工作流](../../chapter9/sequential_planning/README.md)，下一步依赖实际工具结果时进入[工具循环](../../chapter8/manual_tool_loop/README.md)。原理与论文见[推理方法](../README.md#参考阅读)。

[主题目录](../README.md) · [课程首页](../../README.md)
