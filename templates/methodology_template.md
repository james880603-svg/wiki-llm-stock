---
method_name: "{METHOD_NAME}"
category: "機器學習 / 正則化 / 截面計量 / 回測架構"
updated: "{TODAY}"
tags:
  - methodology
  - quant-finance
---

# 方法論研究：{METHOD_NAME}

> 一句話定義：{該計量或機器學習方法在資產定價與收益預測中的核心角色}

---

## 1. 數學原理與模型架構
- **模型形式**：
- **目標函數與損失函數 (Loss Function)**：{如 MSE, Huber Loss, 加權最小平方法}
- **複雜度控制與正則化 (Regularization)**：{如 L1 Lasso, L2 Ridge, Elastic Net, Dropout, Early Stopping}

## 2. 在資產定價中的優勢與局限
- **核心優勢**：{如高維度特徵篩選、非線性交互作用捕捉、對抗噪訊能力}
- **主要風險與局限**：{過擬合 (Overfitting)、黑盒子可解釋性、樣本外泛化能力}

## 3. 代表性經典文獻與實證表現
| 代表論文 | 應用情境 (資產類別/預測目標) | 主要比較基準 (Benchmark) | 實證結果結論 |
| :--- | :--- | :--- | :--- |
| [[{論文名稱}]] | {情境} | {基準} | {結論} |

---

## 4. 實作建議與超參數設定 (Practical Guidelines)
- **資料預處理**：{特徵截面排名映射到 [-1, 1]、缺失值填補}
- **驗證集切分 (Sample Splitting)**：{嚴格時間順序滾動切分，避免 Forward-Looking Bias}
