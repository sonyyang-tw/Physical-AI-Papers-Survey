---
layout: paper
title: "DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos"
section: wm
page_id: "1955665089"
permalink: /Physical-AI-Papers-Survey/wm/dreamdojo-a-generalist-robot-world-model-from-large-scale-human-videos-1955665089/
---

### Abstract

模擬各種環境下動作結果的能力，將徹底改變大規模通用智能體的開發方式。然而，建模這類世界動態——尤其是針對靈巧機器人任務——因資料覆蓋有限與動作標籤稀缺而面臨重大挑戰。作為朝此方向的一項努力，本文提出 DreamDojo，一個從 44,000 小時第一人稱人類影片中學習多樣互動與靈巧控制的基礎 world model。作者的資料組合是目前為止規模最大的 world model 預訓練影片資料集，涵蓋廣泛的日常場景、多樣物件與技能。為解決動作標籤稀缺問題，作者引入連續潛在動作（continuous latent actions）作為統一的代理動作，強化從無標籤影片中遷移互動知識的能力。在小規模目標機器人資料上完成後訓練（post-training）後，DreamDojo 展現出強大的物理理解與精確的動作可控性。作者也設計了一套蒸餾管線，將 DreamDojo 加速至每秒 10.81 幀的即時速度，並進一步改善上下文一致性。此工作使基於生成式 world model 的多項重要應用成為可能，包括即時遠端操作（live teleoperation）、策略評估與模型式規劃。在多個具挑戰性的分布外（OOD）benchmark 上的系統性評測，驗證了此方法對模擬開放世界、接觸豐富（contact-rich）任務的重要性，為通用機器人 world model 鋪路。

### Method

**要解決的問題** ：現有機器人 world model 高度依賴機器人自身收集的示範資料，這類資料規模有限、場景多樣性不足，難以支撐開放世界、接觸豐富任務的物理動態建模；同時，人類第一人稱影片雖然規模龐大且場景多樣，卻普遍缺乏可直接用於訓練的動作標籤，如何有效利用這類無標籤（或弱標籤）人類資料來訓練 world model，是尚未被充分解決的問題。

**Main method** ：DreamDojo 是一個基礎 world model，在迄今規模最大的 world model 預訓練資料集——44,000 小時第一人稱人類影片（DreamDojo-HV，涵蓋約為現有最多樣公開機器人學習資料集 96 倍的場景數）上訓練。為克服動作標籤稀缺的問題，作者提出「連續潛在動作」作為統一的代理動作表示，讓模型能從大量無動作標籤的影片中學習可遷移的互動知識。在小規模目標機器人資料上完成後訓練後，模型展現精確的動作可控性與強物理理解力；作者進一步設計蒸餾管線，將模型加速到 10.81 FPS 的即時速度，同時提升長 rollout 下的上下文一致性。

**和以往方式的差異** ：與過去侷限於機器人自身資料規模的 world model 不同，DreamDojo 首次系統性地將「人類第一人稱影片」規模化到 44K 小時這一數量級，並用連續潛在動作機制解決了「人類影片無動作標籤」這一長期障礙，使得從人類日常行為中遷移互動知識、physics 理解成為可能；這與同團隊 EgoScale（arXiv:2602.16710，本次同時推送至 VLA Papers 頁面）在 policy 學習端的路線形成呼應，但 DreamDojo 專注於「預測」而非「直接生成動作」，補全了 world model 這一側的資料規模化路徑。

**關鍵方法圖** ： ![Figure](/Physical-AI-Papers-Survey/assets/images/1955665089_dreamdojo_overview.png) 展示 DreamDojo 整體流程：從 44K 小時人類第一人稱影片出發，經連續潛在動作提取與預訓練，到後訓練對齊機器人具身，最終支援遠端操作、策略評估、模型式規劃等下游應用。 ![Figure](/Physical-AI-Papers-Survey/assets/images/1955665089_dreamdojo_benchmark.png) 展示在多個分布外（OOD）benchmark 上的系統性評測結果，驗證模型模擬開放世界、接觸豐富任務的能力。

### Result

**Result 結果如何，主要增強了哪些部分** ：DreamDojo 在多個具挑戰性的 OOD benchmark 上驗證了其模擬開放世界、接觸豐富任務的能力；蒸餾後模型達到 10.81 FPS 的即時推論速度，且上下文一致性同步提升，使得即時遠端操作、策略評估等原本因延遲而難以實現的應用成為可行。作者的資料集規模與場景多樣性（44K 小時，約 96 倍於現有最多樣機器人資料集）本身即是一項重要貢獻，超越了單純的模型效能提升。

**Result 是否公正，其他論文提出的結果有沒有和這篇論文 result 不符** ：論文作者陣容龐大且橫跨 NVIDIA GEAR、UC Berkeley（Jitendra Malik、Pieter Abbeel）等知名研究者，屬嚴謹學術產出；由於評測涉及大量自建 OOD benchmark 與人類偏好評估（human preference evaluation），量化結果的絕對可比性依賴其評測設計，目前尚未見獨立第三方對其物理理解與可控性數字提出質疑或反例，但由於資料集與 benchmark 均未完全公開細節，外部復現與交叉驗證仍有限。

### Limitation

**有沒有已知的 limitation** ：作者的評測方法之一是人類偏好評估，這類評估天然帶有主觀性與評分者偏差，量化嚴謹度不如客觀物理指標；此外，模型仍需在「小規模目標機器人資料」上完成後訓練才能具備精確可控性，說明純粹依賴人類影片預訓練尚不足以直接支撐機器人部署，人類到機器人的「域落差」（domain gap）依然存在。

**從 result 來看 limitation 和弱項是甚麼** ：即便蒸餾後達到 10.81 FPS，這一速度相較輕量 VLA policy（通常可達數十甚至上百 Hz）仍然偏低，作為即時規劃或 policy-in-the-loop 使用時的延遲瓶頸依然存在；此外，連續潛在動作作為代理動作的準確性上限，仍受限於從影片中估計人類動作的姿態估計誤差，這類誤差在論文中未見充分的定量分析。

### Related work

**arXiv 上有沒有更新的 related work** ：與本文緊密相關且幾乎同期發表的是同團隊（NVIDIA GEAR，作者高度重疊：Yuke Zhu、Linxi "Jim" Fan、Ruijie Zheng 等）的 EgoScale（arXiv:2602.16710，本次同時推送至 VLA Papers 頁面），該文利用同一批 44K 小時規模量級的第一人稱人類資料直接訓練 VLA policy，並驗證了資料規模與驗證損失間的對數線性 scaling law。兩篇論文共享資料採集與處理基礎設施，分別攻克 world model（DreamDojo）與 policy（EgoScale）兩端，建議一併閱讀。

**判斷 related work 值得 survey 的程度** ：高度值得。這兩篇論文（DreamDojo + EgoScale）共同標誌著 NVIDIA GEAR 在「大規模人類第一人稱資料驅動具身智能」這一研究方向上的系統性投入，對理解 2026 年 world model / VLA 資料規模化的最新趨勢具有指標意義。

### Conclusion

**給這篇文章綜合評價，值不值得參考** ：值得參考。DreamDojo 建立了迄今規模最大的人類影片 world model 預訓練資料集，並提出連續潛在動作這一簡潔有效的機制解決動作標籤稀缺問題，其蒸餾管線使即時應用（遠端操作、policy 評估）成為可行，是 world model 資料規模化與工程落地並重的代表性工作。

**做出跟其他重要文章的關係相依圖，並判斷 ROCm/AMD 在此領域上尚待補強的部分** ：關係上，DreamDojo 與 GAIA-1/GAIA-2（Wayve，自駕 world model）、Genie 3（DeepMind）、Cosmos（NVIDIA）同屬「大規模生成式 world model」譜系，但 DreamDojo 的獨特定位是「以人類第一人稱影片而非機器人/駕駛資料」作為預訓練來源；與同團隊 EgoScale 構成資料規模化的 world model / policy 雙引擎，也與 GR00T N1.7（結合 Cosmos world model 的人形基礎模型）形成技術棧上的呼應。ROCm/AMD 在此領域尚待補強之處：(1) 缺乏針對「影片擴散 + 潛在動作聯合建模」這類大規模多模態訓練負載的 ROCm 效能基準與最佳化算子（目前此類工作高度依賴 NVIDIA CUDA/Cosmos 生態）；(2) 缺乏支援大規模影片資料蒸餾管線（如本文的即時化蒸餾）在 ROCm 硬體上的參考實作與延遲基準，AMD 可考慮優先投入此類「影片 world model 推論加速」的驗證與最佳化，作為切入具身智能基礎設施市場的著力點。