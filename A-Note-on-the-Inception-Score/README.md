
MindSpore 版 Inception Score 实验说明
====================================

项目简介
--------
本示例复现了论文《A Note on the Inception Score》中对生成模型质量评估的核心指标 Inception Score（IS），并将其迁移到 MindSpore 环境。脚本 `inception_score.py` 提供了从 CIFAR-10 数据集加载数据、调用 MindCV 提供的 Inception v3 预训练模型、计算 IS 均值与标准差的完整流程。

运行环境
--------
- Python 3.9+
- MindSpore 2.x（支持 CPU/GPU/Ascend，脚本会根据上下文自动选择）
- mindcv
- numpy、scipy

数据准备
--------
默认示例基于 CIFAR-10 训练集：
1. 下载 CIFAR-10 并放置在 `./data` 目录（MindSpore Dataset 会自动下载）。
2. 数据经过 `Resize -> ToTensor -> Normalize` 的标准 ImageNet 归一化流程，确保与预训练模型兼容。

运行步骤
--------
```bash
python inception_score.py
```
- 可修改 `batch_size`、`splits` 等参数以适应不同规模的数据生成任务。
- 当 `resize=True` 时，脚本会将图像调整为 299×299，以匹配 Inception v3 默认输入尺寸。

结果解释
--------
- 输出格式为 `(IS 均值, IS 标准差)`，数值越高表示生成样本的质量越好、类别多样性越高。
- 若需比较不同生成模型，可将生成图片整理为 MindSpore 数据集，再传入 `inception_score` 函数。

常见问题
--------
- 首次运行会在本地缓存 Inception v3 预训练权重，请确保网络可访问 MindCV 模型仓库或手动下载。
- 使用 GPU/Ascend 时请提前配置好 MindSpore 对应版本与驱动。
