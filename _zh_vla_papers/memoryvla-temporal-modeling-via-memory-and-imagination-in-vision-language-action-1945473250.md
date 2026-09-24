---
layout: paper
title: "MemoryVLA++: Temporal Modeling via Memory and Imagination in Vision-Language-Action Models"
section: vla
page_id: "1945473250"
permalink: /zh/vla/memoryvla-temporal-modeling-via-memory-and-imagination-in-vision-language-action-1945473250/
---

**Paper** : [MemoryVLA++: Temporal Modeling via Memory and Imagination in Vision-Language-Action Models](https://arxiv.org/abs/2606.09827)  
**Source** : arXiv (cs.RO / cs.CV)  
**arXiv ID** : 2606.09827

### Abstract

本文為 MemoryVLA 的延伸作品，指出有效的機器人控制需要同時具備「對過去的記憶」與「對未來的想像」，然而多數 VLA 模型僅依賴當前觀測，因此在長時程、時間依賴任務上表現不佳。作者延續認知科學啟發，除了工作記憶（buffer 短期脈絡）與海馬迴式情節記憶（保存過去經驗）之外，進一步引入「內部模型想像未來狀態演化」的機制，提出 MemoryVLA++，一個完整的時間建模框架，同時賦予 VLA 模型記憶與想像能力。預訓練 VLM 將當前觀測編碼為感知與認知 token 形成工作記憶；這些 token 查詢感知-認知記憶庫以檢索相關歷史脈絡（記憶庫透過冗餘感知的整合機制更新）；一個世界模型在去噪潛在空間中想像未來狀態，並在記憶引導下將想像的潛在表徵與當前資訊整合，形成完整的時間感知 token；最終這些 token 條件化擴散動作專家，預測具時間一致性的動作序列。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473250_memoryvlapp_fig1.png) 

_Fig. 2：三種典型 VLA 範式的核心思路比較。傳統 VLA 屬於反應式(reactive)，僅依賴當前觀測；MemoryVLA 引入「工作記憶-情節記憶」機制；而 MemoryVLA++ 進一步加入想像(imagination)模組，結合記憶與世界模型對未來進行預測。_

![Figure]({{ site.baseurl }}/assets/images/1945473250_memoryvlapp_fig2.png) 

_Fig. 3：MemoryVLA++ 整體架構。當前 RGB 觀測與語言指令由 7B VLM 編碼為知覺與認知 tokens 形成工作記憶；工作記憶進一步與世界模型想像模組、時序感知動作專家(action expert)整合，實現記憶與想像雙軌的時序建模。_

  * 要解決的問題：既有 VLA（包括作者前作 MemoryVLA）僅處理過去記憶，缺乏對未來狀態的預測（想像）能力，無法完整涵蓋時間建模所需的「回顧＋前瞻」雙重需求。
  * Main method：在 MemoryVLA 的「感知-認知記憶庫」架構基礎上，新增「世界模型」（world model）模組：
    * 沿用 MemoryVLA 的工作記憶與 Perceptual-Cognitive Memory Bank 機制（VLM 編碼觀測為感知/認知 token，查詢記憶庫、冗餘感知整合式更新）。
    * 新增世界模型：在去噪潛在空間（denoising latent space）中對未來狀態進行想像式預測。
    * 想像出的未來潛在表徵在「記憶引導」（memory guidance）下與當前 token 整合，形成「完整時間感知 token」（full temporal-aware tokens），同時涵蓋過去記憶與未來想像。
    * 這些 token 條件化擴散動作專家生成動作序列。
  * 和以往方式的差異：相較於 MemoryVLA（僅有記憶、無想像）與其他既有 VLA（僅依賴當前觀測），MemoryVLA++ 首次同時整合記憶與想像兩種時間建模機制，形成「完整」時間建模（full temporal modeling）。
  * 重要方法設計描述：架構可視為在 MemoryVLA 的記憶管線之上，並聯一條「世界模型想像分支」——該分支以擴散式去噪方式在潛在空間中推演未來可能狀態，其輸出再與記憶檢索結果一起，由「記憶引導的整合」步驟融合，最終再交給動作專家解碼，形成一個記憶與想像雙軌並行、匯流至動作生成的架構。



### Result

  * 在 5 個模擬基準（Libero、SimplerEnv、Mikasa-Robo、Calvin、Libero-Plus）與跨 3 種機器人的 3 類真實機器人任務（一般操作、長時程時間依賴任務、機器人穩健性與泛化性任務）上進行大量實驗。
  * 真實機器人上分別取得 +9%（一般任務）、+26%（記憶依賴任務）、+28%（想像依賴任務）的成效提升，驗證了「記憶＋想像」完整時間建模的有效性。
  * 是否公正：論文明確列出多個公開基準與具體百分點提升，可信度較高；但這些數字是與何種基線比較（是否包含前作 MemoryVLA 本身）在摘要中未完全說明，需要查證全文以確認比較基線是否公允、以及是否有其他論文對 Libero-Plus 等基準的復現結果不同。



### Limitation

  * 摘要未明確自陳限制。從架構複雜度推測，加入世界模型後系統包含 VLM 編碼、記憶庫查詢更新、世界模型潛在空間去噪、擴散動作解碼等多重生成式模組，可能帶來較高的推論延遲與運算資源需求，但論文摘要未提供延遲/吞吐量數據，需要查證全文。
  * 摘要未提及訓練資料規模或世界模型的預測時間跨度（horizon）限制，這些都是評估其可擴展性時的重要缺口，需要進一步查證全文。



### Related work

  * 直接前作：MemoryVLA（arXiv:2508.19236，ICLR 2026），本文是其直接延伸（加入世界模型想像機制），為同一作者群的系列研究，值得對照閱讀以了解演進脈絡。
  * 摘要未提及是否與其他同期記憶/想像相關 VLA 論文（如 EventVLA、LaMem-VLA、Explicit Language Memory）比較，需要查證全文中是否有相關討論；此系列論文的持續迭代顯示「記憶＋想像」是 2026 年 VLA 領域一個活躍且值得持續追蹤的研究主線。



### Conclusion

  * 綜合評價：本文延續並補強了前作 MemoryVLA 的核心缺口（缺乏未來想像能力），在多個基準與真實機器人上都有具體且顯著的提升數字，是 VLA 時間建模研究方向中值得參考的重要進展，尤其對於關注長時程規劃與魯棒性的讀者。
  * 與其他重要文章的關係：本文直接延伸自 MemoryVLA（arXiv:2508.19236），並可能與同期出現的 EventVLA（事件驅動視覺證據記憶）、LaMem-VLA（潛在記憶原生框架）、Explicit Language Memory（顯式語言記憶）構成同一時期「VLA 時間/記憶建模」研究群體中彼此競爭或互補的方法，具體比較關係需查證全文與後續文獻。
  * ROCm/AMD 待補強部分：摘要未涉及任何硬體平台討論。由於本方法引入擴散式世界模型與擴散式動作專家的雙重生成模組，屬於運算較密集的架構，若需在 ROCm 上部署，可能涉及擴散模型迭代取樣、潛在空間操作等運算元的效能優化議題，但論文本身未提供相關資訊，這僅為基於架構複雜度的推測，並非論文結論。