---
layout: paper
title: "Let It Be Simple: One-Step Action Generation for Vision-Language-Action Models"
section: vla
page_id: "1945767397"
permalink: /Physical-AI-Papers-Survey/vla/let-it-be-simple-one-step-action-generation-for-vision-language-action-models-1945767397/
---

**Paper** : [Mastering diverse control tasks through world models](https://www.nature.com/articles/s41586-025-08744-2)（arXiv 預印本：[Mastering Diverse Domains through World Models](https://arxiv.org/abs/2301.04104)）  
**Source** : Nature（2025）／arXiv 預印本  
**arXiv ID** : 2301.04104

### Abstract

DreamerV3 是 Danijar Hafner 等人（Google DeepMind）提出的通用強化學習演算法，透過學習環境的世界模型，並在該模型中「想像」未來情境來改善行為策略。單一組態即可在超過 150 種跨領域任務（機器人操作與移動、Atari 2D 遊戲、DMLab 與 Minecraft 等 3D 環境）中超越專用方法，無需針對每個新任務進行大量人工調參。其代表性成果是首個在無人類資料或課程設計的情況下、從零開始在 Minecraft 中學會挖到鑽石的演算法。該研究最初於 2023 年以 arXiv 預印本形式發表，2025 年 4 月正式登上 Nature 期刊。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945767397_letitbesimple_fig1.png) 

_Figure 1: Benchmark summary。使用固定超參數，Dreamer 在多種基準與資料預算下超越調校過的專家演算法，並大幅優於 PPO；同時 Dreamer 在 Minecraft 遊戲中僅憑稀疏獎勵從零開始學會挖鑽石，這是先前方法需要人類資料或領域啟發式規則才能解決的長期挑戰。_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945767397_letitbesimple_fig2.png) 

_Figure 3 (a) World Model Learning: Dreamer 的訓練流程。世界模型（RSSM）將感官輸入編碼為離散表示 z_t，並由具遞歸狀態 h_t 的序列模型依動作 a_t 預測；輸入被重建以確保表示具資訊量，演員與評論家則依世界模型預測的抽象表示軌跡學習動作與價值。_

  * 要解決的問題：現有強化學習演算法雖可用於與其訓練情境相似的任務，但要套用到新的應用領域，通常需要大量人工專業知識與反覆試驗來調整超參數，缺乏一個能「開箱即用」跨領域運作的通用演算法。
  * Main method：Dreamer 學習一個環境的世界模型（將感測輸入編碼為離散的分類表徵，並預測未來的表徵與獎勵），再利用該世界模型「想像」（imagine）未來的多步軌跡，在想像空間中訓練 actor-critic 策略，而非只依賴與真實環境互動的資料。
  * 與以往方式的差異：DreamerV3 引入一系列穩健性技巧——包括對數值進行正規化（normalization）、損失平衡（balancing）、以及變換（transformations）——使同一套固定超參數組態能穩定地跨越不同尺度的獎勵、觀測空間與動作空間，而不需針對每個領域重新調參，這與過去需要大量領域特定調校的 RL 方法形成明顯差異。
  * 重要方法設計：世界模型以類別表徵（categorical representations）編碼觀測，並以循環網路預測未來的潛在表徵與獎勵；行為學習則完全在想像出來的潛在軌跡中進行梯度更新，模型規模與資料效率、最終表現之間呈現良好的擴展性（scaling）關係，即模型越大，資料效率與最終效果越好。



### Result

  * 結果：DreamerV3 以單一固定配置在超過 150 個任務上超越了各領域專用方法，涵蓋機器人操作、移動、Atari、DMLab、Minecraft 等差異極大的環境。最具代表性的成果是應用於 Minecraft 挖鑽石任務——一個公認需要在像素輸入、稀疏獎勵下探索長遠策略的開放世界難題——DreamerV3 是首個無需人類示範資料或課程學習即可從零完成該任務的演算法。
  * 主要增強部分：跨領域通用性（一套配置適用多領域）與資料效率（模型規模擴大能直接轉化為更高的資料效率與最終表現）是本文最主要的貢獻。
  * 是否公正/需查證處：摘要與新聞摘要著重於「超越專用方法」的整體性描述，但未列出具體的跨領域數值比較表；是否所有 150+ 任務上都全面優於「每個任務量身訂做」的最佳專用方法，仍需要查證論文正文與後續復現研究（例如是否有部分任務子集表現略遜於高度調校過的專用基線）。



### Limitation

  * 摘要未明確自陳具體限制段落，但從論文定位可推測：Dreamer 系列依賴世界模型的預測品質，若環境動態高度隨機或難以用緊湊的潛在表徵捕捉（例如高度多代理人、對抗性環境），世界模型的想像軌跡可能與真實環境產生偏差，進而影響策略品質。
  * 需要進一步查證全文以了解：計算與記憶體開銷（想像式 rollout 訓練通常比純 model-free RL 更耗算力）、在部分任務上是否仍不及極度調校過的專用 SOTA 方法。



### Related work

  * DreamerV3 是 Dreamer/DreamerV2 系列的第三代版本，屬於 model-based RL 世界模型路線的代表性延伸；與 GAIA、Genie、Cosmos 等以生成影片/場景為導向的世界模型不同，DreamerV3 更聚焦於「用世界模型提升 RL 策略學習效率」這一目標。
  * 暫無發現明確的、直接取代 DreamerV3 的最新後續研究（截至目前搜尋結果），但 model-based RL 與世界模型結合的研究方向持續活躍，值得留意後續是否有整合大型視覺-語言模型的新一代 Dreamer 變體。
  * 判斷 related work 值得 survey 的程度：高，DreamerV3 是強化學習與世界模型交叉領域的重要里程碑，適合與 V-JEPA 2-AC（同樣涉及以世界模型做規劃/控制）做方法論比較。



### Conclusion

  * 綜合評價：DreamerV3 是強化學習領域極具影響力的通用演算法，其「單一配置跨多領域」與「Minecraft 鑽石任務」的成果具有高度指標性，值得認真參考，尤其對於關注如何用世界模型提升樣本效率與泛化能力的研究者。
  * 與其他文章關係：與 GAIA 系列、Genie 3、Cosmos 3 等以生成影片/互動環境為主的世界模型相比，DreamerV3 走的是「以世界模型輔助策略優化」的路線，兩者可視為世界模型應用的兩個不同分支（生成模擬 vs. 決策規劃）；與 V-JEPA 2-AC 相比，兩者都追求以學習到的世界模型進行規劃，但 DreamerV3 採用像素級/類別表徵重建式建模，V-JEPA 2 則採用聯合嵌入預測（不重建像素）的自監督表徵。
  * ROCm/AMD 關聯：論文摘要與技術報導中未提及使用的具體硬體平台或訓練基礎設施，看不出與 ROCm/AMD 有明確關聯；若要補強，可推測的方向是評估 Dreamer 類世界模型（含循環網路與 actor-critic 想像式訓練）在 ROCm 上的訓練吞吐與穩定性，但此為推測，論文本身未觸及。