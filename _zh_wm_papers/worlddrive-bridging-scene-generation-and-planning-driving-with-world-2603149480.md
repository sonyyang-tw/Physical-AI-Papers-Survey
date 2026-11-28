---
layout: paper
title: "Bridging Scene Generation and Planning: Driving with World Model via Unifying Vision and Motion Representation (WorldDrive)"
section: wm
page_id: "2603149480"
permalink: /zh/wm/worlddrive-bridging-scene-generation-and-planning-driving-with-world-2603149480/
---

### Abstract

端到端自動駕駛的目標是從原始感測器輸入直接產生安全且合理的規劃決策,而建構有效的場景表徵是其中的核心挑戰。Driving World Model(DWM)透過預測駕駛場景的未來演變,展現出學習豐富表徵的強大潛力,然而既有 DWM 主要聚焦於視覺場景表徵,動作(motion)表徵並未被明確設計為可被規劃器共享與繼承,導致場景生成的最佳化目標與精確動作規劃的需求之間存在根本性的斷層。作者提出 WorldDrive,一套透過統一視覺與動作表徵,將場景生成與即時規劃耦合為一體的整體框架。首先提出 Trajectory-aware Driving World Model(TA-DWM),以軌跡詞彙表(trajectory vocabulary)為條件,強制視覺動態與動作意圖之間的一致性,使模型能依據特定軌跡生成多樣且合理的未來場景;接著將 TA-DWM 學得的視覺與動作編碼器直接遷移至下游的 Multi-modal Planner,確保駕駛策略運作在由場景生成任務預先最佳化、成熟一致的潛在空間上。進一步地,為善用 world model 的前瞻能力,作者提出 Future-aware Rewarder(FAR),從凍結的 world model 中蒸餾未來潛在表徵,以即時評估並挑選最佳軌跡。大量實驗顯示 WorldDrive 在純視覺方法中取得領先的規劃表現,同時維持高保真度的動作可控影片生成能力。論文已於 2026 年 11 月 17 日修訂至 v2 並確認獲 NeurIPS 2026 接受,作者團隊來自澳門大學 SKL-IOTSC 人工智慧系、Afari Intelligent Drive 與山東大學。

### Method

- **要解決的問題**:現有將 driving world model 整合進規劃系統的策略大致分兩類,各有缺陷:第一類以高保真模型為下游規劃器生成未來場景(如 Drive-WM、FSDrive),但此過程運算成本極高昂,難以即時部署;第二類完全在潛在空間內運作的 latent world model(如 LAW、World4Drive),雖效率較高,卻犧牲了可解釋的場景模擬能力,也限制了對安全攸關決策而言珍貴的顯式視覺驗證。更根本的是,作者指出這兩種策略都存在「表徵錯位與任務斷裂」的系統性限制:場景模擬器通常針對感知重建最佳化、強調視覺表徵,而規劃器則獨立訓練以回歸動作、編碼動作表徵;缺乏一個在場景生成與規劃任務間共享且一致的統一表徵,使規劃器無法充分利用生成式 driving world model 所學得的動態與動作先驗。

- **Main method**:WorldDrive 的核心哲學是「表徵統一」——主張透過未來生成(場景生成)學得的表徵,應能直接被規劃器重複利用來決定未來(規劃)。具體而言,首先提出 Trajectory-aware Driving World Model(TA-DWM),不同於既有工作將動作僅視為表層條件,TA-DWM 採用建立於預先定義軌跡錨點(以 K-means 分群建構、256 個軌跡錨點)之上的多模態軌跡編碼方案,構建出視覺動態與動作意圖內在耦合的結構化潛在空間,此設計使「表徵繼承」成為可能:TA-DWM 學得的穩健視覺與動作編碼器可直接遷移用於初始化下游規劃器,確保規劃器運作在由未來場景生成任務預先對齊的成熟一致潛在空間中。基於此統一表徵,作者設計了一個輕量化的 Multi-modal Planner,利用這些凍結的編碼器,以查詢中心的交叉注意力機制高效融合視覺情境與動作先驗,產生多樣且高品質的候選軌跡。為了在不付出顯式影片生成高延遲代價的前提下善用 driving world model 的預測前瞻能力,作者進一步提出 Future-aware Rewarder(FAR):雖然 TA-DWM 能夠合成未來影片,但為每個候選軌跡都執行一次完整生成過程在運算上並不可行,FAR 因此採用以規劃為導向的蒸餾機制,直接從凍結的 world model 中蒸餾出未來潛在表徵,據此評估候選軌跡,使軌跡選擇與 world model 所學得的動態對齊,同時維持低延遲推論。訓練分兩階段:Phase 1 訓練 TA-DWM 進行場景生成(以 CogVideoX 預訓練權重初始化 3D VAE 與 DiT,在 nuPlan 與 nuScenes 組合資料集上以 16 張 NVIDIA A100 訓練);Phase 2 凍結編碼器、在 NAVSIM navtrain split 上以 8 張 NVIDIA 3090 訓練規劃器;最後凍結規劃器,以 PDMS 作為 oracle 偏好監督訓練 FAR。推論時 WorldDrive 不執行顯式未來場景生成,因而能實現低延遲規劃。

- **和以往方式的差異**:與既有兩類主流整合策略不同,WorldDrive 並非選擇「高保真生成但高成本」或「高效率但犧牲可解釋性」兩者之一,而是透過軌跡詞彙表為條件的結構化潛在空間設計,使視覺表徵與動作表徵從根本上同時被場景生成任務最佳化、並可直接遷移繼承至規劃器,解決了「場景模擬器強調視覺、規劃器獨立編碼動作」這一表徵錯位問題。此外,Future-aware Rewarder 讓系統得以利用 world model 的預測前瞻能力重新評分候選軌跡,而不需為每個候選軌跡付出顯式影片生成的高延遲成本,使得整套框架能同時兼顧高保真動作可控場景生成與即時規劃效能,相較於既有工作「生成與規劃各自為政」的做法是一次方法論上的整合創新。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖對比三種 driving world model 用於端到端自動駕駛的範式:(a) 以 driving world model 生成的未來場景進行規劃、(b) 以 latent world model 抽取的語意表徵進行規劃、(c) WorldDrive 透過統一視覺與動作表徵同時橋接規劃與 driving world model;第二張圖展示 WorldDrive 的整體架構,涵蓋 Phase 1 場景生成訓練與 Phase 2 動作規劃訓練兩階段,以及視覺與動作表徵如何在兩階段間被共同最佳化與遷移繼承。

![Figure]({{ site.baseurl }}/assets/images/2603.14948_worlddrive_paradigm.png)

_Figure 1: 三種 driving world model 整合規劃的範式比較——(a) 以生成未來場景規劃、(b) 以 latent world model 語意表徵規劃、(c) WorldDrive 統一視覺與動作表徵橋接兩者_

![Figure]({{ site.baseurl }}/assets/images/2603.14948_worlddrive_architecture.png)

_Figure 2: WorldDrive 整體架構——Phase 1 場景生成訓練與 Phase 2 動作規劃訓練，視覺與動作表徵在兩階段間共同最佳化與遷移繼承_

### Result

- **主要增強部分**:在 NAVSIM navtest split 的閉環規劃評測中,WorldDrive(單視角相機,world-model-based)取得 88.1 的 PDMS 分數,在同屬 world-model-based 的方法中與多視角+LiDAR 的 WoTE(88.3)相當接近,並明顯優於同為單視角的 DrivingGPT(82.4)、Epona(86.2)等方法,也優於多視角 world-model-based 的 LAW(84.6)、World4Drive(85.1)、FSDrive(85.1)。在 NAVSIM、NAVSIM-v2、nuScenes 三個 benchmark 上的大量實驗驗證了 WorldDrive 在純視覺方法中取得領先的規劃表現。在場景生成品質評測上(以 FID 與 FVD 量化),TA-DWM 同時展現高保真度的動作可控影片生成能力,並以定量分析驗證模型對不同動作控制的敏感度。

- **結果是否公正**:論文的評測涵蓋三個獨立的公開 benchmark(NAVSIM、NAVSIM-v2、nuScenes),並明確以感測器組態(多視角相機/單視角相機/LiDAR)與是否為 world-model-based 方法分類列表比較,使讀者能清楚辨識 WorldDrive 作為「單視角相機、無 LiDAR」配置下所取得表現的相對意義——其 88.1 分在感測器資訊量明顯少於 WoTE(多視角+LiDAR)的前提下仍取得相近表現,這一比較框架本身即誠實揭露了方法在感測器簡化與效能之間的權衡。附錄並提供 CARLA 模擬器的閉環規劃結果與進一步消融研究,增加結果的穩健性佐證。

- **已知 limitation**(論文原文 Limitations 章節):論文明確指出 WorldDrive 目前僅使用前視單一相機觀測,未採用多視角或多感測器輸入,相較於傳統使用多視角相機或多感測器融合的端到端駕駛方法,感測器配置較弱,這可能限制其在需要大範圍空間感知的場景(如大型路口、側向其他道路使用者互動)中的穩健性。此外,雖然軌跡詞彙表提供了結構化且有效的動作先驗,但它是由訓練軌跡分佈建構而成,對於罕見操作、高度互動行為或極端分佈外場景可能表現力不足。

### Limitation

- **從 result 來看的弱項**:在單視角、無 LiDAR 的感測器限制下,WorldDrive 的 PDMS(88.1)雖已逼近多視角+LiDAR 的 WoTE(88.3),但尚未能超越後者,顯示感測器資訊量的簡化仍對最終規劃表現構成一定上限;作者自陳的軌跡詞彙表侷限性,也意味著 WorldDrive 在長尾、高度互動的駕駛場景中的泛化能力仍待更多驗證,而這類場景往往正是自動駕駛安全性評估的核心關切。

### Related work

- WorldDrive 與本頁「World Models for Autonomous Driving」主題下既有收錄的 DriVerse、WoTE、PhyGenesis、Percept-WAM 等論文同屬駕駛場景 driving world model 譜系,但 WorldDrive 的獨特貢獻在於明確提出「表徵統一」這一設計哲學——不只是用 world model 生成場景或抽取語意表徵輔助規劃,而是讓場景生成與規劃任務共享同一組可遷移繼承的視覺-動作編碼器,此一角度此前較少被系統性地提出並驗證。
- 與本頁「World Models as Data Engines / Simulators for Robot Learning」主題下強調以生成式 world model 產生訓練資料或模擬評測的論文相比,WorldDrive 並非將 world model 用於資料生成,而是將其表徵學習能力直接注入規劃器的初始化與推論評分流程,是「表徵遷移」而非「資料遷移」的另一種整合路徑。
- 判斷值得 survey 的程度:中高。WorldDrive 已確認獲 NeurIPS 2026 接受,並公開釋出完整程式碼與模型檢查點,針對 driving world model 與規劃器之間長期存在的表徵錯位問題提出具體可行且已在三個公開 benchmark 上驗證的解法,對於理解 driving world model 的規劃整合方向具參考價值。

### Conclusion

- **綜合評價**:WorldDrive 針對既有 driving world model 整合進端到端規劃系統時普遍存在的「場景生成最佳化視覺表徵、規劃器獨立編碼動作表徵」表徵錯位問題,提出以軌跡詞彙表為條件的統一視覺-動作表徵框架,透過表徵繼承與 Future-aware Rewarder 的未來潛在表徵蒸餾機制,在不犧牲即時規劃低延遲特性的前提下,讓規劃器得以充分利用 driving world model 學得的動態與動作先驗,在三個公開 benchmark 上取得純視覺方法中具競爭力的規劃表現,同時維持高保真度的動作可控場景生成能力。
- **與其他重要文章的關係**:WorldDrive 可視為本頁「World Models for Autonomous Driving」主題下強調「生成與規劃整合」這一子方向的代表性延伸,其「表徵統一」設計哲學也呼應本頁「Model-Based RL / Latent Dynamics for Control」主題下以學習到的潛在動態模型做規劃的精神,但聚焦於駕駛場景的軌跡層級決策而非機器人操作的全身控制。ROCm/AMD 在此領域尚待補強之處:WorldDrive 的兩階段訓練流程涉及大規模影片擴散模型(3D VAE + DiT)預訓練與下游輕量規劃器的表徵遷移微調,這類「先以生成任務訓練大型視覺骨幹、再將其凍結表徵遷移至下游決策任務」的混合訓練範式,對底層深度學習框架在大型擴散模型訓練與下游凍結編碼器高效推論之間的無縫銜接提出要求;隨著 driving world model 與規劃整合的研究方向日益成熟,驗證此類表徵遷移訓練流程在 ROCm 軟體棧上的訓練與推論效能,是值得關注的生態系拓展方向。
