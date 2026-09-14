---
layout: paper
title: "EventVLA: Event-Driven Visual Evidence Memory for Long-Horizon Vision-Language-Action Policies"
section: vla
page_id: "1945538699"
permalink: /Physical-AI-Papers-Survey/vla/eventvla-event-driven-visual-evidence-memory-for-long-horizon-vision-language-ac-1945538699/
---

**Paper** : [EventVLA: Event-Driven Visual Evidence Memory for Long-Horizon Vision-Language-Action Policies](https://arxiv.org/abs/2606.20092)  
**Source** : arXiv (cs.CV)  
**arXiv ID** : 2606.20092

### Abstract

本文指出記憶仍是長時程機器人操作的關鍵瓶頸，標準 VLA 策略在任務相關線索隨時間被遮擋或不可觀測時常常失效。既有記憶增強方法雖利用歷史脈絡，但要嘛存在嚴重的資訊瓶頸、要嘛因採用解耦雙系統而延遲過高、要嘛仰賴不加篩選的緩衝區而累積大量視覺冗餘。為解決這些限制，作者提出 EventVLA，一個基於「稀疏視覺證據記憶」概念的端到端框架，包含兩個核心元件：用於保留初始與短期脈絡的基礎視覺錨點（visual anchors），以及動態的關鍵幀證據記憶模組（Keyframe Evidence Memory, KEM）。KEM 直接從 VLA 的潛在嵌入預測未來關鍵幀機率，自主捕捉並儲存稀疏、任務關鍵的視覺事件；此「前瞻驅動」機制讓策略能動態評估當前觀測對未來的因果效用，在視覺證據變得不可觀測前先行保存。此外作者提出 RoboTwin-MeM，一個專門用於評估具互動視覺證據的非馬可夫操作任務的診斷型基準。在 17 個需要記憶的模擬任務與 4 個真實世界雙臂任務上的廣泛評測顯示，EventVLA 相較於最先進的記憶增強 VLA 平均成功率提升 +40%。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945538699_eventvla_fig1.png) 

_Figure 1：EventVLA 總覽。EventVLA 透過儲存稀疏且任務關鍵的視覺證據(visual evidence)來處理需要長時程記憶的操作任務，圖中說明其核心設計理念與整體資料流程。_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945538699_eventvla_fig2.png) 

_Figure 2：EventVLA 框架架構。EventVLA 維護一個由基礎視覺錨點(visual anchors)與互動驅動事件關鍵幀(event keyframes)組成的稀疏視覺證據記憶庫，並透過 KEM 模組進行關鍵事件記憶的建立與檢索。_

  * 要解決的問題：既有記憶增強 VLA 方法各有缺陷——資訊瓶頸（記憶壓縮過度損失細節）、雙系統解耦導致高延遲、或不加篩選的緩衝區造成大量視覺資訊冗餘，使模型難以應對任務相關視覺線索被遮擋或消失的長時程場景。
  * Main method：提出「稀疏視覺證據記憶」（sparse visual evidence memory）概念，由兩部分組成：
    * 基礎視覺錨點（foundational visual anchors）：保留任務初始狀態與短期脈絡的視覺資訊。
    * 動態關鍵幀證據記憶模組（Keyframe Evidence Memory, KEM）：此模組的核心創新是「直接從 VLA 的潛在嵌入預測未來關鍵幀機率」，即模型會自主判斷「未來會需要用到當前這一幀的資訊嗎」，若判斷未來有用（因果效用高），便將其視為關鍵幀捕捉並存入記憶，而非事後才決定該保留哪些幀。
    * 這種「前瞻驅動」（foresight-driven）機制讓策略能在視覺證據即將變得不可觀測（如被遮擋）之前，提前保存下來，而非被動累積所有歷史畫面。
  * 和以往方式的差異：相較於既有方法的三種缺陷模式（資訊瓶頸 / 雙系統高延遲 / 冗餘緩衝區），EventVLA 走「端到端＋稀疏事件驅動」路線——不需要獨立的第二套系統，也不需儲存完整歷史，而是用模型自身潛在表徵主動預測「未來會用到什麼」，只保留稀疏但任務關鍵的視覺事件。
  * 重要方法設計描述：可將此架構想像為一條主幹管線（視覺錨點提供基礎脈絡），並聯一個「預測性守門員」模組（KEM）——該守門員持續監看當前潛在表徵，預測「這一幀在未來是否會成為關鍵證據」，若是則將其存入稀疏記憶庫；決策時，策略同時參考視覺錨點與 KEM 中挑選出的關鍵幀證據，而非參考完整歷史或經過壓縮損失的單一記憶向量。



### Result

  * 論文額外提出 RoboTwin-MeM 診斷型基準，專門用於評測具互動視覺證據的非馬可夫操作任務，此舉本身即是對社群的一項貢獻（提供更精準的記憶能力評測工具）。
  * 在 17 個需要記憶的模擬任務與 4 個真實世界雙臂任務上，EventVLA 相較於最先進的記憶增強 VLA 平均成功率提升 +40%，此為相當顯著的增幅。
  * 是否公正：摘要提供了具體評測任務數量（17+4）與平均提升幅度（+40%），但「最先進的記憶增強 VLA」具體所指哪些方法（是否包含 MemoryVLA、LaMem-VLA 等）在摘要中未明確列出，需要查證全文確認比較基線的公允性,以及是否有其他論文對 RoboTwin-MeM 這個新基準提出不同的評測結果或方法論質疑。



### Limitation

  * 摘要未明確自陳限制。從方法設計推測，KEM 模組依賴「預測未來關鍵幀機率」的準確性，若預測失準（誤判某幀不重要而遺漏，或誤判次要幀為關鍵幀造成記憶庫充斥雜訊），可能影響長時程任務表現，但這僅為根據架構原理的推測。
  * 論文提出的新基準 RoboTwin-MeM 是否會因為由同一團隊設計而傾向對自身方法有利,也是值得留意的潛在問題，需要查證全文與後續社群復現結果。



### Related work

  * 摘要中提及既有記憶增強方法的三種缺陷模式（資訊瓶頸、雙系統高延遲、冗餘緩衝區），隱含與 MemoryVLA/MemoryVLA++（感知-認知記憶庫，可能有資訊瓶頸疑慮）、Explicit Language Memory（顯式語言記憶＋階層雙系統，可能有高延遲疑慮）等論文的對照與潛在挑戰關係，但摘要未明確點名。
  * 暫無發現此篇之後更新的直接後續研究，但其提出的 RoboTwin-MeM 基準本身可能成為後續 VLA 記憶研究的標準評測工具，值得追蹤其後續是否被廣泛採用。



### Conclusion

  * 綜合評價：EventVLA 提出「前瞻驅動的稀疏事件記憶」是一個有新意且直觀合理的設計（讓模型主動判斷「未來會用到什麼」而非被動記錄一切），+40% 的平均提升幅度相當顯著，且额外貢獻了 RoboTwin-MeM 診斷基準，對於關心長時程記憶機制與評測方法論的讀者都值得參考。
  * 與其他重要文章的關係：本文明確以既有「記憶增強 VLA」方法的三類缺陷作為出發點進行挑戰，隱含批評/超越 MemoryVLA 系列（資訊瓶頸疑慮）與 Explicit Language Memory（雙系統延遲疑慮）等路線，是同一研究主題（VLA 記憶機制）下的競爭性方法，具體比較細節需查證全文。
  * ROCm/AMD 待補強部分：摘要未提及任何特定硬體平台。EventVLA 強調「端到端」（無需雙系統）以降低延遲，此設計理念本身即隱含對推論效率的重視，但論文並未提供在特定硬體（如 GPU 廠商）上的延遲/吞吐量數據，因此無法判斷其與 ROCm 平台優化的具體關聯；若企業關心低延遲端到端 VLA 推論在 ROCm 上的表現，此為值得後續查證全文並自行測試的方向，但論文本身未提供相關資訊。