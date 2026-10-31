---
layout: paper
title: "RynnWorld-Latent: A Cross-Embodiment World Model Conditioned on Universal Latent Actions"
section: wm
page_id: "2610367910"
permalink: /zh/wm/rynnworld-latent-a-cross-embodiment-world-model-conditioned-on-universal-2610367910/
---

### Abstract

從異質互動影片中學習可控的世界動態極具挑戰:不同機器人具身使用互不相容的動作空間,而人類影片又缺乏原生控制標籤。本論文提出 RynnWorld-Latent,一套 cross-embodiment 影片 world model,使用姊妹論文 RynnVLA-Latent 中提出的 RynnLAM 3D 接地 latent action 作為共享條件介面。此一表示使得在人類互動影片、機器人示範、模擬 rollout 上進行聯合預訓練成為可能,而不需要求其原生動作空間彼此對齊。RynnWorld-Latent 建構於預訓練影片 transformer 之上,結合全域 action token 與恆等初始化(identity-initialized)的局部條件路徑,將動作與未來影片 latent 對齊。作者在 23 個資料集、約 5.535 億影格上進行預訓練,並透過後訓練將模型適配至目標機器人。此框架支援兩種資料生成路線:數位遙操作(digital teleoperation)使用目標機器人指令生成動作-影片示範資料;latent action 合成則將來源動作轉移至經編輯的初始影格,並與重新定位後的偽機器人動作配對。實驗顯示在公開 benchmark 與兩個真實機器人平台上均提升了影片預測指標,並在定性比較中展示當不同動作序列共享同一初始觀測時模型能忠實跟隨指定動作。合成資料 mid-training 提升了 LIBERO 與 LIBERO-Plus 上的 policy 成功率,兩種生成路線也都在評測場景中提升了真實世界 policy 成功率。論文於 2026 年 10 月 27 日發佈於 arXiv,作者團隊來自 DAMO Academy(阿里巴巴集團)、Hupan Lab、Hong Kong Embodied AI Lab 與 CUHK,與同日收錄的姊妹論文 RynnVLA-Latent(見 VLA 頁面)共享同一組作者與核心技術基礎。

### Method

- **要解決的問題**:語言條件式影片生成器應用於機器人操作時面臨介面不匹配問題——其主要控制訊號是任務層級描述,而物理互動實際上是由連續、逐影格的因果介入所主導。「撿起杯子」這類指令只指定任務結果,並未決定達成結果的精確軌跡;在接觸豐富的操作中,時機、接觸順序、夾爪狀態、相機運動的細微差異即可導致截然不同的未來。若直接以原生機器人動作作為條件,又會面臨嚴重的對齊瓶頸:不同具身的運動學空間、關節數、座標慣例、控制頻率、硬體限制彼此互異,難以跨平台規模化。

- **Main method**:作者主張 latent action 提供了這樣的共享介面——與其將動作表示為機器人指令,latent action 描述的是「觀測之間發生了什麼變化」。RynnWorld-Latent 建構於 Cosmos3-Edge(Mixture-of-Transformers 影片基礎模型)之上,使用凍結的 RynnLAM 編碼器產生的 latent action 描述子作為條件,結合全域 action token 與恆等初始化、逐影格對齊的局部條件路徑,利用 latent action 抽取與影片 latent 壓縮之間的時間對應關係,讓每個動作描述子條件化其對應的未來影片 latent。此設計使模型能在人類、機器人、模擬影片上進行聯合預訓練,完全不需要求其原生動作空間對齊。作者進一步將 RynnWorld-Latent 定位為「資料生成引擎」而非僅是未來預測器,支援兩種互補的生成模式:數位遙操作(後訓練後以目標機器人動作為條件,將操作者控制訊號映射至目標動作並驅動影片生成,產出配對的動作-影片資料而無需額外真實機器人執行)與 latent action 合成(從來源影片萃取 latent action 序列,編輯初始影格以替換具身或環境,並以編輯後的初始影格與原始 latent action 序列生成新的 rollout)。

- **和以往方式的差異**:既有 action-conditioned world model 多半需要將機器人原生動作直接編碼進條件訊號,因而難以跨越異質具身規模化;本論文與姊妹論文 RynnVLA-Latent 共同提出的 latent action 介面則讓「監督目標」(RynnVLA-Latent 用於 policy 預訓練)與「生成條件」(RynnWorld-Latent 用於可控影片生成)共用同一組凍結描述子,是目前同類研究中少見地將 latent action 同時用於 policy 學習與 world model 條件化兩端的系統性嘗試。相較於單純將 world model 視為未來預測器或政策評測工具的既有研究(如 WoVR、Interactive World Simulator),RynnWorld-Latent 明確定位為「資料生成引擎」,透過數位遙操作與 latent action 合成兩條路線主動產出可用於下游策略訓練的資料,而非僅被動提供 rollout 評測。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示預訓練語料庫概覽,涵蓋 23 個資料集、約 6,190 小時、257 萬個 episode 的人類、真實機器人、模擬影片分布;第二張圖展示資料生成引擎的兩條路線,呈現數位遙操作與 latent action 合成如何分別從目標機器人指令與來源影片的 latent action 序列生成配對的動作-影片訓練資料。

![Figure]({{ site.baseurl }}/assets/images/2610.36791_rynnworld_overview.png)

_Figure 1: RynnWorld-Latent 預訓練語料庫概覽——23 個資料集,約 6,190 小時、257 萬個 episode,涵蓋人類、真實機器人、模擬影片_

![Figure]({{ site.baseurl }}/assets/images/2610.36791_rynnworld_dataengine.png)

_Figure 2: RynnWorld-Latent 資料生成引擎——數位遙操作與 latent action 合成兩條路線,產出可用於下游 policy 訓練的配對動作-影片資料_

### Result

- **主要增強部分**:在模擬 benchmark 上,合成資料 mid-training 將 π₀ 從 94.4% 提升至 96.1%(LIBERO)、從 53.6% 提升至 79.4%(LIBERO-Plus);π₀.₅ 則從 96.9% 提升至 97.8%(LIBERO)、從 84.4% 提升至 84.8%(LIBERO-Plus),顯示增益在 π₀ 上更為顯著。在真實世界任務中,數位遙操作資料為兩個 backbone 在全部四項任務上均帶來成功率提升,例如 π₀.₅ 的 Plate-Placement 從 82.86% 提升至 91.43%、Steak-Serving 從 40.00% 提升至 54.29%;以 RynnWorld-Latent-80M 進行合成資料 mid-training 後,π₀.₅ 的 Steak-Serving 自 40.00% 升至 60.00%、Plate-Retrieval 自 45.71% 升至 68.57%。在 Marvin-WUJI 平台上,Real + Digital Teleop 設定甚至優於 Real + RynnWorld-Teleop 約 5.71 與 8.57 個百分點(Plate-Placement 與 Plate-Wiping),對應兩筆與三筆額外成功試驗。

- **結果是否公正**:論文在 DreamDojo GR-1 評測集、LIBERO/LIBERO-Plus 模擬 benchmark,以及 Marvin-WUJI(靜態雙臂靈巧手)與 Astribot-S1(輪式移動雙臂夾爪)兩個真實機器人平台上進行多層次驗證,並明確說明每項真實世界結果僅基於 35 次試驗,作者也主動指出這些應被視為「觀察到的改善」而非具統計顯著性的結論,同時坦承實驗未能將合成資料品質與合成資料數量、額外訓練運算量的差異完全隔離,顯示作者對結果的保守詮釋與方法透明度。

### Limitation

- **已知 limitation**:論文明確指出,latent action 是從觀測到的視覺轉變中推斷而來,可能同時編碼相機運動或外觀資訊,因此定性動作跟隨與基於影像的預測指標並不足以確立因果可識別性或物理正確性。在合成管線中,重新定位的機器人指令與生成觀測是透過各自獨立的流程取得,時間對齊與篩選機制無法保證兩者的物理一致性。真實世界成功率數字僅基於每任務 35 次試驗,細微差異的詮釋應保持謹慎。此外,合成 mid-training 同時增加了資料量與優化運算量,現有比較並未將兩者的貢獻拆分開來。

- **從 result 來看的弱項**:Real + Digital Teleop 在 Marvin-WUJI 平台上部分任務甚至優於使用 RynnWorld 生成資料的設定,顯示目前的合成資料生成品質在某些具身/任務組合下仍未能完全取代直接的遙操作資料收集,「世界模型生成資料優於真實資料增強」這一假設在具體任務層級上並非普遍成立,需要依任務特性審慎評估兩種路線的相對效益。

### Related work

- RynnWorld-Latent 與本頁「Robot-Specific Action-Conditioned World Models」主題下已收錄的多篇論文(如 DreamDojo、GeniWorld、WorldSync)同屬「讓 world model 與機器人動作空間耦合」這一方向,但切入點不同:DreamDojo 以連續潛在動作作為代理動作機制在大規模人類影片上預訓練,GeniWorld 以 URDF 渲染視覺動作取代數值動作條件化以解耦具身運動學,WorldSync 聚焦於診斷與對齊 action-conditioned 生成的忠實度;RynnWorld-Latent 的獨特貢獻在於將同一套 3D 接地 latent action 描述子(RynnLAM)同時用於姊妹論文 RynnVLA-Latent 的 policy 預訓練監督與本論文的 world model 條件化,並明確以「資料生成引擎」定位支援數位遙操作與 latent action 合成兩條資料生成路線。
- 與本頁 VLA 頁面第 7 類「World Models Integration」中收錄的多篇 WAM(World Action Model)論文相比,RynnWorld-Latent 更聚焦於「預測/模擬優先」的影片生成,而非「動作生成優先」的整合研究,與姊妹論文 RynnVLA-Latent 共同構成同一技術基礎(RynnLAM)在兩個不同應用方向(policy 學習監督 vs. 可控影片生成與資料合成)的互補實現。
- 判斷值得 survey 的程度:高。RynnWorld-Latent 出自 DAMO Academy(阿里巴巴集團)等大型產業實驗室,在 23 個資料集、約 5.535 億影格的規模上進行預訓練,並在兩個真實機器人平台上完成驗證,其「latent action 作為資料生成引擎」的定位為降低機器人學習資料收集成本提供了具體且經過真實世界驗證的新思路。

### Conclusion

- **綜合評價**:RynnWorld-Latent 針對「如何在不要求原生動作空間對齊的前提下,利用異質具身互動影片學習可控視覺動態」這一問題,提出以 3D 接地 latent action 作為共享條件介面的解法,並透過數位遙操作與 latent action 合成兩條資料生成路線,將 world model 的角色從單純的未來預測器擴展為可規模化的機器人資料生成引擎。其與姊妹論文 RynnVLA-Latent 共用同一套 latent action 基礎設施,呈現出一條從「影片監督訊號」到「policy 預訓練」再到「可控資料生成」的完整技術路徑。

- **與其他重要文章的關係**:RynnWorld-Latent 可與本頁「World Models as Data Engines / Simulators for Robot Learning」主題下聚焦合成訓練資料的論文(如 MimicGen、Dreamitate)互補對照——後者透過傳統示範增強或影片生成學習視覺運動 policy,RynnWorld-Latent 則以跨具身 latent action 條件化作為核心機制,系統性支援數位遙操作與來源動作遷移兩種資料生成模式。ROCm/AMD 在此領域尚待補強之處:論文訓練管線採用 hybrid-sharded FSDP(每節點 shard degree 8、跨節點 replication degree 4)搭配 bf16 訓練與 power-function EMA,此類大規模影片 transformer 預訓練與多資料集聯合訓練的工作負載對記憶體頻寬與分散式訓練框架相容性要求極高;隨著「latent action 條件化世界模型作為資料生成引擎」逐漸成為業界擴展機器人訓練資料的標準手法,驗證此類 FSDP 混合分片訓練范式與大規模影片 VAE/diffusion transformer 推論管線在 ROCm 軟體棧上的效能與相容性,將是具體且具產業急迫性的生態系拓展方向。
