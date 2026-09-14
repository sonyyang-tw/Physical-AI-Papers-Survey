---
layout: paper
title: "DFM-VLA: Iterative Action Refinement for Robot Manipulation via Discrete Flow Matching"
section: vla
page_id: "1945538880"
permalink: /Physical-AI-Papers-Survey/vla/dfm-vla-iterative-action-refinement-for-robot-manipulation-via-discrete-flow-mat-1945538880/
---

**Paper** : [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)](https://arxiv.org/abs/2503.09215)  
**Source** : arXiv (cs.CV / cs.AI)  
**arXiv ID** : 2503.09215

### Abstract

EOT-WM 是一個自動駕駛用的世界模型，重點在於同時控制「自車（ego vehicle）」與「他車（other vehicles）」的軌跡，用於生成更真實的駕駛模擬影片。作者指出，先進的端到端自動駕駛系統會預測他車的運動並規劃自車軌跡，而現有的世界模型多半只強調自車軌跡的可控性，讓他車運動不可控，因而難以真實模擬自車與周遭環境的互動。EOT-WM 先將 BEV（鳥瞰圖）空間中自車與他車的軌跡投影到影像座標，以像素位置將軌跡與影片中對應的車輛匹配；再用時空變分自編碼器（Spatial-Temporal VAE）將軌跡影片編碼，與駕駛影片的潛在表示在時空上對齊；並設計軌跡注入式擴散 Transformer（trajectory-injected diffusion Transformer）對含噪潛在影片去噪以生成影片。作者也提出一個基於控制潛在相似度的新指標評估軌跡可控性。在 nuScenes 資料集上的實驗顯示，該方法相較 SOTA 方法 FID 提升 30%、FVD 提升 55%，並能用自產軌跡預測未見過的駕駛場景。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945538880_dfmvla_fig1.png) 

_Figure 1: 解碼範式比較 ——(1) 自迴歸（AR）模型需要與動作序列長度相同的步數；(2) 離散擴散/流匹配方法可用更少步數迭代精煉動作。_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945538880_dfmvla_fig2.png) 

_Figure 2: DFM-VLA 整體架構 ——給定語言-視覺上下文與帶噪動作 token，模型預測乾淨動作並透過離散流匹配進行迭代式精煉。_

  * 要解決的問題：既有的駕駛世界模型只能可控地生成自車軌跡，他車運動是不可控（隨機或依賴資料分佈），無法真實模擬自車與其他交通參與者之間的互動場景，限制了世界模型作為模擬器評估自動駕駛系統的可信度。
  * Main method：EOT-WM（Ego-Other vehicle Trajectories World Model）統一控制自車與他車軌跡於同一影片潛在空間，核心分三部分：
    * Video-based Trajectory Representation（VTR）：將 BEV 空間中每台車（自車＋他車）的軌跡投影到影像座標系，透過像素位置將軌跡與影片畫面中的對應車輛匹配。
    * Aligned Motion Guidance Generation（AMGG）：用時空 VAE 將這些「軌跡影片」編碼，使其在空間與時間上都能與駕駛影片本身的潛在表示對齊。
    * Trajectory-injected Diffusion Transformer（TiDiT）：以擴散 Transformer 對含噪的影片潛在做去噪，並在去噪過程注入軌跡引導訊號，生成受控的駕駛影片。
  * 與以往方式的差異：以往方法（如僅以自車軌跡或路徑點作為條件）忽略他車的可控性，導致模擬中他車行為與真實互動脫節；EOT-WM 把多台車的軌跡都轉換到統一的視覺潛在空間中處理，讓生成模型能同時「看懂」自車與他車的運動意圖。
  * 重要方法設計描述：模型建構於 CogVideoX（一個文字/影像轉影片的擴散模型）之上；輸入端除了原始駕駛影片外，還有一組軌跡影片（把每輛車的未來軌跡畫成視覺化的軌跡圖層，位置對應影像座標系）；這些軌跡影片經 VTR 對齊車輛身份、經 AMGG 編碼成與駕駛影片同維度的潛在張量；TiDiT 在擴散去噪的每一步將軌跡潛在與影片潛在共同輸入 Transformer，逐步去噪生成最終的駕駛影片，因此軌跡條件可以同時影響自車與畫面中每台他車的運動軌跡。



### Result

  * 主要成果：在 nuScenes 資料集上，相較於當時的 SOTA 方法，FID 提升 30%，FVD 提升 55%；並提出新指標（基於控制潛在相似度）評估軌跡可控性，顯示軌跡控制的忠實度較高。此外模型可用自己生成的軌跡去預測未見過的駕駛場景，顯示一定的泛化能力。
  * 增強部分：主要增強了「影片生成品質」（FID/FVD 大幅提升）與「多車軌跡可控性」，這是相對於先前只控制自車軌跡的方法的核心差異化優勢。
  * 是否公正：摘要中提供的 FID/FVD 提升百分比是作者自行比較的結果，未說明具體比較對象是哪一個/哪幾個 SOTA baseline，也未見第三方或後續論文對這些數字的獨立驗證。需要查證其他論文（例如後續的 driving world model benchmark 論文）是否有對 EOT-WM 的結果做過交叉驗證或提出不同看法。



### Limitation

  * 論文中自陳的限制：僅讀取 arXiv abstract 頁面，摘要本身未列出明確的 limitation 章節內容。
  * 從結果推測的弱項：
    * 方法依賴 BEV 到影像座標的投影與像素位置匹配，在遮蔽（occlusion）嚴重或車輛密集重疊的場景中，軌跡與車輛的匹配可能不穩定，但摘要未討論此情形。
    * 僅在 nuScenes（單一資料集、特定感測器配置與地區）上驗證，跨資料集或跨感測器配置的泛化性未知。
    * 論文歷經多次修訂（v1 到 v4，橫跨 2025 年 3 月至 11 月），可能反映方法或評估在審稿過程中有調整，但無法從摘要判斷具體變更內容。



### Related work

  * 根據網路搜尋，該研究方向已有後續相關工作，例如 2026 年的「EgoExo-WM: Unlocking Exo Video for Ego World Models」以及「Ego-Dynamics-Augmented World Model for Autonomous Driving with Zero-Shot Cross-Chassis Adaptation」，顯示 driving world model 領域持續朝向更豐富的視角融合與跨載具泛化發展。另外 2025 年 10 月出現的survey「A Comprehensive Survey on World Models for Embodied AI」(arXiv:2510.16732) 有引用本論文，可作為快速掌握該領域全貌的入口。
  * Related work 值得 survey 的程度：高。此領域（driving world model 的可控性與多主體互動模擬）持續有新工作發表，建議透過上述 survey 快速定位其他相關方法並比較。



### Conclusion

  * 綜合評價：EOT-WM 針對「他車軌跡不可控」這一具體且實用的問題提出了清晰的架構解法（VTR + AMGG + TiDiT），FID/FVD 提升幅度可觀，是駕駛世界模型可控性研究中值得參考的一篇工作，尤其其軌跡到影像座標的投影技巧具有工程可複製性。
  * 與其他重要文章的關係：延伸自以 CogVideoX 等影片擴散模型為底座的 driving world model 系列工作，挑戰的是「只能控制自車軌跡」這類先前方法的局限；與後續的 EgoExo-WM、Ego-Dynamics-Augmented World Model 等工作在同一脈絡下持續演進。
  * ROCm/AMD 待補強部分：摘要未提及訓練/推論所使用的硬體平台或框架細節，看不出與 ROCm/AMD 的明確關聯，不宜臆測。若團隊要在 AMD 硬體上復現此類以 CogVideoX 為底座的擴散 Transformer 訓練流程，需要另外查證 CogVideoX 系列模型在 ROCm 上的支援狀況。