# CoT 提示

在一次模型请求中加入求解提示，区分提示变化、回答形式与结果正确性。

## 运行同一个问题

使用课程 Python 3.11 或 3.12 环境，从仓库根目录安装依赖，并按[模型配置](../../README-DEEPSEEK.md#setup)设置 `OPENAI_BASE_URL`、`OPENAI_MODEL`、`OPENAI_API_KEY`：

```bash
python -m pip install -r chapter7/cot_workflows/requirements.txt
python chapter7/cot_workflows/example1.py
```

[example1.py](example1.py) 使用已有算式 `5 + 3 + 7`，在问题后追加 `Let's think step by step.`。先自行得到15，再核对实际回答；这个简单问题主要用于观察提示，不能代表复杂推理表现。

## 只改变提示

固定问题、模型与接口，在副本中移除追加的求解提示，重新运行。对照两份实际提示、最终答案及回答形式，说明哪些内容由提示引导，哪些仍需要独立计算核对；可见的解释不是内部推理过程的完整记录。

程序每次发送一条用户消息，没有跨轮状态。需要研究多次请求如何使用中间结果，进入[多轮上下文传递](CONTEXT.md)。

[推理实验目录](README.md) · [推理方法与参考阅读](../README.md) · [全部练习](../../README.md#练习索引)
