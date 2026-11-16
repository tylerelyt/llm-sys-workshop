# 检查点与停止条件

逐步生成候选结果，由模型检查后决定是否继续；用已有错误注入观察执行控制与模型判断的区别。

## 起点与运行

使用课程 Python 3.11 或 3.12 环境，从仓库根目录安装依赖，并按[模型配置](../../README-DEEPSEEK.md#setup)设置 `OPENAI_BASE_URL`、`OPENAI_MODEL`、`OPENAI_API_KEY`：

```bash
python -m pip install -r chapter7/cot_workflows/requirements.txt
python chapter7/cot_workflows/example4.py
python chapter7/cot_workflows/example4.py --inject-error
```

已有耗材任务是4张桌子各需6套，另备3套，每套2元；先复算桌面24套、总计27套、费用54元，再运行。

## 沿候选结果检查执行

[example4.py](example4.py) 的 `--inject-error` 只把第二步候选替换成26套，原任务与模型不变。检查终端中的候选、评议结果与后续执行：判定失败时是否停止，是否仍生成最终汇总？

回到 `check_result` 核对原任务、当前步骤和实际候选都进入了检查请求。`PASS` 是模型的评议文本，仍要与你的算式核对；错误候选若被放行，说明本轮检查漏检，不能修改参考答案让它通过。

`reasoning_with_checkpoints` 负责决定是否继续，模型负责给出候选与评议。分别解释这两部分的职责，再与[单次 CoT 提示](PROMPTING.md)比较调用路径。

[推理实验目录](README.md) · [推理方法与参考阅读](../README.md) · [全部练习](../../README.md#练习索引)
