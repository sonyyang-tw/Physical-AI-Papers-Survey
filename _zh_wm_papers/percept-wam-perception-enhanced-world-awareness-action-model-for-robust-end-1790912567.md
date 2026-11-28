---
layout: paper
title: "Percept-WAM: Perception-Enhanced World-Awareness-Action Model for Robust End-to-End Autonomous Driving"
section: wm
page_id: "1790912567"
permalink: /zh/wm/percept-wam-perception-enhanced-world-awareness-action-model-for-robust-end-1790912567/
---

### Abstract

自動駕駛高度仰賴精準且穩健的空間感知能力,然而現有系統的失誤多半來自感知不準確與不穩定,尤其在長尾(long-tail)場景與複雜互動情境下更為明顯。現行視覺-語言模型(VLM)在空間定位(spatial grounding)與空間理解上能力薄弱,使得建立於其上的 VLA(視覺-語言-動作)自動駕駛系統,感知與定位能力也連帶受限。為解決此問題,作者提出 Percept-WAM,一個感知增強的 World-Awareness-Action Model,首度在單一 VLM 內部隱式整合 2D/3D 場景理解能力。不同於依賴問答式(QA-style)空間推理的既有做法,Percept-WAM 將 2D/3D 感知任務統一為 World-PV(透視視角)與 World-BEV(鳥瞰視角)兩種 token 類型,同時編碼空間座標與信心分數。作者並提出一套網格條件化(grid-conditioned)預測機制處理密集物件感知,結合 IoU-aware 評分與平行自迴歸解碼,提升長尾、遠距、小物件場景下的穩定性。此外,Percept-WAM 利用預訓練 VLM 參數保留通用智能(如邏輯推理能力),並能直接輸出感知結果與軌跡控制輸出。實驗顯示,Percept-WAM 在下游感知基準上達到或超越傳統(非 VLM)偵測器與分割器的表現,於 COCO 2D 偵測達 51.7 mAP、nuScenes BEV 3D 偵測達 58.9 mAP。當與軌跡解碼器整合後,進一步提升了 nuScenes 與 NAVSIM 上的規劃表現,例如在 NAVSIM 的 PDMS 指標上超越 DiffusionDrive 達 2.1 分。質化結果也凸顯其強大的開放詞彙(open-vocabulary)與長尾泛化能力。本論文由 Yinwang Intelligent Technology(引望智能技術,華為旗下智慧駕駛子公司,AITO/華為 ADS 智駕系統背後團隊)與復旦大學共 19 位研究者(Jianhua Han、Meng Tian、Jiangtong Zhu 等)於 2025 年 11 月 24 日發佈於 arXiv,已確認獲 CVPR 2026 接受(見 CVPR 2026 Open Access Repository 正式收錄頁面),雖非 2026 年 9 月最新發佈,但作為頂會接受論文、出自華為旗下智駕子公司與復旦大學,且尚未於本頁記錄,屬「World Models for Autonomous Driving」子主題下值得收錄的代表性工作。

### Method

- **要解決的問題**:自動駕駛系統的失效案例大量集中在長尾場景與複雜互動情境,例如擁擠路口、遠距小物件、非典型障礙物等。許多近期自駕系統嘗試建立在 VLM 之上以取得開放世界的語意理解與推理能力,但現有 VLM 普遍在空間定位與空間理解上能力薄弱——它們多半只能以問答(QA)形式描述「畫面中大致有什麼」,卻難以精確輸出物件的 2D/3D 座標、尺寸與方向。另一條路線是純擴散式(diffusion-based)規劃器,直接從視覺編碼器接上擴散解碼器生成軌跡,雖然規劃輸出精確,但缺乏語言層級的推理能力,難以處理需要常識判斷的場景(例如判斷「前方施工區應減速繞行」)。如何在同一個模型內同時具備精確的 2D/3D 空間感知能力與語言推理能力,是本論文試圖解決的根本問題。

- **Main method**:Percept-WAM 的核心創新是將 2D/3D 場景理解能力「隱式」整合進單一 VLM 內部,而非透過外掛式的問答模組。具體而言,模型以 InternVL2-8B 為 VLM 骨幹,並引入兩種新的 token 類型:World-PV(透視視角)token 負責處理 2D 偵測、實例分割、單目 3D 偵測等以相機視角為基礎的感知任務;World-BEV(鳥瞰視角)token 則透過可學習的 BEV 層級網格 token,隱式建模從 PV 特徵到 BEV 空間表示的映射,負責處理 BEV 3D 偵測與 BEV 地圖分割等任務。這兩類 token 皆同時編碼空間座標資訊與信心分數,使模型能直接輸出帶信心度的感知結果,而非僅止於文字描述。為處理密集物件感知(例如擁擠場景中大量相近物件),作者提出網格條件化預測機制:將 World-PV 或 World-BEV token 插值成網格查詢 token,每個網格查詢 token 負責預測對應位置是否存在物件及其邊界框,並搭配 IoU-aware 信心度訓練策略——訓練資料由模型自身預測結果搭配真實標註(ground truth)資料集生成信心度分數,使信心度分佈更貼近真實情況,相較於隨機擾動生成的信心度資料集,能有效降低假陽性(false positive)。解碼端採用串流 KV 快取(streaming KV cache)搭配 Prefill 階段處理視覺輸入,語言推理部分以自迴歸方式解碼思維鏈(Chain-of-Thought),軌跡預測則透過獨立的 Action Head 以平行解碼方式輸出 waypoint,兩種解碼模式並存於同一架構。模型同時支援相機、光達(LiDAR,選用)與文字輸入,文字輸入涵蓋任務指令與感知/軌跡預測的雙重監督訊號。

- **和以往方式的差異**:與傳統 VLM-based 方法(如 EMMA 等採用問答式空間推理)相比,Percept-WAM 不再透過文字描述物件位置,而是用專屬的 World-PV/World-BEV token 直接編碼精確空間座標,避免了語言表示空間座標時固有的精度損失與模糊性。與純擴散式規劃器(如 Diffusion Planner)相比,Percept-WAM 保留了 VLM 的語言推理能力,能同時處理需要常識判斷的場景語意理解與精確的軌跡規劃,而非僅做視覺到動作的直接映射。論文摘要明確宣稱這是首個在單一 VLM 內隱式整合 2D/3D 場景理解能力的工作,其網格條件化預測搭配 IoU-aware 信心度訓練,也是針對長尾、遠距、小物件這類感知難點量身打造的技術組合,而非既有偵測/分割技術的簡單移植。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖對比三種既有做法(問答式 VLM 感知、純擴散式規劃器)與 Percept-WAM 方法的差異,說明為何僅有 Percept-WAM 能同時達成「推理」與「感知」雙重目標;第二張圖展示完整架構,呈現串流相機輸入、選用光達輸入與文字輸入如何分別經編碼器處理後,透過 Prefill 與自迴歸/平行解碼雙模式,同時產生 World-PV/World-BEV 感知 token、語言推理思維鏈,以及軌跡預測的 World-Action token。

![Figure]({{ site.baseurl }}/assets/images/2511.19221_percept-wam_teaser.png)

_Figure 1: 既有做法 vs. Percept-WAM——問答式 VLM 感知缺乏精確空間座標、純擴散式規劃器缺乏推理能力,Percept-WAM 以 World-PV/World-BEV/文字/World-Action 四類 token 同時達成推理與感知_

![Figure]({{ site.baseurl }}/assets/images/2511.19221_percept-wam_architecture.png)

_Figure 2: Percept-WAM 完整架構——串流相機輸入與選用光達輸入經編碼器處理後,透過 Prefill 階段與自迴歸/平行解碼雙模式,同時輸出 PV/BEV 感知 token、語言推理思維鏈(CoT)、以及軌跡預測的 World-Action token_

### Result

- **主要增強部分**:在純感知基準上,Percept-WAM 達到或超越傳統(非 VLM)偵測器與分割器的表現——COCO 2D 偵測達 51.7 mAP、nuScenes BEV 3D 偵測達 58.9 mAP,證明將感知能力整合進 VLM 架構並未犧牲感知精度。當與軌跡解碼器整合、用於下游規劃任務時,在 nuScenes 與 NAVSIM 兩個自駕規劃基準上皆取得提升,其中在 NAVSIM 的 PDMS(Predictive Driver Model Score)指標上超越強基線 DiffusionDrive 達 2.1 分,顯示感知增強確實能轉化為規劃效益,而非僅止於感知基準上的數字提升。質化結果也展示了模型在開放詞彙偵測與長尾場景(遠距、小物件、擁擠場景)下的穩健泛化能力。

- **結果是否公正**:論文選擇與 DiffusionDrive 這類公認強健的既有規劃基線比較,而非僅與較弱的基線比較,2.1 分的 PDMS 提升幅度雖不算壓倒性,但在高度成熟的 NAVSIM 基準上仍屬有意義的進步。感知基準部分的比較對象涵蓋傳統非 VLM 的專用偵測/分割模型,顯示作者願意與該領域最強的非通用模型正面比較,而非僅在同屬 VLM 路線的模型間互相比較,增加了結果的說服力。

### Limitation

- **已知 limitation**:論文摘要與方法描述中並未詳細討論模型的計算成本與推理延遲——同時維護 PV 與 BEV 兩類 token 表示、搭配串流 KV 快取與雙重解碼模式(自迴歸 CoT + 平行 Action Head),其系統複雜度與部署時的即時性要求(自動駕駛對延遲極為敏感)之間的權衡,論文中著墨有限,這是從方法設計角度可以預見、但論文本身未充分展開討論的潛在限制。

- **從 result 來看的弱項**:感知基準提升雖達到與傳統偵測器相當或更好的水準,但並未顯著超越當前最強的專用感知模型(僅稱「matches or surpasses」),顯示將感知整合進 VLM 架構目前主要帶來的是「保留感知精度同時獲得語言推理能力」的綜合效益,而非感知精度本身的突破性提升;规劃任務上 2.1 分的 PDMS 提升幅度,相對於感知整合帶來的架構複雜度增加,其性價比仍待更多消融實驗驗證(例如移除語言推理分支是否會讓規劃表現下降,以釐清語言推理對規劃效益的具體貢獻)。

### Related work

- Percept-WAM 與本頁「World Models for Autonomous Driving」主題下已收錄的 Percept-WAM 之外論文(如 DriVerse、WoTE、EOT-WM、PhyGenesis)同屬自駕場景的 world/action model 研究,但切入角度有所不同——既有收錄論文多聚焦於場景生成、軌跡預測或閉環模擬評測,Percept-WAM 則是從「VLM 感知能力薄弱」這個更上游的問題切入,主張感知與動作生成應整合進同一個模型的同一組 token 表示中,這是與本頁既有收錄論文互補、而非重疊的切入點。其以 World-PV/World-BEV token 隱式編碼空間資訊的設計,也與本頁「Robot-Specific Action-Conditioned World Models」中強調統一動作-影片表示的論文(如 GeniWorld 以 URDF 渲染視覺動作取代數值動作條件化)在設計哲學上有相通之處——都試圖避免依賴「文字/數值」這類間接表示來傳遞空間或動作資訊,改用更貼近任務本質的 token 化表示。
- 判斷值得 survey 的程度:高。Percept-WAM 是少數同時提供感知基準(COCO、nuScenes)與下游規劃基準(nuScenes、NAVSIM)雙重驗證的自駕 VLA 論文,其「首度在單一 VLM 內隱式整合 2D/3D 場景理解」的主張若屬實,對於正在探索「VLM-based 自駕系統感知瓶頸」這一業界普遍關注問題的研究者具有高參考價值,適合與本頁「Model-Based RL / Latent Dynamics for Control」及「World Model Evaluation」主題交叉參照。

### Conclusion

- **綜合評價**:Percept-WAM 針對 VLM-based 自駕系統長期存在的空間定位薄弱問題,提出了一個架構層級的解法——將 2D/3D 感知任務統一編碼為 World-PV/World-BEV token,而非依賴問答式的間接文字描述。其在感知與規劃兩類基準上皆取得驗證,且與公認強健的基線(DiffusionDrive)正面比較並取得提升,顯示方法具備一定的實務意義。作為獲 CVPR 2026 接受、出自華為旗下智駕子公司引望智能技術與復旦大學的工業界論文,其結果直接服務於量產自動駕駛系統的感知-規劃一體化設計決策。

- **與其他重要文章的關係**:Percept-WAM 與本頁「World Models for Autonomous Driving」主題下的既有收錄論文形成互補視角,共同勾勒出自駕 world/action model 領域「場景生成」與「感知增強」兩條並行的研究路線。ROCm/AMD 在此領域尚待補強之處:Percept-WAM 的訓練與推理管線涉及 InternVL2-8B 這類大型 VLM 骨幹的微調、串流 KV 快取機制、以及自迴歸與平行解碼雙模式並存的複雜解碼邏輯,這類「感知-語言-動作三合一」的統一自駕模型架構正逐漸成為中國主要智駕供應商(華為引望、以及本頁已收錄的 AGIBOT 等)的技術路線共識;若 AMD 欲切入中國自動駕駛產業鏈的訓練與推理基礎設施市場,驗證此類多模態 token 混合解碼架構(尤其是串流 KV 快取與平行解碼混合使用時的記憶體管理與排程效率)在 ROCm 上的相容性與效能,將是具體且具產業急迫性的生態系拓展方向,特別是考量到中國自駕供應商在地緣政治因素下對多元硬體供應鏈的潛在需求。
