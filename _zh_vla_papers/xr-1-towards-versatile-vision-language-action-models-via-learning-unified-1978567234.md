---
layout: paper
title: "XR-1: Towards Versatile Vision-Language-Action Models via Learning Unified Vision-Motion Representations"
section: vla
page_id: "1978567234"
permalink: /zh/vla/xr-1-towards-versatile-vision-language-action-models-via-learning-unified-1978567234/
---

### Abstract

XR-1（arXiv:2511.02776，ICML 2026 Oral，Beijing Innovation Center of Humanoid Robotics 與北京大學、北京航空航天大學合作）提出「X Robotic Model 1」框架，核心創新是 Unified Vision-Motion Codes (UVMC)：一個透過雙分支 VQ-VAE 學習得到的離散潛在表示，同時編碼視覺動態與機器人運動訊號，作為觀測與動作之間的中介表示，並用以對齊跨異質資料來源（不同機器人具身與人類示範）的動態資訊。作者提出三階段訓練範式：(1) 自監督 UVMC 學習、(2) UVMC 引導的跨具身通用預訓練、(3) 任務專屬後訓練。XR-1 在六種異質機器人具身、超過 120 項操作任務上進行超過 14,000 次真實世界 rollout 驗證，全面勝過 π0.5、π0、RDT、UniVLA、GR00T-N1.5 等 state-of-the-art baseline，並展現出對新物件、背景變化、干擾物與光照變化的強健泛化能力。

### Method

**要解決的問題**：現有 VLA 模型面對兩項根本挑戰：(1) 難以從高維觀測中生成精確的低階動作；(2) 難以彌合跨異質資料來源（不同機器人具身、人類示範）之間的領域落差。既有方法通常只從視覺動態或機器人動作其中一方編碼潛在變數來引導 policy 學習，未能充分利用大規模異質資料集中互補的多模態知識。

**Main method**：XR-1 的核心是 Unified Vision-Motion Codes (UVMC)——透過雙分支 VQ-VAE 學習得到的離散潛在表示，Vision Branch 以目前幀與未來幀為輸入編碼視覺動態變化（解碼器重建未來幀），Motion Branch 編碼低階動作序列與本體感覺狀態（重建動作序列），兩分支共享同一組 codebook，並以 KL 散度對齊損失強迫視覺編碼與對應動作編碼在共享潛在空間中對齊。UVMC 因而同時扮演「觀測與動作之間的中介表示」與「跨異質資料來源動態資訊對齊樞紐」兩種角色。訓練上採三階段範式：Stage-1 以 RoboMIND、Open-X、XR-D、Ego4D 等大規模異質資料自監督學習 UVMC；Stage-2 在 XR-D 跨具身資料上以 UVMC 引導通用 policy 預訓練；Stage-3 針對下游目標任務做專屬後訓練。

**和以往方式的差異**：既有方法多半只從「視覺動態」或「機器人動作」單一模態學習潛在變數來引導 policy（例如僅以影片預測或僅以動作重建為目標），XR-1 首次以雙分支 VQ-VAE 加共享 codebook 加對齊損失的方式，同時且聯合地從兩種模態萃取互補動態知識，使 UVMC 兼具跨具身通用性（作為與具身無關的抽象表示）與跨資料來源對齊能力（可同時吸收機器人示範與人類第一人稱影片如 Ego4D）。

**關鍵方法圖**：Figure 1 展示 XR-1 作為跨多種機器人具身與環境的通用 VLA 框架總覽；Figure 2 展示 UVMC 雙分支 VQ-VAE 架構與三階段訓練管線的完整細節。

![Figure]({{ site.baseurl }}/assets/images/2511.02776_xr1_teaser.png)

_Figure 1: XR-1 支援跨多種機器人具身與環境的通用穩健多工學習_

![Figure]({{ site.baseurl }}/assets/images/2511.02776_xr1_overview.png)

_Figure 2: XR-1 的 UVMC 雙分支 VQ-VAE 架構與三階段訓練範式總覽_

### Result

**Result 結果如何**：在六種異質具身（Tien Kung 1.0/2.0 人形、單/雙臂 UR-5e、雙臂 Franka、AgileX Cobot Magic 2.0）、超過 120 項任務、逾 14,000 次真實機器人 rollout 上驗證。於 Dual-Arm UR-5e 20 項任務上全面勝過所有 baseline（如 DUR-FindTapeBasket 任務 XR-1 達 85% vs. π0 的 50%）；在預訓練階段完全未見過的 Tien Kung 2.0（20 項任務的嚴格具身遷移測試）上，XR-1 平均成功率達 72.0%，遠超 π0.5（41.0%）、π0（40.8%）、GR00T-N1.5（38.0%）、UniVLA（17.8%）、RDT（17.0%）。消融實驗（Table 3）顯示：僅用視覺分支或僅用動作分支的 UVMC 均劣於完整雙分支版本，且移除 KL 對齊損失、移除大規模預訓練（DT-only）或使用人類影片資料（Ego4D）比例遞減，皆導致成功率顯著下降，驗證了雙模態聯合編碼、跨資料源對齊與規模化預訓練三者缺一不可。

**Result 是否公正**：論文提供了完整消融實驗（Table 3）與跨具身遷移的嚴格測試（Tien Kung 2.0 在預訓練階段完全未見過），並公開了逐任務成功率數字（非僅平均值），透明度較高；同時已通過 ICML 2026 同行評審（並獲選 Oral，代表審稿人認可其實驗嚴謹度與貢獻度）。惟其評測平台與任務設計皆由作者自訂，尚待第三方獨立復現於其他機構的機器人平台上。

### Limitation

**已知的 limitation**：論文本文（含附錄）並未設立獨立的「Limitations」章節具體討論方法侷限；從方法設計反推，UVMC 依賴大規模異質資料（RoboMIND、Open-X、XR-D、Ego4D）進行自監督預訓練，其資料規模與品質要求可能對資源較少的研究團隊構成門檻；此外，離散 codebook 的容量與粒度如何影響精細操作（如高精度插入、力控任務）的表現，論文未見系統性分析。

**從 result 來看的弱項**：消融實驗顯示資料規模化（DT 10% vs. 100% vs. 加入 XR-D）對成功率影響顯著（Table 3 中 29.2%→65.0%→81.6%），意味著 XR-1 的性能高度仰賴大規模預訓練資料的取得，對資料稀缺場景的適用性仍待驗證；且真實機器人評測皆由人類評分 20 次 rollout，樣本量偏小，統計置信度有限。

### Related work

與本頁「World Models Integration」子主題中已收錄的 GR00T N1（本頁基礎模型）、π0/π0.5/π0.7（本頁基礎模型/參考模型）構成直接效能比較基準，XR-1 論文即以此四者及 RDT、UniVLA 為主要 baseline；其「離散化中介表示對齊跨模態動態」的設計理念，與本頁「Memory, History-Awareness & Long-Horizon Control」子主題下 MemoryVLA++ 的「world-model imagination 注入去噪 latent space」有方法論上的呼應之處，皆試圖以額外的中介表示提升動作生成品質，值得後續交叉比對兩種路線在長 horizon 任務上的優劣。

值得 survey 的程度：高。UVMC 提出的「雙分支 VQ-VAE + 共享 codebook 對齊」範式為本頁尚未收錄的具體技術路線，且已獲 ICML 2026 Oral 認可，來自與本頁 τ0-VLA、GE-Act 2.0、ACoT-VLA 同源的 Beijing Innovation Center of Humanoid Robotics（X-Humanoid），顯示該機構在 VLA 表示學習面向的持續投入，值得追蹤其後續模型迭代。

### Conclusion

**綜合評價**：XR-1 提出了一個概念清晰且經過大規模真實機器人驗證的跨具身 VLA 框架，UVMC 的雙模態聯合離散表示學習是具體的架構創新而非既有技巧的組合，且獲 ICML 2026 Oral 肯定，是本頁「Architecture Paradigms」與「World Models Integration」跨主題下值得記錄的重要進展。

**與其他重要文章的關係**：XR-1 與本頁基礎模型 GR00T N1、π0 系列構成直接效能比較對象，並與 Beijing Innovation Center of Humanoid Robotics（X-Humanoid）同源的 τ0-VLA、GE-Act 2.0、ACoT-VLA 共享機構脈絡，顯示該團隊正從「階層式規劃」（τ0-VLA）、「動作空間 CoT」（ACoT-VLA）、「從零訓練 WAM」（GE-Act 2.0）延伸至「統一視覺-動作離散表示」（XR-1）等多條技術路線同時推進 VLA 研究。ROCm/AMD 待補強：UVMC 雙分支 VQ-VAE 的訓練涉及大量離散化 codebook 查表與跨模態對齊損失計算，這類「VQ-VAE + 跨模態對齊」的訓練管線在 ROCm 上的算子支援與效能調校（尤其向量量化查表操作的 kernel 最佳化）目前公開基準有限，是 AMD 在此類跨模態表示學習訓練基礎設施上可切入的方向。
