---
layout: paper
title: "Inference-time Physics Alignment of Video Generative Models with Latent World Models"
section: wm
page_id: "1959634541"
permalink: /wm/inference-time-physics-alignment-of-video-generative-models-with-latent-world-mo-1959634541/
---

### Abstract

當前最先進的影片生成模型能產生視覺上頗具說服力的內容，卻經常違反基本物理法則，限制了其實用性。過去多將此歸咎於預訓練階段物理理解不足，但本文作者發現，物理合理性的缺陷同時也源自次優的推論策略。作者因此提出 WMReward，將「提升影片生成的物理合理性」重新定義為一個推論時對齊（inference-time alignment）問題：利用潛在世界模型（本文採用 Meta 的 V-JEPA 2）強大的物理先驗作為獎勵訊號，在生成過程中搜尋並引導多條候選去噪軌跡，藉由擴大測試時運算量（test-time compute scaling）換取更佳的生成表現。實驗顯示此方法在影像條件式（I2V）、多幀條件式（V2V）與文字條件式生成情境下，皆顯著提升物理合理性，並經人類偏好研究驗證。值得注意的是，在 ICCV 2025 Perception Test PhysicsIQ Challenge 中，本方法以 62.64% 的最終分數奪得第一名，超越先前最佳結果 7.42 個百分點。本研究證明了利用潛在世界模型提升影片生成物理合理性的可行性，且此思路不侷限於特定的模型實作或參數化方式。

### Method

**要解決的問題** ：現有影片生成模型（無論是 image-to-video 或 video-to-video）常產生違反物理直覺的結果（如物體穿透、不合理的碰撞反應），過去研究多將此歸因於訓練資料或架構本身的物理理解不足，而較少探討「推論策略」本身是否也是造成物理不合理性的根本原因之一。

**Main method** ：作者提出 WMReward——以 V-JEPA 2（Meta 的自監督潛在世界模型）作為物理合理性的獎勵函數，在影片擴散模型的推論階段，對多條候選去噪軌跡進行搜尋與引導（search and steer），本質上是將測試時運算規模化（test-time compute scaling）應用於影片生成的物理對齊問題：不需重新訓練生成模型本身，僅在推論時額外花費運算資源篩選/引導出更符合世界模型物理先驗的生成結果。

**和以往方式的差異** ：與大多數改善影片生成物理合理性的既有研究（聚焦於訓練資料增強、架構改動、或訓練時的物理損失函數）不同，WMReward 完全在推論時操作，將「使用預訓練潛在世界模型作為即時獎勵訊號」與「多候選軌跡搜尋」結合，是一個與訓練時修正正交、可疊加於任意預訓練生成模型之上的新方案；同時也展示了 V-JEPA 2 這類最初為表徵學習/機器人任務設計的世界模型，可直接轉用作影片生成品質的評估與引導工具，跨越了「world model 訓練 vs. 生成模型推論」的傳統界線。

**關鍵方法圖示** ：Figure 1（已嵌入下方，teaser）展示本方法在 PhysicsIQ benchmark 上於單幀（I2V）與多幀（V2V）條件式生成情境下皆取得新的 state-of-the-art；Figure 3（已嵌入下方，method overview）詳細呈現以滑動視窗（sliding window）方式運用 V-JEPA-2 對候選去噪軌跡進行評分與引導的整體流程。

![Figure]({{ site.baseurl }}/assets/images/1959634541_wmreward_teaser.png) 

_Figure 1: 在 PhysicsIQ benchmark 上，WMReward 於 I2V 與 V2V 條件式生成皆取得新 SOTA_

![Figure]({{ site.baseurl }}/assets/images/1959634541_wmreward_method.png) 

_Figure 3: Method Overview — 以 V-JEPA-2 潛在世界模型作為獎勵，透過滑動視窗引導候選去噪軌跡_

### Result

**主要增強** ：在 ICCV 2025 Perception Test PhysicsIQ Challenge 官方排行榜上以 62.64% 最終分數奪冠，超越前一代 SOTA 達 7.42 個百分點；在影像條件式、多幀條件式、文字條件式（VideoPhy benchmark）等多種生成情境下皆有物理合理性的顯著提升，且以人類偏好研究（Physics Plausibility / Visual Quality / Prompt Alignment 三項標準的成對比較）驗證了結果的實際感知有效性，而非僅止於自動化指標的數字提升。

**結果是否公正** ：論文同時報告了視覺品質（VBench 指標，Table 5）作為對照，說明改善物理合理性並非以犧牲整體視覺品質為代價；並在 Table 4 揭露了完整的運算成本（推論時間、記憶體開銷相對倍數），對「用運算量換取物理合理性」這個核心權衡給予了透明呈現，未見刻意迴避成本揭露。PhysicsIQ Challenge 為第三方（ICCV 2025 Perception Test workshop）主辦的獨立評測，第一名成績具有較高公信力，與作者自行報告的結果相互印證。

### Limitation

**已知限制** ：作者在 Figure 10（Failure Mode Analysis）中誠實揭露即便使用 V-JEPA-2 進行推論時引導，仍存在若干持續失敗的物理現象，例如流體潑濺等急遽物理事件的建模仍不準確，顯示此方法對「世界模型本身尚未學好的物理現象」無能為力——本質上受限於底層潛在世界模型（V-JEPA-2）的物理理解上限。

**從 result 推論的弱項** ：Table 4 顯示的運算成本倍數意味著此方法屬於推論時大量增加算力換取品質的路線，實際部署時的延遲與成本可能相當可觀，對即時應用（如互動式模擬、機器人 policy-in-the-loop rollout）的適用性有限；此外方法高度依賴 V-JEPA-2 本身的物理先驗品質，若替換為較弱的世界模型，效果可能大打折扣，論文雖聲稱方法「不侷限於特定實作」，但實證僅以 V-JEPA-2 一種世界模型驗證，泛化性仍待更多世界模型的交叉驗證。

### Related work

本頁「World Model Evaluation & Physical-Reasoning Benchmarks」子主題已收錄 PhyGround、WorldBench 等物理合理性評測論文，可與本文的 PhysicsIQ/VideoPhy 評測結果相互對照；本頁基礎模型區已收錄 V-JEPA 2（arXiv:2506.09985），本文可視為其下游應用的延伸研究，展示了 V-JEPA 2 除了原本的機器人規劃/表徵學習用途外，亦可直接用作生成模型的推論時獎勵訊號，值得將兩篇論文並列閱讀以理解 V-JEPA 系列世界模型的多重應用場景。建議後續追蹤是否有將此「world model as inference-time reward」思路應用於機器人動作生成（而非僅止於影片生成）的後續論文。

### Conclusion

本文提出的「推論時物理對齊」視角是一個新穎且具啟發性的切入點，將世界模型的角色從「訓練資料生成/規劃工具」延伸為「生成品質的即時裁判與引導者」，且有第三方權威評測（ICCV 2025 PhysicsIQ Challenge 冠軍）背書，方法論貢獻與實證強度俱佳，值得參考。與本頁基礎模型 V-JEPA 2 構成「上游世界模型－下游推論時應用」的直接依存關係；與 Video-Generation World Models（子主題1，如 Genie 3、Cosmos 3）及 Evaluation & Benchmarks（子主題5）子主題則構成「生成器－評測基準－品質引導方法」的三角關係。對 ROCm/AMD 而言，此類論文凸顯的缺口在於：test-time compute scaling（多候選軌跡搜尋與引導）對記憶體頻寬與批次推論吞吐量要求極高，而目前業界公開的 V-JEPA 2 / 影片擴散模型推論效能評測與最佳化案例幾乎均基於 NVIDIA GPU，AMD 尚缺乏針對此類「world-model-guided test-time search」推論模式的 ROCm 效能基準與最佳化實踐，值得作為後續補強方向。