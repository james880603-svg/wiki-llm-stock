---
title: "{TITLE}"
authors:
  - "{AUTHOR_1}"
institution: "{INSTITUTION_OR_JOURNAL}" # 學校 / 期刊 (例如：台大財金、政大企管、RFS, JF)
year: {YEAR}
sample_period: "{START_YEAR}-{END_YEAR}"
market: "台股" # 台股 / 美股 / 跨市場
asset_universe: "上市櫃全市場" # 上市櫃全市場 / 台灣50 / 大型股 / 中小型股
methodology: "截面回歸" # Panel 回測 / 截面 Fama-MacBeth / 機器學習 (Tree, NN) / 事件研究法
performance_highlight: "年化夏普值 X.XX / 樣外 R² X.XX%"
key_conclusion: "有效" # 顯著有效 / 週期性有效 / 需搭配濾網 / 完全失效
updated: "{TODAY}"
tags:
  - literature
  - empirical-finance
---

# [{YEAR}] {AUTHORS} - {TITLE}

> 一句話核心結論：{用一句話總結該論文最重要的實證發現或理論貢獻}

---

## 1. 研究問題與核心論點 (Research Question)
- **探討主題**：{例如技術指標在台股之有效性、多因子模型在大型股的表現}
- **核心假說**：{例如技術指標能否在扣除交易成本後產生穩健超額報酬}

## 2. 樣本資料與實證設計 (Data & Methodology)
- **資料來源與樣本期間**：{例如 TEJ / CRSP，期間 YYYY~YYYY}
- **研究標的池 (Universe)**：{例如 台灣加權指數、台灣50成分股、全市場普通股}
- **資料頻率**：{日 / 週 / 月}
- **使用模型與特徵 (Predictors / Factors)**：
  - 輸入變數：{列出使用的指標、因子或宏觀變數}
  - 模型方法：{OLS, 因子排序, 機器學習模型, 正則化方法}
- **樣外驗證設計 (Validation / OOS Design)**：{例如 Rolling window, 訓練集/驗證集/測試集分割}

## 3. 關鍵實證成果 (Empirical Findings & Metrics)
### 📊 統計預測力與衡量指標
- **樣外預測力 (Out-of-Sample R² / MSE)**：
- **統計顯著性 (t-stat / p-value / Diebold-Mariano 檢定)**：

### 💰 投資組合與經濟效益 (Economic Gains)
- **策略型態**：{多空對沖 (Long-Short Decile) / 做多擇時 (Long-Only Timing)}
- **年化報酬率 (Annualized Return)**：
- **年化夏普值 (Sharpe Ratio)**：
- **最大回撤 (Max Drawdown)**：
- **風險調整後超額報酬 (Alpha)**：{相對於 CAPM / Fama-French 3/5 因子模型的 Alpha}

### 🏆 最具預測力的特徵/指標排行 (Feature Importance)
1. 
2. 
3. 

## 4. 關鍵洞察與文獻對話 (Insights & Novelty)
- **非線性與交互作用**：{是否存在非線性特徵？例如高波動下動能失效？}
- **市場有效性意涵**：{支持弱式效率市場、行為偏差、還是市場摩擦（如流動性限制）？}
- **文獻分歧**：{本文結論與哪些過去研究矛盾或一致？}

---

## 5. 本文對 Wiki 知識庫的更新連動 (Compounding Links)
- 關聯指標：[[{技術指標}]]
- 關聯因子：[[{因子名稱}]]
- 關聯行為/異象：[[{行為財務或異象}]]
- 關聯方法：[[{實證方法}]]
