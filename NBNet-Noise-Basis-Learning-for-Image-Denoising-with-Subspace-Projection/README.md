
NBNet 图像去噪 MindSpore 实现
============================

项目简介
--------
本示例基于论文《Noise Basis Learning for Image Denoising with Subspace Projection》实现了 NBNet 结构的 MindSpore 版本。代码 `NBNet.py` 包含：
- 编码器/解码器对称结构与 Skip-Self Attention（SSA）模块；
- 噪声子空间投影的矩阵求逆与特征提取流程；
- 简单的前向推理示例，验证网络输出尺寸与残差连接效果。

环境依赖
--------
- Python 3.9+
- MindSpore 2.x（CPU/GPU/Ascend 均可）

快速验证
--------
```bash
python NBNet.py
```
脚本会：
1. 设置 MindSpore 运行于 CPU；
2. 构造随机噪声图像作为输入；
3. 前向传播并输出结果张量形状，验证网络搭建正确。

将 NBNet 集成到训练流程
------------------------
- 使用实际数据集时，可将 `NBNet` 实例化后接入 L1/L2 损失或感知损失。
- SSA 模块涉及矩阵求逆，输入尺寸较大时需关注数值稳定性，可在 MindSpore 中使用混合精度或增加正则项。
- 若在 Ascend 设备上训练，请确认 `ops.MatrixInverse` 在目标硬件上支持对应数据类型。
