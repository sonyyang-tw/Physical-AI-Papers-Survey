---
layout: paper
title: "Pelican-Sim 1.0: A General World Model Simulator for Embodied Intelligence"
section: wm
page_id: "1968596049"
permalink: /zh/wm/pelican-sim-1-0-a-general-world-model-simulator-for-embodied-intelligence-1968596049/
---

### Abstract

Pelican-Sim 1.0（arXiv:2609.12036，2026年9月10日提交，AgiBot 旗下 Beijing Innovation Center of Humanoid Robotics）是一個通用型 world model 模擬器，用於預測機器人在給定視覺情境與動作下的未來觀測，以支援下游學習與決策。模型有四項關鍵設計：(1) 統一 28 維動作值空間，涵蓋主流異質具身，讓單一模型可跨裝置使用；(2) Action-visual injection：以 URDF 與相機渲染的動作影片橋接動作與像素，大幅提升跨具身/場景/任務的可控性（PSNR 較其他融合基線 +0.904）；(3) Sparse mixture-of-experts (MoE)：稀疏 MoE 層為異質動態提供額外容量並吸收動作模態，降低模態間衝突（FVD 較 dense backbone -6.530）；(4) 高效 rollout 生成：因果適配 (causal adaptation) 與少步驟蒸餾產出僅需 4 步的自迴歸模擬器，較 35 步教師模型加速 5.67 倍。訓練資料約 100 萬筆真實與模擬軌跡，於 AgiBotWorld Beta、RoboMIND、RoboTwin 三個 benchmark 上 PSNR 分別提升 4.636、2.080、10.343；下游應用上，於 RoboTwin 每任務加入 500 筆生成軌跡（原僅 50 筆示範）可將 policy 成功率從 70% 提升至 93%，policy 評估的 Pearson 相關係數達 0.994。

### Method

**要解決的問題**：現有 world model 多針對單一具身或單一任務域訓練，難以跨異質機器人平台（不同自由度、不同動作空間）通用，且動作條件與像素預測之間的耦合（controllability）往往不足，導致模擬結果對動作變化不夠敏感或不夠準確。

**Main method**：(1) 以 28 維統一動作值空間表示跨主流具身的動作；(2) Action-visual injection 機制，將 URDF 結構與相機標定資訊渲染成「動作影片」，作為額外訊號注入 Video DiT 骨幹（於偶數層以 Context Block 注入動作影片殘差，奇數層以動作值 embedding 做 scale-and-shift 調變）；(3) 在 Video DiT 中加入稀疏 MoE 層，讓不同專家分別吸收不同具身/動態模式，減少模態衝突；(4) 透過因果適配與少步驟蒸餾，將原本 35 步的擴散 rollout 壓縮為 4 步自迴歸生成，達成 5.67 倍加速。

**和以往方式的差異**：與既有機器人 world model（如本頁已收錄的 τ0-WM、WEAVER、Ctrl-World）多半僅在單一或少數具身上驗證不同，Pelican-Sim 1.0 以統一動作值空間 + URDF/相機渲染的動作影片顯式橋接動作與像素，是首次系統性地在架構層面同時解決「跨具身通用」與「動作可控性」兩個問題，並輔以稀疏 MoE 處理由此帶來的異質動態衝突，屬於架構層面的組合創新而非單一技巧的延伸。

**關鍵方法圖**：Figure 1（teaser）展示 Pelican-Sim 1.0 的整體概覽——輸入初始 RGB 影像、28 維統一動作值與相機對齊的動作影片，輸出未來觀測預測；Figure 3 展示模型架構——28 層 Video DiT 如何同時接收動作值 embedding（調變）與動作影片殘差（Context Block 注入），以及稀疏 MoE 層如何結合共享專家與路由專家輸出。

![Figure]({{ site.baseurl }}/assets/images/2609.12036_pelican_teaser.png)

_Figure 1: Pelican-Sim 1.0 整體概覽_

![Figure]({{ site.baseurl }}/assets/images/2609.12036_pelican_archi.png)

_Figure 3: 模型架構 — Video DiT + 稀疏 MoE_

### Result

**Result 結果如何**：在三個 benchmark（AgiBotWorld Beta、RoboMIND、RoboTwin）上，PSNR 較最強基線分別提升 4.636、2.080、10.343，RoboTwin 上 EWMBench DYN 分數提升 0.426；下游四項應用全部成功驗證：(a) 資料擴增——500 筆生成軌跡加 50 筆示範使 policy 成功率從 70% 提升至 93%；(b) policy 評估——五個 checkpoint 間 Pearson 相關係數達 0.994；(c) action selection 相對提升 47.7%；(d) policy improvement 相對提升 20.3%。

**Result 是否公正**：論文在三個獨立 benchmark 上一致展現優勢，且下游應用涵蓋資料生成、policy 評估、action selection、policy improvement 四種不同用途，交叉驗證了模型的實用性而非單一指標的過擬合；然而作為技術報告（technical report）而非經同行評審的會議論文，其比較基線的選取與實驗設計未經第三方審稿把關，仍待後續獨立復現或會議接受後進一步確認。

### Limitation

**已知的 limitation**：論文本身為技術報告，尚未標註具體會議接受狀態；跨具身泛化雖有定性展示（trajectory、scene、object、embodiment、viewpoint shifts），但四項下游應用的量化驗證僅在 RoboTwin 單一 benchmark 上進行，尚未在 AgiBotWorld Beta 或 RoboMIND 上驗證下游應用效果。

**從 result 來看 limitation 和弱項**：4 步自迴歸模擬器相較 35 步教師模型雖有 5.67 倍加速，但論文未充分討論蒸餾後模型在長 horizon rollout 下是否會累積誤差放大；稀疏 MoE 對訓練/推論記憶體開銷的影響亦未見詳細分析。

### Related work

arXiv 上更新的 related work：本頁已收錄的 τ0-WM（AGIBOT，統一影片-動作 world model）、Ctrl-World（ICLR 2026，可控多視角生成式 world model）、DreamDojo（NVIDIA GEAR，大規模人類影片預訓練）皆屬同一「機器人專用 action-conditioned world model」子主題，可與 Pelican-Sim 1.0 在「跨具身統一動作表示」與「訓練資料規模化」兩個維度上做比較。

值得 survey 的程度：中高。Pelican-Sim 1.0 的 action-visual injection 與稀疏 MoE 設計具體回應了跨具身 world model 的核心痛點，值得追蹤其後續版本（如 Pelican-Sim 2.0）是否引入更大規模訓練資料或延伸至人類影片預訓練。

### Conclusion

**綜合評價**：Pelican-Sim 1.0 在架構設計上系統性地解決跨具身 world model 的可控性與異質動態衝突問題，並以四項下游應用（資料擴增、policy 評估、action selection、policy improvement）驗證實用價值，出自 AgiBot 旗下研究機構，符合大廠/知名實驗室出品準則；雖為技術報告尚未見明確會議接受狀態，但方法論創新程度與驗證完整度足以列入本頁「Robot-Specific Action-Conditioned World Models」子主題參考文獻。

**與其他重要文章的關係**：與本頁已收錄的 τ0-WM、DreamDojo、Ctrl-World 構成「機器人專用 world model」譜系，並與同源團隊 AGIBOT 的 τ0-VLA（VLA Papers 頁面已收錄）在資料與具身工程上可能共享基礎設施，形成 AgiBot 世界模型與 VLA 兩條產品線的交叉參照點。ROCm/AMD 待補強：Pelican-Sim 1.0 的稀疏 MoE 層與 Video DiT 混合架構、以及少步驟蒸餾後的 4 步自迴歸推論管線，對 ROCm 上大規模影片擴散模型 + MoE 混合架構的推論優化（尤其是動作影片殘差注入這類非標準 cross-attention 路徑）目前公開的最佳化方案有限，是 AMD 在此類跨具身 world model 推論加速上可切入的方向。
