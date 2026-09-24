---
layout: paper
title: "VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model"
section: vla
page_id: "1945538827"
permalink: /zh/vla/vla-adapter-an-effective-paradigm-for-tiny-scale-vision-language-action-model-1945538827/
---

**Paper** : [VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model](https://arxiv.org/abs/2509.09372)  
**Source** : arXiv, Accepted by AAAI 2026 (Oral)  
**arXiv ID** : 2509.09372

### Abstract

Vision-Language-Action (VLA) 模型通常透過在機器人資料上預訓練大型視覺語言模型（VLM），來銜接感知空間與動作空間之間的落差；這種做法雖然大幅提升表現，但也帶來顯著的訓練成本。本文探討如何有效地將「視覺-語言（VL）表示」橋接到「動作（A）」，提出 VLA-Adapter 這一新範式，旨在降低 VLA 模型對大規模 VLM 與大量預訓練的依賴。作者首先系統性分析了各種 VL 條件（condition）的有效性，找出哪些條件對橋接感知與動作空間是關鍵的；基於這些發現，提出一個輕量級的 Policy 模組，搭配 Bridge Attention 機制，自動將最佳條件注入動作空間。透過這種方式，此方法僅用 0.5B 參數的骨幹、且無需任何機器人資料預訓練，就能達到高效能。在模擬與真實機器人基準上的大量實驗顯示，VLA-Adapter 不僅達到最先進水準的效能，還提供目前已知最快的推理速度，並能在單張消費級 GPU 上僅用 8 小時就訓練出一個強力的 VLA 模型。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945538827_vlaadapter_fig1.png) 

_Figure 2: 既有代表性 VL 到 A 的橋接範式（bridge paradigms）比較，說明過去方法如何連接視覺語言模型輸出與動作生成。_

![Figure]({{ site.baseurl }}/assets/images/1945538827_vlaadapter_fig2.png) 

_Figure 3: VLA-Adapter 提出的整體框架，關鍵元件包含條件探索（condition exploration）與 Bridge Attention 設計。_

  * **要解決的問題** ：既有 VLA 模型仰賴在大規模機器人資料上預訓練大型 VLM 才能達到好效果,但這帶來龐大的訓練成本與硬體門檻,如何在不做機器人資料預訓練、且用極小骨幹（tiny-scale）的情況下仍達到高效能，是本文要解決的核心問題。
  * **Main method** ：VLA-Adapter 先系統性分析各種「VL 條件」（即從 VLM 中萃取哪些中間表示，如不同層的特徵）對於橋接感知與動作空間的有效性，找出關鍵的必要條件；再基於此設計一個輕量級 Policy 模組，透過「Bridge Attention」機制自動挑選並注入最適合的 VL 條件到動作生成過程中。
  * **和以往方式的差異** ：多數既有 VLA 模型（如 OpenVLA 等）依賴大型 VLM（數十億參數）並在大規模機器人資料上做預訓練才能有效銜接感知與動作；VLA-Adapter 反其道而行，僅用 0.5B 參數的小型骨幹（基於 Qwen2.5-0.5B），完全跳過機器人資料預訓練階段，改用精心設計的「條件橋接」機制彌補模型規模與預訓練資料的不足。
  * **架構/流程描述** ：模型以 Prismatic-VLMs 架構為基礎，LLM 骨幹為 Qwen2.5-0.5B；訓練前先分析 VLM 各層/各類型表示（VL conditions）對動作預測的貢獻度，篩選出關鍵條件後，透過 Bridge Attention 將這些條件動態注入到一個輕量 Policy 模組中，該模組負責將橋接後的表示轉換為機器人動作輸出，整個流程強調輕量化與訓練效率（單卡消費級 GPU、8 小時即可完成訓練）。



### Result

  * 根據搜尋結果摘要（WebSearch，非直接讀取 arXiv 全文），VLA-Adapter 相較既有 SOTA 方法達成約 14 倍模型規模縮減、38 倍微調加速、3 倍推理吞吐量提升,並在模擬與真實機器人基準上達到 SOTA 級效能與目前已知最快的推理速度。
  * 由於此段數據來自 WebSearch 摘要而非直接讀取論文全文或摘要原文,需要查證全文以確認上述倍數的具體計算基準與比較對象是否公正。
  * arXiv 摘要原文本身僅以「state-of-the-art level performance」及「fastest inference speed reported to date」等定性描述，未包含具體數字，量化結果需要查證全文。



### Limitation

  * 論文本身（摘要層級）未明確自陳限制。
  * 從方法設計看，僅用 0.5B 參數骨幹且跳過機器人資料預訓練，雖然效率高，但在面對高度分佈外（out-of-distribution）或極複雜的長時程任務時，是否仍能與大型預訓練 VLA（如 7B 等級模型）匹敵，需要查證全文的更廣泛基準比較（尤其是與大模型在困難任務上的差距）。
  * 論文與 VLA-AD（Offline Semantic Guidance，本清單論文7）在「降低模型規模同時維持效能」這一目標上方向相似，但採取的方法路徑不同（VLA-Adapter 靠條件橋接注意力機制,VLA-AD 靠語意蒸餾），兩者在真實場景的優劣需要進一步查證比較。



### Related work

  * 此論文已在 GitHub（OpenHelix-Team/VLA-Adapter）與 HuggingFace 有完整開源實作與後續優化版本（Pro version），顯示社群關注度較高。
  * 根據 WebSearch 結果，相關/同期工作包括 StableVLA（arXiv:2605.18287，關於無需額外資料的穩健 VLA 模型），值得一併查閱比較。
  * Related work 值得 survey 的程度：高。此文獲 AAAI 2026 Oral 認可，且在效率／輕量化 VLA 議題上具有指標性地位，與 VLA-AD、EcoVLA、VLA-Perf 等同樣關注效率議題的論文放在一起 survey，能建立起「VLA 輕量化/高效部署」這條技術脈絡的全貌。



### Conclusion

  * 本文提出的「輕量 Policy + Bridge Attention」思路針對 VLA 訓練成本與部署門檻這一實務痛點提出有效解法，並獲 AAAI 2026 Oral 肯定，具高度參考價值，尤其適合資源受限（如中小型團隊、單卡消費級 GPU）場景參考。
  * 與其他重要文章的關係：本文與 VLA-AD（蒸餾路線）、EcoVLA（裝置-邊緣協同推理路線）同屬「讓 VLA 更輕量、更快、更省資源」這一大方向下的不同技術路線，三者可放在一起比較，理解「模型端輕量化設計」vs「訓練後蒸餾」vs「系統級部署優化」三種互補思路。
  * 對 ROCm/AMD 的關聯：此文強調「單張消費級 GPU、8 小時訓練完成」，若 ROCm 生態能支援 Qwen2.5-0.5B 骨幹與 Prismatic-VLMs 架構的訓練/推理（PyTorch ROCm 版本理論上可行），此方法的低硬體門檻特性對於 AMD GPU 平台上複現/驗證 VLA 訓練具有一定吸引力，但摘要與搜尋結果均未提及作者是否曾在 ROCm/AMD 硬體上測試，仍需要查證全文與官方程式碼庫（GitHub）的硬體相容性說明。