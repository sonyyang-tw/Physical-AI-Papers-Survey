---
layout: paper
title: "Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning"
section: wm
page_id: "1963892209"
permalink: /wm/cosmos-policy-fine-tuning-video-models-for-visuomotor-control-and-planning-1963892209/
---

### Abstract

近期影片生成模型展現出捕捉複雜物理交互與場景演化的強大能力，機器人研究因此嘗試將影片模型改造為 policy，但既有作法往往需要多階段後訓練與額外的動作生成架構元件，徒增複雜度。本文提出 Cosmos Policy，一套將大型預訓練影片模型（Cosmos-Predict2）改造為有效機器人 policy 的簡潔方法：僅需在目標平台採集的機器人示範資料上進行單一階段後訓練，且不需任何架構修改。Cosmos Policy 將機器人動作編碼為影片模型潛在擴散過程中的「潛在影格」（latent frame）直接生成，充分利用模型既有的預訓練先驗與學習演算法來捕捉複雜的動作分布；此外，模型同時以相同方式生成未來狀態影像與價值（預期累積獎勵），使推論時能對動作軌跡進行測試時規劃（test-time planning），提高成功機率。在 LIBERO 與 RoboCasa 模擬 benchmark 上，Cosmos Policy 分別達到 98.5% 與 67.1% 的平均成功率，刷新 state-of-the-art 紀錄；在具挑戰性的真實世界雙臂操作任務上，其平均分數也超越從頭訓練的強力 diffusion policy、既有影片模型 policy，以及在相同機器人示範資料上微調的 state-of-the-art VLA 模型。此外，給定 policy rollout 資料後，Cosmos Policy 還能從經驗中持續精煉其 world model 與價值函數，並利用 model-based planning 在困難任務上達到更高成功率。本文已被 ICLR 2026 接受。

### Method

**要解決的問題：** 將預訓練影片模型的時空先驗遷移至機器人 policy 學習，是提升泛化性與資料效率的一條有前景路線，但既有方法通常需要引入新的動作生成架構（例如額外的 action head 或 diffusion policy 頭），並拆分成多階段後訓練流程（先做影片預測微調，再接動作解碼器訓練），這使得整個系統複雜、難以維護，也可能無法充分利用影片模型原本學到的先驗知識。

**Main method：** Cosmos Policy 的核心創新是「潛在影格注入」（latent frame injection）：不修改 Cosmos-Predict2 影片擴散模型的架構，而是將機器人動作、未來狀態（本體感覺 proprioception + 影像觀測）與價值估計，都編碼成該模型序列結構中的「潛在影格」，與原本的影像/動作序列一起透過同一套影片擴散學習目標聯合建模。換言之，動作生成、未來預測與價值評估全部被重新表述為「生成下一批潛在影格」的問題，因此可以直接沿用影片模型既有的訓練演算法與預訓練權重，僅需單一階段的機器人示範資料後訓練即可完成適配。推論時，模型不僅輸出動作序列，還同時生成對應的未來狀態影像與價值估計，讓系統能在測試時對多條候選動作軌跡進行規劃篩選，挑出預期價值最高者執行。

**和以往方式的差異：** 相較於既有「影片模型 + 額外動作頭 + 多階段訓練」的典型範式，Cosmos Policy 完全不引入新架構元件，僅靠「潛在影格注入」這一表示層級的巧思，就讓同一個影片擴散骨幹同時肩負動作生成、未來預測與價值評估三種功能，訓練流程也簡化為單一階段。這使其能更充分保留並利用預訓練影片模型的先驗知識，同時透過生成的價值估計啟用測試時規劃，這是既有 VLA 或影片模型 policy 方法所不具備的能力。

下圖為 Cosmos Policy 總覽（圖一）與潛在擴散序列/潛在影格注入機制圖解（圖二）：

![Figure](/assets/images/1963892209_cosmos_fig1.jpeg) ![Figure](/assets/images/1963892209_cosmos_fig2.jpeg) 

### Result

Cosmos Policy 在 LIBERO 模擬 benchmark 上達到 98.5% 平均成功率，在 RoboCasa 24 項廚房操作任務上達到 67.1% 平均成功率，均為當前最佳（state-of-the-art）。在真實世界 ALOHA 雙臂機器人任務評測中，Cosmos Policy 的平均分數超越從頭訓練的強力 diffusion policy、既有影片模型 policy，以及在同一批機器人示範資料上微調的 π0.5、OpenVLA-OFT+ 等 state-of-the-art VLA 模型；論文並展示 π0.5 與 OpenVLA-OFT+ 在高精細度動作長 horizon 任務上的具體失敗模式作為對照。此外，作者證明給定 policy rollout 資料後，Cosmos Policy 能以自身生成的經驗持續精煉 world model 與價值函數，並藉由 model-based planning 在困難任務上進一步提升成功率，顯示其潛在影格架構具備自我改進的閉環潛力。由於評測涵蓋公開模擬 benchmark（LIBERO、RoboCasa）與真實硬體（ALOHA）雙軌驗證，且與多個公開發表的強力 baseline（diffusion policy、π0.5 等）直接比較，結果具備較高的公正性與可信度。

### Limitation

論文聚焦於方法有效性驗證，對限制的討論相對簡略，但可推論的弱項包括：(1) 模型高度依賴 Cosmos-Predict2 這一特定預訓練影片基礎模型的品質與先驗，若遷移至其他影片模型骨幹，潛在影格注入機制的有效性尚待驗證；(2) 真實世界評測僅限 ALOHA 雙臂平台，跨具身（如人形、單臂、四足）的可遷移性未見系統性驗證；(3) 影片擴散模型的推論延遲相較輕量 VLA policy 通常較高，論文雖展示了測試時規劃的效能提升，但未充分討論其對即時部署延遲/吞吐量的影響，這在需要高頻控制的接觸密集型任務上可能構成部署瓶頸。

### Related work

Cosmos Policy 與本頁已收錄的 Robot-Specific Action-Conditioned World Models 類別論文（如 Ctrl-World、τ0-WM、WEAVER）同屬「將 world model 生成能力與機器人動作耦合」的技術路線，但 Cosmos Policy 的獨特之處在於：它並非另外設計一個獨立的 world model 供 policy 查詢，而是直接把動作、狀態預測、價值估計統一表述為同一影片擴散模型的潛在影格生成任務，架構上更為精簡。此外，Cosmos Policy 與 NVIDIA 同期發布的 DreamZero（arXiv:2602.15922，已於本頁 2026-09-09 推送記錄收錄）同樣師承「video as dense world representation」的理念，但 DreamZero 聚焦於零樣本跨具身泛化與 RoboArena 排行榜驗證，Cosmos Policy 則更聚焦於測試時規劃與價值估計的整合，兩者可視為 NVIDIA 在「影片模型即 policy」路線上的互補嘗試，值得後續合併追蹤其技術收斂方向。

### Conclusion

Cosmos Policy 以簡潔優雅的「潛在影格注入」機制，證明了預訓練影片模型可以在幾乎不增加架構複雜度的情況下，同時勝任動作生成、未來預測與價值評估三重角色，並在模擬與真實世界評測上都取得業界頂尖成績，是 World-Action Model 路線上兼具方法論簡潔性與實證強度的重要工作，值得優先參考。就與其他重要文章的關係而言，Cosmos Policy 與 DreamZero、τ0-WM 等論文共同勾勒出「影片模型逐漸取代/融合傳統 VLA 動作頭」這一新興技術匯流趨勢。就 AMD/ROCm 而言，Cosmos Policy 直接建立在 NVIDIA Cosmos-Predict2 這一與 CUDA 生態系深度綁定的影片基礎模型之上，凸顯出 ROCm 目前在「大型影片擴散基礎模型的高效訓練與推論」這塊拼圖上的顯著缺口——若要在 AMD 硬體上復現或改良此類「影片模型即 policy」的研究路線，需要先補齊對等規模、對等品質的開源影片擴散基礎模型與相應的 ROCm 優化訓練/推論框架，這是現階段 AMD/ROCm 生態系亟待補強的關鍵基礎設施。