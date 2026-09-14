---
layout: paper
title: "DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models"
section: vla
page_id: "1945473584"
permalink: /vla/deepthinkvla-enhancing-reasoning-capability-of-vision-language-action-models-1945473584/
---

**Paper** : [DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models](https://arxiv.org/abs/2511.15669)  
**Source** : arXiv (conference paper,26 pages)  
**arXiv ID** : 2511.15669

### Abstract

本文探討 Chain-of-Thought (CoT) 推理是否真的能提升 Vision-Language-Action (VLA) 模型的表現，還是只是增加額外開銷。作者透過系統性實驗發現，CoT 要對 VLA 有效，必須同時滿足兩個條件：(1) Decoding Alignment（解碼對齊）—— CoT 與動作必須用符合各自模態特性的機制生成，若強迫用單一自回歸解碼器同時生成兩者，反而會傷害效能；(2) Causal Alignment（因果對齊）—— CoT 必須透過以任務成功為導向的優化，與任務結果建立因果連結,否則單純的監督式 CoT 在動作執行敏感的動態偏移下,效果和完全不推理幾乎一樣差。基於這兩個發現，作者提出 DeepThinkVLA,在 LIBERO、LIBERO-Plus、RoboTwin 2.0 等模擬基準上取得顯著提升,並有初步真實機器人實驗佐證。

### Method

![Figure](/assets/images/1945473584_deepthinkvla_fig2.png) 

_Figure 1：VLA 架構比較。DeepThinkVLA 提出一種混合設計，將自回歸式(autoregressive) Chain-of-Thought 推理與並行動作解碼(parallel action decoding)相結合，兼顧推理能力與推論效率。_

![Figure](/assets/images/1945473584_deepthinkvla_fig1.png) 

_Figure 2：具身 CoT 資料集建構的兩階段流程。第一階段透過夾爪狀態變化擷取關鍵幀並查詢雲端大型視覺語言模型(LVLM)；第二階段則在本地 VLM 上進行微調，以生成高品質的具身推理鏈標註。_

  * **要解決的問題** ：既有 CoT-VLA 方法報告的收益有限且不穩定，沒有工作嚴謹診斷過 CoT 何時、為何能幫助機器人動作決策。
  * **Main method** ：DeepThinkVLA 採用「hybrid-attention decoder」（混合注意力解碼器）：語言（CoT）部分用因果注意力（causal attention）逐token生成，動作部分則用雙向注意力（bidirectional attention）平行解碼，藉此同時滿足模態各自的生成需求（解決 Decoding Alignment 問題）。訓練上採用兩階段 SFT（監督式微調）接著 RL（強化學習）的流程，用稀疏的任務成功獎勵，把完整的「推理鏈到動作」的因果關係對齊起來（解決 Causal Alignment 問題）。
  * **和以往方式的差異** ：以往 CoT-VLA 多半用單一自回歸解碼器同時生成文字推理與動作 token，且僅靠監督式學習訓練 CoT，未必與任務結果因果掛鉤；DeepThinkVLA 明確拆分解碼機制並引入結果導向的 RL 優化。
  * **架構/流程描述** ：輸入視覺與語言指令後，模型先以因果注意力自回歸產生一段文字化推理（CoT），再以雙向注意力一次性（平行）產生一組動作 token 序列；訓練分兩階段，先用人類/教師示範的 CoT+動作做 SFT，再用 RL 以任務成功與否作為稀疏獎勵微調整條推理-動作鏈。



### Result

  * DeepThinkVLA 在 LIBERO 達到 97.0% 成功率，在 LIBERO-Plus（機器人穩健性測試）達到 79.0%（相較 π0-FAST 的 61.6%），在 RoboTwin 2.0 達到 59.3% 成功率，超越最強基準 21.7 個百分點。
  * 消融實驗顯示：若把 CoT 與動作硬塞進同一個自回歸解碼器，效能會下降 4.2 個百分點；若沒有因果對齊（純監督式 CoT），在動態偏移情境下效能會下降 32.0 個百分點，幾乎等同於完全不用推理的基線（下降 31.6 個百分點）。
  * 論文也做了初步真實機器人實驗，證明其 CoT 資料建構與混合式架構具備物理可行性,但真實機器人的量化結果篇幅有限。
  * 是否公正：摘要中的比較基準（π0-FAST 等）為作者自行複現/引用的既有工作,需要查證其他論文的比較數據是否有出入。



### Limitation

  * 論文自陳的限制：真實機器人實驗僅為「初步證據」（preliminary evidence），規模與多樣性可能有限。
  * 從結果看，此方法高度依賴任務成功訊號作為 RL 獎勵，在獎勵稀疏、任務成功難以自動判定的真實場景下，訓練穩定性與可擴展性需要進一步查證全文才能確認。
  * 摘要未明確提及模型規模、訓練資料量與計算成本，對於部署與硬體需求（如是否能在 ROCm/AMD GPU 上高效訓練 RL 階段）需要查證全文。



### Related work

  * 論文提及與之比較的基準包含 π0-FAST 等既有 CoT-VLA / VLA 方法，但摘要未列出更完整的相關研究清單。
  * 暫無發現明確更新的後續研究（截至目前檢索範圍）。
  * Related work 值得 survey 的程度：中等偏高，因為此文對「CoT 何時有效」提出可驗證的診斷框架，後續 VLA 推理類論文（如 LaRA-VLA）很可能會引用或對比此文的兩個對齊條件。



### Conclusion

  * 本文提出的兩個必要條件（Decoding Alignment、Causal Alignment）具有一定的診斷/方法論價值，並非單純堆疊架構技巧，對理解「CoT 在 VLA 中何時有效」很有參考價值，值得精讀。
  * 與其他重要文章的關係：直接對話並挑戰既有 CoT-VLA 系統（如摘要中提及的 π0-FAST），並可能與 LaRA-VLA（本清單論文3，同樣談 CoT 但改用潛在推理以降低延遲）互補或形成對照——DeepThinkVLA 走「顯式 CoT + RL 對齊」路線,LaRA-VLA 走「潛在推理」路線，兩者對於推理是否要「顯式化」給出不同答案。
  * 對 ROCm/AMD 的關聯：摘要未提及具體訓練/推理硬體（大概率為 NVIDIA GPU 生態），此文的 RL 微調與混合注意力解碼器在 ROCm 上的相容性與效能未知，看不出明確關聯，需要查證全文的實作細節（是否用 vLLM、FlashAttention 等對 ROCm 支援程度不一的套件）。