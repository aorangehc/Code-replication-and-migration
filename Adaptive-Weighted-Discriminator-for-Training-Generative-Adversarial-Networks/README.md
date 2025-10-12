
自适应加权判别器损失（AW Loss）MindSpore 实现
============================================

项目简介
--------
本目录提供论文《Adaptive Weighted Discriminator for Training Generative Adversarial Networks》中提出的 AW Loss 在 MindSpore 上的复现。脚本 `aw_loss.py` 展示了如何：
- 定义自适应权重计算方法，根据判别器对真实/生成样本的预测情况动态调整梯度；
- 构建简单的判别器网络，采用随机噪声构造真实/生成样本；
- 在训练循环中获取损失并写回梯度，以便与 GAN 框架对接。

环境依赖
--------
- Python 3.9+
- MindSpore 2.x（CPU 环境即可运行示例）
- NumPy

快速体验
--------
```bash
python aw_loss.py
```
运行后将输出计算得到的 AW Loss 值，并验证梯度回写逻辑是否正常。

如何集成到 GAN
--------------
1. 将 `aw_method` 类复制到您的 GAN 项目中，确保判别器网络实现 `trainable_params()` 接口。
2. 在判别器训练阶段，调用 `aw_loss` 传入真实样本与生成样本张量，获取损失值。
3. 使用返回的损失在优化器中执行后向传播；梯度已经在方法内部按权重合成。

注意事项
--------
- 示例将 `ms.set_context(device_target="CPU")` 固定为 CPU，如需使用 GPU/Ascend，请根据硬件修改。
- 若在大模型上使用，请关注梯度范数的数值稳定性，可通过 `epsilon` 参数微调。
