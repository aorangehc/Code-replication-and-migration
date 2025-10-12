
AltCLIP 视觉模型微调示例
========================

项目概览
--------
本目录包含两个针对 CIFAR-10 数据集的 AltCLIP Vision 模型微调脚本：
- `altclip_pytorch.py`：基于 PyTorch 与 Hugging Face Transformers，实现全量参数微调与分类头训练。
- `altclip_mindnlp.py`：使用 MindSpore + MindNLP，在 Ascend 设备上复现相同流程。

通用准备
--------
- Python 3.9+
- Hugging Face 模型下载通道已设置为镜像端点 `https://hf-mirror.com`，如需更换，请修改脚本开头的 `HF_ENDPOINT`。
- 默认使用 CIFAR-10 数据集，脚本会在首次运行时自动下载或期望在 `./data`（PyTorch）/`./cifar10_data_bin`（MindSpore）目录找到数据。

PyTorch 版本
------------
**依赖：**
- PyTorch 2.x、TorchVision
- transformers>=4.35
- scikit-learn、tqdm、numpy

**运行：**
```bash
python altclip_pytorch.py
```
- 训练集按照 8:2 划分为训练/验证集，默认 10 个 epoch，可修改 `train_model` 中参数。
- 训练完成后会将权重保存至 `./cifar10_altclip_model/altclip_cifar10.pth`。

MindSpore 版本
--------------
**依赖：**
- MindSpore 2.x（脚本示例设置为 `Ascend`，可根据环境改为 `GPU` 或 `CPU`）
- MindNLP >= 0.2
- scikit-learn、numpy、tqdm

**运行：**
```bash
python altclip_mindnlp.py
```
- 使用自定义 `WarmupDecayLR` 学习率调度器，并输出验证集 Loss / Accuracy / Macro-F1。
- 训练完成后生成 `altclip_mindnlp.ckpt`。

常见问题
--------
- 若下载模型或数据集超时，可手动预先缓存到本地并指定 `cache_dir`。
- Ascend 环境需确保已正确安装 MindSpore 对应版本与驱动；若仅有 GPU，可将 `context.set_context(device_target="Ascend")` 修改为 `GPU`。
