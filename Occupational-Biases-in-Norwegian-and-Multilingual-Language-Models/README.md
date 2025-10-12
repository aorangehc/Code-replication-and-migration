
挪威语与多语言模型的职业性别偏差评估
==================================

项目简介
--------
本目录复现了论文《Occupational Biases in Norwegian and Multilingual Language Models》中针对职业描述的性别偏差测量流程。核心脚本 `codes/compute_scores.py` 会读取模板句子，调用多种预训练语言模型，统计 `[MASK]` 位置生成女性/男性指代表达的概率，并输出偏差评分。

目录结构
--------
- `codes/compute_scores.py`：主脚本，负责加载模型、计算概率与导出结果。
- `templates/`：包含两份挪威语模板（`templates_er.txt`、`templates_jobber_som.txt`），用于构造带 `[MASK]` 的职业句子。
- `gold_data/gender_equality_NSB.ods`：官方性别平等指数参考数据，可对比量化结果。

环境依赖
--------
- Python 3.9+
- MindSpore 2.x（脚本默认使用 CPU）
- MindNLP（提供 `AutoTokenizer`、`AutoModelForMaskedLM` 等接口）
- pandas

使用方法
--------
1. 选择要评估的模型，可选项包括 `norbert`、`norbert2`、`nbbert`、`mbert`、`roberta`、`nbbertLarge`、`nbroberta`。
2. 执行命令：
   ```bash
   python codes/compute_scores.py \
     --task occupations \
     --template_file templates/templates_er.txt \
     --lm_model nbbert \
     --output_file results_nbbert.csv
   ```
3. 生成的 CSV 将包含女性/男性概率、百分比以及二元偏差标记，可结合 `gold_data` 进行进一步分析。

注意事项
--------
- 脚本会将 Hugging Face 模型加载到 MindSpore 后端，如需 GPU/Ascend 推理，请修改 `ms.set_context(device_target="CPU")`。
- 模型首次下载可能耗时，请确保已配置镜像或具备网络访问权限；也可提前将模型缓存到本地。
- 模板文件采用 UTF-8 编码，编辑时请保持编码一致以避免解析问题。
