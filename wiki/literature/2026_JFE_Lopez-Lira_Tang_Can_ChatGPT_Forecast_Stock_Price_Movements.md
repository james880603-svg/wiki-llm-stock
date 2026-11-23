---
title: "Can ChatGPT forecast stock price movements? Return predictability and large language models"
authors:
  - "Alejandro Lopez-Lira"
  - "Yuehua Tang"
institution: "Journal of Financial Economics (JFE) / University of Florida"
year: 2026
sample_period: "2021.10-2024.05 (嚴格樣外，避開GPT知識截止日)"
market: "美股"
asset_universe: "NYSE, NASDAQ, AMEX 4,123 檔上市普通股 (15.9萬則新聞頭條)"
methodology: "大語言模型零樣本提示 (Zero-Shot Prompting) / 多空對沖漂移策略 / 文字主題模型 (BERTopic) / 資訊處理摩擦理論模型"
performance_highlight: "隔夜新聞即時反應準確率 93.3%；隔日漂移多空年化夏普值 2.97 (日均報酬 34 bps)；2021Q4-2024 策略 Alpha 隨 AI 普及遞減 (夏普 6.54 降至 1.22)"
key_conclusion: "顯著有效：大語言模型 (GPT-4) 具備未經金融微調即可湧現之經濟推理能力；市場對複雜新聞（如內部人交易）存在顯著反應不足 (Underreaction)，且負面新聞與小型股漂移最顯著"
updated: "2026-11-23"
tags:
  - literature
  - large-language-models
  - chatgpt
  - textual-analysis
  - market-efficiency
  - behavioral-finance
---

# [2026] Lopez-Lira and Tang - Can ChatGPT forecast stock price movements? Return predictability and large language models

> **一句話核心結論**：  
> 本文是**生成式 AI 與大型語言模型（LLM）進入頂級金融期刊（JFE）的里程碑之作**；證明未經任何金融數據監督訓練的通用大型語言模型（GPT-4），具備極高的即時經濟推理能力（**預測隔夜新聞即時反應準確率達 93.3%**），且因市場對複雜新聞存在資訊處理瓶頸與套利限制，**事後漂移多空策略創造了高達 2.97 的年化夏普值**；同時實證記錄了隨 LLM 廣泛普及，市場定價效率提升、該超額收益逐年衰減的動態演進。

---

## 1. 研究問題與核心論點 (Research Question)
- **探討主題**：通用大語言模型（如 ChatGPT / GPT-4）能否在完全沒有看過標籤回測資料（Zero-shot）的情況下，正確解讀財經新聞並預測股價反應？
- **實證金融學核心叩問**：
  1. **金融推理是湧現能力嗎？** 語言模型只訓練「預測下一個字詞」，它真的懂新聞背後的商業意涵與市場定價邏輯嗎？
  2. **市場是否完全有效反映新聞？** 如果 GPT-4 能準確理解新聞，市場是否會出現「反應不足（Underreaction）」與「後續價格漂移（Drift）」？
  3. **AI 的普及如何改變市場效率？** 當越來越多投資人開始使用 LLM 解析資訊，市場是否變得更有效率（Alpha 衰退）？

---

## 2. 樣本資料與實證設計 (Data & Methodology)

### 2.1 樣本資料與避免未來資訊偏誤 (Strict OOS)
- **樣本時間**：2021 年 10 月至 2024 年 5 月。
  - **關鍵設計**：GPT-4 基礎模型的知識截止日為 **2021 年 9 月**，因此本研究測試的所有新聞完全落在訓練截止日之後，徹底杜絕了前瞻偏誤（Look-ahead Bias）與記憶效應（Memorization）。
- **涵蓋標的**：CRSP 4,123 檔美股普通股（約佔市場 85%）。
- **新聞資料庫**：RavenPack 篩選之重大通訊社與財經媒體新聞頭條，共 159,137 則（67.5% 為企業發布的新聞稿，32.5% 為記者撰寫的新聞報導；82% 為非交易時段的隔夜新聞，18% 為盤中新聞）。

### 2.2 提示詞工程與評分機制 (Prompt Design)
研究直接採用通用 API 進行對話式提示（設定 `temperature = 0` 確保可重複性）：
```text
Forget all your previous instructions. Pretend you are a financial expert. 
You are a financial expert with stock recommendation experience.
Answer "YES" if good news, "NO" if bad news, or "UNKNOWN" if uncertain in the first line. 
Then elaborate with one short and concise sentence on the next line. 
Is this headline good or bad for the stock price of _company_name_ in the short term?
Headline: _headline_
```
- **GPT 分數映射**：YES 映射為 `+1`，UNKNOWN 為 `0`，NO 映射為 `-1`。

### 2.3 橫向比對的模型家族 (12 款 LLM + 3 款基準)
- **早期與基礎模型**：GPT-1, GPT-2, BERT, BERT-Large, BART-Large, Llama2-7B, Llama2-13B。
- **進階與旗艦模型**：DistilBART-MNLI, GPT-3.5, Llama2-70B, GPT-4。
- **領域專用與傳統基準**：FinBERT、RavenPack 專業情緒分數、Loughran-McDonald (2011) 財經字典、Tetlock (2008) Harvard-IV 心理學字典。
- **監督式文本嵌入 (Embeddings)**：OpenAI text-embedding-ada-002 (1536維) 與 MiniLM (384維) 搭配滾動 6 個月邏輯回歸。

---

## 3. 關鍵實證成果 (Empirical Findings)

### 3.1 即時反應 vs 事後漂移 (Initial Reaction vs. Post-Announcement Drift)
| 預測維度 | 隔夜新聞即時開盤反應 (Init) | 隔日開盤至收盤漂移 (Drift) | 盤中新聞即時 (15分) | 盤中後續漂移 (至次日收盤) |
| :--- | :--- | :--- | :--- | :--- |
| **日組合勝率 (Hit Rate)** | **93.28%** | **58.06%** | **88.78%** | **54.67%** |
| **多空日均報酬 (Mean Ret)** | **3.06%** (不可直接交易) | **0.34% (34 bps)** | **4.44%** | **0.50% (50 bps)** |
| **年化夏普值 (Sharpe Ratio)** | — | **2.97** | — | **2.63** |
| **做多腳 (Good News)** | 1.27% (勝率 83.3%) | 0.08% (SR = 0.78) | 1.33% | 0.19% (SR = 1.37) |
| **放空腳 (Bad News)** | -1.79% (勝率 79.4%) | **0.26% (SR = 2.01)** | -3.11% | **0.31% (SR = 1.71)** |

> **核心實證定論**：  
> 1. **超強即時解讀力**：GPT-4 預測市場對隔夜新聞初始開盤方向的勝率高達 **93.3%**，證明其精準掌握市場共識。  
> 2. **事後可交易漂移**：在新聞開盤後才進場、持有至收盤，每天仍能穩定賺取 **34 bps** 的價格延遲反映利潤，多空策略未計成本累積報酬達 **700%**。

---

### 3.2 跨模型能力評比：金融推理是「規模湧現能力 (Emergent Ability)」

| 模型級別 | 代表模型 | 初始反應勝率 (HR-I) | 漂移勝率 (HR-D) | 漂移多空年化夏普值 (Sharpe) | 結論與評價 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **頂級旗艦** | **GPT-4** | **93.3%** | **58.1%** | **2.97** | 全面碾壓所有模型，深層語意理解 |
| **進階大模型** | **GPT-3.5** | 93.0% | 56.0% | 1.66 | 即時判斷精準，但事後漂移捕捉弱於 GPT-4 |
| | **DistilBART-MNLI** | 87.0% | 56.0% | 1.26 | 輕量化推論模型，具備一定判別力 |
| | **Llama2-70B** | 86.0% | 53.0% | 0.97 | 開源大模型龍頭，遠優於小參數版 |
| **金融專用小模型** | **FinBERT (110M)** | 90.0% | 48.0% | **-0.33** | 雖能辨識基本正負向，但 75% 標註為中性，漂移預測失敗 |
| **傳統小模型** | **GPT-1 / GPT-2 / BERT** | 52% ~ 64% | 46% ~ 53% | **全部為負值 (-0.11 ~ -0.64)** | 完全缺乏金融經濟推理能力，經常給出相反預測 |
| **傳統基準** | **RavenPack (專業數據)** | 88.0% | 60.0% | 2.50 | 表現優異，但被 GPT-4 納入回歸後失去統計顯著性 |
| | **Loughran-McDonald 字典** | 76.0% | 51.0% | -0.19 | 傳統計詞字典在複雜新聞情境下徹底失效 |

---

### 3.3 市場反應不足 (Underreaction) 的微觀結構機制

為什麼即使新聞已經公開，股價還會持續漂移 1~2 天？論文透過主題模型 (BERTopic) 與截面回歸揭示了市場資訊處理的深層瓶頸：

1. **新聞主題的異質性 (Topic Heterogeneity)**：
   - **市場高效率反映（無漂移）**：透明、格式化、易量化的事件（例如：**財報公布 Earnings Reports**、**策略結盟 Strategic Partnerships**、**新藥臨床試驗結果 Clinical Trials**）。市場在開盤時瞬間定價完畢，GPT 初始對齊度極高（308~337 bps），後續漂移接近 0。
   - **市場顯著反應不足（強烈漂移）**：需要複雜背景綜合推理的事件（例如：**內部人股權交易 Insider Stock Transactions** 漂移 +26.3 bps***、**股利政策變更 Dividend Announcements** 漂移 +22.3 bps***、**醫療研討會專業演講 Conference Presentations** 漂移 +34.2 bps*）。一般市場參與者無法第一時間解析其深層影響，導致價格緩慢調整。
2. **負面新聞漂移遠大於正面新聞 (Asymmetry & Short-Sale Constraints)**：
   - 放空端 (Short leg) 的年化夏普值 (2.01) 是做多端 (0.78) 的近 3 倍！
   - 理論機制：放空存在融券限制、借券成本與制度約束，使得知情套利者修正「被高估資產」的速度遠慢於修正「被低估資產」。
3. **小型股漂移顯著高於大型股 (Firm Size Friction)**：
   - 大型股在開盤後幾乎無漂移（市場極度高效）；小型股與非流動性標的漂移持續 2 天（交互項 $t=4.55$）。小型股受關注度低、專業分析師覆蓋少，資訊擴散嚴重滯後。

---

### 3.4 交易成本耐受度與換手率調優 (Transaction Costs)
- **手續費侵蝕**：純 100% 每日換手策略日周轉率高達 190%；
  - 單邊 5 bps（來回 10 bps）時，策略累積回報仍超過 100%，年化夏普值約 1.29。
  - 單邊 10 bps（來回 20 bps）時，Alpha 被交易成本吞噬殆盡。
- **部分再平衡改善 (Partial Rebalancing, 25%)**：
  - 將每日再平衡比例降至 25%，換手率大幅降至每日 46%，在來回 10 bps 成本下，夏普值反而逆勢維持在 **1.34**（優於 100% 再平衡）。

---

### 3.5 AI 普及與市場效率演進（Alpha 的自我消亡）
研究追蹤了 2021Q4 到 2024 年策略夏普值的逐年變化：
- **2021 年 Q4**：年化夏普值高達 **6.54**
- **2022 年**：年化夏普值降至 **3.68**
- **2023 年**：年化夏普值降至 **2.33**
- **2024 年 (1~5月)**：年化夏普值降至 **1.22**

> **理論意涵 (Proposition B.4)**：大語言模型的低門檻對話介面降低了普通投資人處理複雜文本的成本。隨著避險基金與機構全面導入 Generative AI，原本存在反應不足的資訊被越來越快速地定價，**LLM 的預測成功孕育了自身交易信號的消亡（Seeds of its own obsolescence）**。

---

## 4. 本文對 Wiki 知識庫的更新連動 (Compounding Links)
- 關聯方法論：
  - [[大語言模型與金融文字分析]]（Zero-shot 提示 vs 監督式 Embeddings）
  - [[機器學習資產定價]]（非線性模型擴展至非結構化文字維度）
- 關聯行為與異象：
  - [[市場反應不足與漂移現象]]（盈餘後漂移 PEAD、新聞後漂移、套利限制）
  - [[散戶交易虧損與法人超額收益]]（散戶資訊處理能力受限與 AI 賦能）
