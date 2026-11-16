# 多轮上下文传递

在多次独立请求之间显式传入中间结果，检查预算、数量和原始约束能否一路保留。

## 起点与运行

使用课程 Python 3.11 或 3.12 环境，从仓库根目录安装依赖，并按[模型配置](../../README-DEEPSEEK.md#setup)设置 `OPENAI_BASE_URL`、`OPENAI_MODEL`、`OPENAI_API_KEY`：

```bash
python -m pip install -r chapter7/cot_workflows/requirements.txt
python chapter7/cot_workflows/example2.py
```

已有任务是为23人采购耗材，总预算200美元，每包32美元含5套，场地预留35美元。先独立算出5包、总费用195美元、剩余5美元，再读各轮实际输出。

## 跟踪历史来自哪里

在 [cross_session_reasoning](example2.py) 中找到 `previous_answers`、每轮 `history` 和最后的 `final_prompt`。每次请求只有应用重新拼出的消息；同一模型名称不会替程序保存前轮答案。

保持原任务、问题顺序与模型不变，只将循环中 `history` 的值改成 `None yet.`，保留最终汇总逻辑。比较中间请求能否继续使用前轮结果，再检查最终汇总读取了什么；原任务仍包含全部数字，模型可能重新计算，因此不能预设移除中间结果后一定答错。

也可另起一轮，只把原任务中的场地费用从35改成45美元，检查总费用和预算判断是否跟随变化。两项修改分别运行，避免混淆原因。

[推理实验目录](README.md) · [推理方法与参考阅读](../README.md) · [全部练习](../../README.md#练习索引)
