---
layout: paper
title: "iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework"
section: wm
page_id: "1945539121"
permalink: /wm/iworld-bench-a-benchmark-for-interactive-world-models-with-a-unified-action-gene-1945539121/
---

**Paper** : [iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework](https://arxiv.org/abs/2605.03941)  
**Source** : arXiv (cs.CV, cs.AI)，Accepted at ICML 2026  
**arXiv ID** : 2605.03941

### Abstract

達成通用人工智慧 (AGI) 需要能夠自適應學習與互動的智能體，而互動式世界模型 (interactive world models) 提供了可擴展的感知、推理、行動環境。然而目前研究仍缺乏大規模資料集與統一基準來評測其物理互動能力。本文提出 iWorld-Bench，一個用於訓練與測試世界模型在「距離感知」與「記憶」等互動相關能力上表現的綜合基準。作者建構了包含 33 萬個影片片段的多樣化資料集，並挑選出 2,100 個涵蓋不同視角、天氣、場景的高品質樣本。由於現有世界模型的互動模式（action modality）各不相同，作者提出一個「動作生成框架 (Action Generation Framework)」以統一評測標準，設計六種任務類型，共產生 4,900 個測試樣本，聯合評估模型在視覺生成、軌跡跟隨、記憶三方面的表現。作者評測了 14 個具代表性的世界模型，發現了關鍵限制並為未來研究提供洞見。排行榜公開於 iWorld-Bench.com。

### Method

![Figure](/assets/images/1945539121_iworldbench_fig1.png) 

_Figure 1: iWorld-Bench 總覽，涵蓋 UGV/UAV/人類/機器人四種視角，結合統一的 Action Generation Framework 評測互動式世界模型。_

![Figure](/assets/images/1945539121_iworldbench_fig2.png) 

_Figure 2: 資料處理流程與總覽，包含資料收集、統一化、VLM 輔助標註、人工驗證四步驟。_

  * **要解決的問題** ：不同世界模型的互動輸入模式（動作條件的形式，例如文字指令、軌跡座標、鍵盤按鍵等）彼此不統一，導致難以用同一套基準做公平比較；同時業界缺乏大規模、涵蓋多元場景（不同視角/天氣/場景）的互動能力評測資料。
  * **Main method** ：
    * 建構 330k 影片片段資料集，篩選出 2.1k 高品質樣本，涵蓋多視角、天氣、場景變化。
    * 提出「Action Generation Framework」把不同世界模型各自的動作輸入形式，轉換/統一成可比較的評測介面。
    * 基於此框架設計 6 種任務類型（涵蓋視覺生成品質、軌跡跟隨準確度、長期記憶維持能力），共生成 4.9k 測試樣本。
    * 對 14 個代表性世界模型進行評測。
  * **與以往方式的差異** ：以往針對世界模型的評測往往綁定特定模型的動作介面，難以跨模型比較；iWorld-Bench 透過統一動作生成框架，讓不同動作模態的模型可以在同一套任務下被公平評測，並額外強調「距離感知」與「記憶」這兩個過去較少被系統性測試的互動能力面向。
  * **重要設計描述** ：整體流程為資料收集（330k clips）→ 品質篩選（2.1k samples，涵蓋視角/天氣/場景多樣性）→ 透過 Action Generation Framework 產生統一格式的動作條件輸入 → 依六種任務類型批次生成 4.9k 測試樣本 → 送入 14 個世界模型做視覺生成、軌跡跟隨、記憶三面向評分 → 建立排行榜。



### Result

  * 評測 14 個具代表性世界模型後，找出了「關鍵限制」（key limitations），但摘要未列出具體數值分數，需要查證全文或 iWorld-Bench.com 排行榜取得詳細比較數據。
  * 是否公正：由於此論文已被 ICML 2026 接受，經過同儕審查，方法論相對可信；但摘要未透露評測時是否對所有模型使用相同運算資源/取樣設定，需要查證全文以確認公平性。
  * 需要查證其他論文（例如 WorldOlympiad）在重疊模型上的評測結果是否與此一致，摘要未提供足夠資訊直接比對。



### Limitation

  * 摘要提及「識別出關鍵限制」，但未具體展開是哪些限制，需要查證全文的實驗分析章節。
  * 從方法設計推測，潛在弱項可能包括：Action Generation Framework 在轉換不同動作模態時可能引入近似誤差，統一化過程本身可能對某些原生動作模態的模型不利或有利；2.1k 高品質樣本規模仍相對有限，可能無法完全代表真實世界互動多樣性。



### Related work

  * 同期的 WorldOlympiad (arXiv:2606.11129) 也是世界模型基準論文，但著重物理/幾何/互動三軌評測，與 iWorld-Bench 的距離感知/記憶/統一動作框架形成互補視角，值得對照閱讀。
  * 暫無發現明確的更新後續研究（例如針對 iWorld-Bench 做二次分析或擴展的論文）。
  * 值得 survey 的程度：中高，尤其對於需要選擇評測工具的研究者，此篇的統一動作框架設計思路具有實用參考價值。



### Conclusion

  * 整體評價：這是一篇已被 ICML 2026 接受、方法論嚴謹的世界模型基準論文，其「統一動作生成框架」解決了跨模型比較的實際痛點，對於希望公平比較不同互動式世界模型的研究者有參考價值。
  * 與其他重要文章的關係：與 WorldOlympiad 同屬 2026 年出現的世界模型評測基準浪潮，兩者互補（前者聚焦距離感知/記憶/統一動作介面，後者聚焦物理/幾何一致性）；也可能被後續 VLA / world-model-as-simulator 類論文（如 WoVR、Interactive World Simulator）引用作為評測手段。
  * ROCm/AMD 待補強部分：論文本身聚焦於評測基準設計，不涉及底層硬體或訓練框架，看不出與 ROCm 的直接關聯；若 AMD 要驗證自家硬體上訓練/推論的世界模型的互動能力，此基準可作為現成評測工具參考。