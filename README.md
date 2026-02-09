# criteo-ctr-prediction
A CTR prediction project based on the Criteo dataset, including feature preprocessing, baseline models (LR/MLP), and evaluation with AUC/LogLoss.

# Criteo CTR 预测项目

本项目基于 **Criteo Display Ads Dataset**，实现点击率（CTR）预测任务，目标是构建一个**可复现、可扩展、符合工业实践的推荐 / 广告算法项目**，用于推荐算法与广告算法岗位的项目展示。

---

## 项目目标

- 搭建完整 CTR 预测流程（数据 → 特征 → 模型 → 评估）
- 从 **Logistic Regression baseline** 逐步扩展到 **深度模型（DNN）**
- 使用 CTR 场景的标准评估指标（AUC / LogLoss）
- 代码结构清晰，便于复现和扩展

---

## 项目结构

criteo-ctr-prediction/
├── data/
│ ├── raw/ # 原始数据（不提交到 Git）
│ └── processed/ # 处理后的特征数据（不提交到 Git）
├── src/
│ ├── dataset.py # 数据读取与特征预处理
│ ├── models.py # 模型定义（LR / DNN）
│ ├── train.py # 训练逻辑
│ └── eval.py # 评估与推理
├── notebooks/ # EDA / 实验记录
├── reports/ # 实验结果与总结
├── README.md
└── .gitignore

yaml
复制代码

---

## 数据集说明

- **数据集**：Criteo Display Ads Dataset
- **特征构成**：
  - 13 个连续特征（数值型）
  - 26 个离散特征（类别型）
- **标签**：是否点击（0 / 1）

> 数据集体量较大，`data/` 目录被 `.gitignore` 忽略，符合真实工业项目规范。

---

## 环境配置

```bash
python -m venv .venv
source .venv/bin/activate
pip install numpy pandas scikit-learn torch tqdm
快速运行
1. 数据预处理
bash
复制代码
python -m src.dataset \
  --input data/raw/train.txt \
  --output data/processed/train.npz
2. 模型训练
bash
复制代码
python -m src.train \
  --train data/processed/train.npz \
  --model lr \
  --epochs 3
3. 模型评估
bash
复制代码
python -m src.eval \
  --ckpt models/best.pt \
  --data data/processed/valid.npz
模型设计
Logistic Regression（CTR baseline）

Deep Neural Network（Embedding + MLP）

后续可扩展：Wide&Deep / DeepFM / DCN

评估指标
AUC：CTR 预测核心排序指标

