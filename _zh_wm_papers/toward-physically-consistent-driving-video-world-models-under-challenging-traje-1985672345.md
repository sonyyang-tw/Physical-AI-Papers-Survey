---
layout: paper
title: "Toward Physically Consistent Driving Video World Models under Challenging Trajectories"
section: wm
page_id: "1985672345"
permalink: /zh/wm/toward-physically-consistent-driving-video-world-models-under-challenging-traje-1985672345/
---

### Abstract

影片生成模型已展現作為自駕模擬 world model 的強大潛力，但現有方法主要以真實世界駕駛資料集訓練，這些資料集多半僅含自然、安全的駕駛情境；因此當模型被要求以具挑戰性或反事實的軌跡（例如模擬器或規劃系統產生的不完美軌跡）作為條件時，現有模型常常失效，產生嚴重物理不一致與視覺偽影。為解決此限制，本文提出 PhyGenesis，一個能生成高視覺保真度、且具強物理一致性駕駛影片的 world model。其框架包含兩個核心元件：(1) 物理條件生成器（Physical Condition Generator），將可能無效的軌跡輸入轉換為物理上合理的條件；(2) 物理增強影片生成器（Physics-enhanced Video Generator），在這些條件下產出高保真多視角駕駛影片。為有效訓練這兩個元件，作者建構了一個大規模、物理內容豐富的異質資料集：除真實世界駕駛影片外，還以 CARLA 模擬器生成多樣的具挑戰性駕駛情境，並從中萃取監督訊號，引導模型在極端條件下學習物理紮根的動態。此「具挑戰性軌跡學習」策略使模型能進行軌跡修正並促進物理一致的影片生成。大量實驗證明，PhyGenesis 在具挑戰性軌跡上尤其大幅超越現有 state-of-the-art 方法。作者群來自浙江大學、小米汽車（Xiaomi EV）、香港理工大學與深圳灣實驗室（Shenzhen Loop Area Institute）聯合團隊。

### Method

- **要解決的問題**：現有自駕影片 world model 在部署於具挑戰性軌跡條件（由模擬器、規劃系統或使用者互動產生）時普遍失效，作者歸納出兩項根本限制：其一，現有模型缺乏對「軌跡可行性」的物理感知——模擬器或規劃器產生的軌跡條件可能不完美、違反基本物理限制，但既有模型缺乏顯式物理推理能力，本質上僅是「條件到像素」的翻譯器，被迫遵循物理不一致輸入時常產生嚴重渲染偽影與結構性失敗；其二，現有模型缺乏物理一致的生成能力——多數既有方法主要以安全、常態行為為主的真實世界資料訓練，即便輸入軌跡本身物理可行，仍難以生成碰撞、偏離道路等罕見情境下的真實動態。

- **Main method**：PhyGenesis 的核心洞見是「物理一致的世界建模需要同時處理軌跡可行性與物理一致影片生成」。物理條件生成器（Physical Condition Generator）將任意軌跡條件轉換為物理上合理的 6 自由度（6-DoF）車輛運動：作者設計了一套新穎的「反事實軌跡修正」（counterfactual trajectory rectification）訓練任務，賦予模型解決物理違反軌跡所需的內在物理先驗——具體做法是保留碰撞前軌跡不變，並以各代理碰撞前的速度外推碰撞後的運動，構造反事實的物理違反條件供模型學習修正。修正後的條件接著輸入物理增強影片生成器（Physics-Enhanced Video Generator），此生成器以 WAN2.1 預訓練權重初始化，並以透視視角（PV）特徵（透過 ResNet50 萃取）搭配兩階段訓練排程（先在較低解析度以較大批次訓練，再於較高解析度以較小批次微調）產出高保真多視角駕駛影片。為支援此學習過程，作者建構了結合真實世界駕駛資料與 CARLA 模擬生成的物理挑戰資料集（CARLA Ego、CARLA ADV）的異質訓練集：真實資料提供豐富的常態駕駛行為，CARLA 生成資料則引入碰撞、偏離道路等多樣極端情境，為學習複雜物件-環境互動提供在真實常態駕駛資料中極為稀缺的密集監督訊號。

- **和以往方式的差異**：與既有僅將結構化條件（如車道線、BEV 地圖）當作「條件到像素」翻譯任務的自駕 world model（如 MagicDrive-V2、UniMLVG、DiST-4D）不同，PhyGenesis 是首個能明確處理軌跡可行性、並在初始輸入為物理違反軌跡時仍能合成物理一致多視角駕駛影片的框架；其關鍵區隔在於顯式的物理條件修正模組，而非僅依賴訓練資料本身的物理分佈去隱式學習物理規律——這使其能同時處理「輸入軌跡本身不合理」與「場景需呈現罕見物理事件」兩類挑戰，而既有方法通常只能處理其中一種。

- **關鍵方法圖**：見下方嵌入圖片——Figure 1（teaser）展示既有方法（如 DiST-4D）在物理違反軌跡條件下產生嚴重偽影與結構性失敗，PhyGenesis 則能維持物理一致性；另一張圖展示 PhyGenesis 整體框架，包含物理條件生成器與物理增強影片生成器兩大模組如何串接。

![Figure]({{ site.baseurl }}/assets/images/2603.24506_teaser.png)

_Figure 1: PhyGenesis 概覽——既有方法在物理違反軌跡下產生嚴重偽影，PhyGenesis 藉由物理條件生成器與物理增強影片生成器維持物理一致性_

![Figure]({{ site.baseurl }}/assets/images/2603.24506_framework.png)

_Figure 2: PhyGenesis 框架架構——物理條件生成器將軌跡輸入修正為物理合理條件，再由物理增強影片生成器產出高保真多視角駕駛影片_

### Result

- **主要增強部分**：在 nuScenes（常態軌跡）、CARLA Ego 與 CARLA ADV（物理違反軌跡）三個資料集上，PhyGenesis 在視覺品質（FID/FVD）、物理一致性（PHY，取自 WorldModelBench 四項指標平均：Mass、Impenetrability、Frame-wise Quality、Temporal Quality）與人類偏好率（Pref.）上全面優於 UniMLVG、MagicDrive-V2、DiST-4D 三個基線。具體數據：nuScenes 上 FID 10.24／FVD 40.41／PHY 0.97／Pref. 0.67（次佳的 DiST-4D 為 FID 10.49／FVD 46.95／PHY 0.86／Pref. 0.13）；在物理最具挑戰性的 CARLA ADV 上差距更為顯著，PhyGenesis 達 FID 9.28／FVD 77.83／PHY 0.87／Pref. 0.66，而 DiST-4D 僅 FID 16.07／FVD 128.88／PHY 0.56／Pref. 0.05，顯示既有方法在物理違反軌跡下的表現明顯崩壞，PhyGenesis 則維持穩健。消融實驗證實，加入 CARLA 物理豐富資料進行異質訓練後，CARLA ADV 上的 FVD 從 89.83 降至 77.83（約 13.4% 相對改善），人類偏好率從 0.13 大幅提升至 0.53，且定性上訓練於單純 nuScenes 常態資料時，模型在具挑戰性互動中容易出現車輛變形，異質協同訓練後畫面明顯更銳利、物理動態更連貫。

- **結果是否公正**：作者採用三重評估維度（視覺品質、物理合理性、可控性）並輔以人類偏好研究，而非僅依賴單一自動化指標，且對三個基線方法均在相同資料集與相同評估協議下重新評測（並針對 DiST-4D 額外提供深度圖輸入以確保公平比較），方法論設計嚴謹。物理合理性指標採用第三方 WorldModelBench 的 VLM 對齊人類偏好評判標準，而非自建指標，增加結果可信度。消融實驗清楚拆解了「異質訓練資料」這一項設計選擇的獨立貢獻，佐證核心論點並非僅憑主觀論述。

- **Limitation**：論文正文與可得摘要內容中未見獨立的作者自陳 Limitation 段落，需查閱附錄以確認更細節的限制討論。從方法設計可推論的潛在弱項：CARLA 模擬生成資料與真實 nuScenes 資料之間仍存在視覺風格落差，論文透過一個額外訓練的風格轉換模型將 CARLA 片段轉換為 nuScenes 視覺風格以求公平比較，這一額外轉換步驟本身可能引入误差來源；此外，反事實軌跡修正的訓練任務目前聚焦於碰撞與偏離道路兩類事件，能否涵蓋更廣泛的物理違反情境（如側滑、爆胎等）仍待驗證，且模型的物理先驗終究來自於訓練資料涵蓋的具體事件類型，面對訓練分佈之外的全新物理現象時的泛化能力尚不明朗。

### Related work

- PhyGenesis 與本頁已收錄的自駕 world model 基礎模型（GAIA-1、GAIA-2）及既有結構化條件生成方法（BEVGen、BEVControl、MagicDrive、MagicDrive-V2）一脈相承，並直接與 DiST-4D、WorldSplat 等引入度量深度做 4D 場景提升的方法比較；在物理挑戰資料構造上，與先前 ReSim（同樣嘗試引入合成資料以彌補真實資料分佈覆蓋不足）形成對照，但 ReSim 僅限單視角、僅有 ego 軌跡標註，PhyGenesis 的 CARLA 生成資料則涵蓋多視角與多代理標註，能訓練控制多個代理的模型。
- 判斷值得 survey 的程度：中高。PhyGenesis 首次系統性地將「軌跡可行性物理推理」與「物理一致影片生成」整合為單一框架，並以真實與模擬混合資料驗證其在極端物理情境下的優勢，對本頁「World Models for Autonomous Driving」主題下正需要驗證長尾安全情境的既有基礎模型（GAIA 系列、Waymo World Model 等）皆有直接參考價值，適合對照閱讀。

### Conclusion

- **綜合評價**：PhyGenesis 針對自駕 world model 在具挑戰性軌跡下表現失真的問題提出了具體、可驗證的解法，其「物理條件生成器 + 物理增強影片生成器」雙模組設計思路清晰，並透過真實與 CARLA 混合資料的異質訓練策略提供了實質效能提升，尤其在最具挑戰性的物理違反情境下優勢最為明顯，為自駕安全測試與長尾情境模擬提供了更可靠的建構模塊。

- **與其他重要文章的關係**：PhyGenesis 與本頁已收錄的 GAIA-1、GAIA-2（Wayve）等自駕生成式 world model 基礎模型同屬「以生成式影片模型模擬自駕場景」譜系，但更聚焦於「物理違反軌跡下的穩健性」這一此前較少被系統性處理的子問題，與同頁 NVIDIA OmniDreams 強調的「即時閉環模擬」形成互補——OmniDreams 著重推論速度與閉環互動性，PhyGenesis 則著重極端物理情境下的生成正確性，兩者代表自駕 world model 演進的不同面向。ROCm/AMD 在此領域尚待補強之處：PhyGenesis 的影片生成骨幹以 WAN2.1 擴散模型為基礎，訓練於 48 張 NVIDIA H20 GPU 之上，且高度依賴 CARLA 模擬器（其本身仰賴 NVIDIA GPU 加速的即時渲染管線）產生訓練資料；若 AMD 欲切入自駕 world model 訓練與模擬基礎設施市場，驗證 ROCm 上大規模擴散影片模型訓練（含兩階段解析度排程）與 CARLA 類模擬器的相容性，將是值得評估的技術方向。
