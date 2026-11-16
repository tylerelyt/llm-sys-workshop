# Token 与生成预算

运行已有的文本续写示例，观察输入怎样编码、模型怎样逐 Token 生成，以及输出预算怎样影响结束位置；本练习不需要 MaaS 凭据。

## 准备与运行

使用 Python 3.11 或 3.12，在仓库根目录安装依赖，再进入本课目录；首次运行需要下载本地权重，已有可用权重时将 `WORKSHOP_LOCAL_MODEL` 指向其路径。

```bash
python -m pip install -r chapter4/model_service/requirements.txt
cd chapter4/model_service
export WORKSHOP_LOCAL_MODEL=Qwen/Qwen2.5-0.5B-Instruct
python example1.py --max-new-tokens 8
python example1.py --max-new-tokens 32
```

模型加载由 [local_model.py](local_model.py) 负责，已有示例文本位于 [example1.py](example1.py)。模型资料与下载入口见[模型页](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct)。

## 预测、修改与解释

保持输入文本和模型不变，只改变 `--max-new-tokens`。运行前预测：预算增加后，输入 Token 会不会变化，输出是否一定用满预算？

对照终端中的输入 Token 数、前12个 ID 与片段、实际输出 Token 数和最后一个 Token。一个 Token 可以是字、词的一部分或标点；预算是上限，遇到结束标记也会提前停止。该示例不固定生成采样状态，两次文本差异不能全归因于预算。

找到源码中输入长度与生成长度相减的位置，解释 `max_new_tokens` 限制的是哪一部分，并指出模型输出何时可能被预算截断。

[Completion 与 Chat 输入](CHAT.md) · [模型基础](../README.md) · [全部练习](../../README.md#练习索引)
