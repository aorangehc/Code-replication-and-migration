Code-replication-and-migration
========================================

本仓库收集了多个将论文思路迁移到 MindSpore、PyTorch 等框架的示例项目，便于快速复现关键实验。各子目录均包含可直接运行的脚本以及相应的中文说明。

目录导航
--------
- `A-Note-on-the-Inception-Score`：MindSpore 版 Inception Score 计算实现。
- `Adaptive-Weighted-Discriminator-for-Training-Generative-Adversarial-Networks`：自适应加权判别器损失（AW Loss）MindSpore 复现。
- `altclip`：AltCLIP 视觉编码器微调，包含 PyTorch 与 MindSpore 两个版本。
- `NBNet-Noise-Basis-Learning-for-Image-Denoising-with-Subspace-Projection`：NBNet 图像去噪网络的 MindSpore 实现。
- `Occupational-Biases-in-Norwegian-and-Multilingual-Language-Models`：挪威语/多语言语言模型职业性别偏差评估。

环境依赖概览
------------
- Python 3.9+
- MindSpore 2.x 与相关生态包（`mindcv`、`mindnlp` 等，具体参见子项目 README）
- PyTorch 2.x、TorchVision、Transformers（仅 `altclip` PyTorch 版本需要）
- 其它通用依赖：NumPy、SciPy、pandas、scikit-learn、tqdm 等

快速开始
--------
1. 根据目标子项目进入对应目录，阅读其中的 `README.md` 了解所需依赖与运行步骤。
2. 按照说明准备数据集或模板文件。
3. 运行示例脚本验证移植效果，必要时根据硬件环境调整设备配置（如 `device_target` 或 `cuda`）。

常见问题
--------
- 如需使用 Hugging Face 模型，脚本默认配置了镜像端点；若下载失败，可改用官方源或手动缓存模型。
- MindSpore 脚本支持 CPU/GPU/Ascend，不同设备需确保驱动与框架版本匹配。

反馈与扩展
----------
欢迎在各子项目中补充实验结果或新增迁移案例，提交 PR 时请同时更新对应的中文说明文档。
