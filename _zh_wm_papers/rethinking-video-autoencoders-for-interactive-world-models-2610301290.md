---
layout: paper
title: "Rethinking Video Autoencoders for Interactive World Models"
section: wm
page_id: "2610301290"
permalink: /zh/wm/rethinking-video-autoencoders-for-interactive-world-models-2610301290/
---

### Abstract

互動式 video world model 從過去影格與動作預測未來影格,作為訓練、規劃、評估 agent 的模擬器,也供人類即時互動控制。這類模型在 video autoencoder 的 latent space 中生成,autoencoder 的壓縮程度決定了每影格成本與每個動作需等待多久才能生效。然而既有 world model 往往沿用 text-to-video 生成模型的 autoencoder,這類 autoencoder 是為離線生成(無 agent 等待)而設計,且因訓練資料與程式碼未公開而無法在其他壓縮程度下重新訓練。作者提出 CADRE(Causal Diffusion REpresentation autoencoders),一套涵蓋多種時空壓縮程度的開源 causal diffusion representation autoencoder 家族,家族成員僅在凍結特徵上的小型瓶頸層有所差異,並共享一個經自我蒸餾至一到數步的 diffusion 解碼器。作者在操作(manipulation)與導航(navigation)兩大領域、各含兩個環境的設定下,於每個 autoencoder 上訓練相同的 world model。CADRE 構成了延遲-品質前沿的絕大部分,在移動相機情境下尤其明顯。研究並歸納出四項發現:在強壓縮下,diffusion 解碼器比感知式迴歸更清晰;在機器人操作中,時間壓縮在 autoencoder 層級比在 world model 層級更有效;操作與導航場景需要相反的壓縮策略(靜止相機下時間壓縮代價低,移動相機下則偏好空間壓縮);令人意外的是,在靜止相機情境下,較粗糙的空間 token 對動作品質的傷害遠大於對影像品質的傷害。論文於 2026 年 10 月 21 日發佈於 arXiv,作者團隊來自 Kyutai(法國 AI 實驗室)、LIGM/ENPC/IP Paris/CNRS/UGE 與 UC Berkeley,程式碼、模型與線上展示已公開於 kyutai.org。

### Method

- **要解決的問題**:一個互動式 world model 的每影格成本、動作延遲、乃至大部分生成品質,都繼承自其 video autoencoder,因此 autoencoder 的壓縮程度本質上是一項設計選擇。然而既有 world model 普遍直接沿用 text-to-video 生成模型(如 Wan、LTX、Cosmos)的 autoencoder,這些 autoencoder 是為「無 agent 在旁等待」的離線批次生成情境設計,其壓縮程度未必適合互動式場景對低延遲、高反應性的需求;更根本的問題是,這些 autoencoder 的訓練資料與程式碼大多未公開,使得研究者無法在不同壓縮程度下重新訓練以系統性研究「world model 應該如何、在何處、壓縮多少」這一核心問題。

- **Main method**:CADRE 採用凍結特徵提取器(DINOv3)搭配一個可訓練的 3D 卷積瓶頸層,將每 τ 個影格的 s′² 個 patch 壓縮為確定性 latent,只有這個瓶頸層、lift 層與時間 patch size 隨壓縮程度(τ×s×s)而異,其餘recipe 完全共享,確保七個家族成員之間的 world model 效能差異只能歸因於壓縮程度本身而非訓練 recipe 的差異。解碼端使用 time-causal diffusion 解碼器而非感知式迴歸解碼器,因為強壓縮 latent 保留場景佈局與語意卻丟失紋理細節,迴歸解碼器會將多個合理紋理平均成模糊畫面,而 diffusion 解碼器則透過在三個位置條件化 latent(轉置卷積提升並疊加至 patchify 後的雜訊片段、每個區塊中的空間 AdaLN、零初始化卷積頭的 skip connection)來採樣影片,並透過自我蒸餾壓縮至一到數個去噪步驟以降低推論成本。解碼器以 flow matching 訓練,搭配 diffusion forcing 讓每個 τ 影格的片段各自抽取獨立的雜訊時間點 t,訓練目標結合平均絕對誤差、兩種感知距離(LPIPS 與 DINO 特徵空間類比版本)。作者接著在操作與導航兩大領域、各兩個環境上,於每個壓縮點的 autoencoder 上訓練相同的 1.2B 參數 causal diffusion transformer world model,系統性比較七種壓縮程度在延遲-品質前沿上的表現。

- **和以往方式的差異**:既有 world model 研究(如 Cosmos、Wan、LTX 系列)多將 autoencoder 視為既定的外部元件,直接重用現成的 text-to-video autoencoder 並專注於 world model 本身的架構與訓練改進。CADRE 的差異在於首次將「autoencoder 的壓縮設計」本身作為一個可系統性研究的自由變數,透過開源一整個家族(僅瓶頸層不同、其餘 recipe 完全共享)使研究者得以公平地分離 autoencoder 選擇對 world model 延遲與品質的獨立影響,而非被既有商用 autoencoder 的黑盒壓縮策略所限制。這種「開源可重訓練 autoencoder 家族」的研究方法論本身,填補了既有 world model 文獻中「autoencoder 選擇被視為既定事實而非研究對象」的空白。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示 CADRE 的核心發現總覽:在單張 H100 上,CADRE world model 可達 20 fps 並在低於 230 毫秒內做出反應(低於可察覺的動作延遲門檻),且在運動保真度(FVD)與動作遵循(ARR)的延遲-品質前沿上構成大部分最優點;第二張圖展示跨壓縮程度的質化重建結果比較。

![Figure]({{ site.baseurl }}/assets/images/2610.30129_cadre_teaser.png)

_Figure 1: CADRE 核心發現總覽——在單張 H100 上,CADRE world model 達 20 fps 並於低於 230 毫秒內反應,構成運動保真度(FVD)與動作遵循(ARR)延遲-品質前沿的大部分最優點;右側展示動作延遲過長會使雜耍、摺疊等任務難以執行、駕駛等任務產生危險_

![Figure]({{ site.baseurl }}/assets/images/2610.30129_cadre_qualitative.png)

_Figure 2: 跨壓縮程度的質化重建結果比較,展示不同時空壓縮點下 autoencoder 重建品質與細節保真度的差異_

### Result

- **主要增強部分**:CADRE 在單張 H100 上運行達 20 fps,反應延遲低於 230 毫秒(低於文獻中可察覺動作延遲的門檻),在 Wan 2.2、LTX-2、Cosmos 等既有 autoencoder 的對比中,於 48 項比較中的 42 項同時更快且品質更佳,構成運動保真度(FVD)與動作遵循率(ARR)延遲-品質前沿的絕大部分最優點。具體而言,在相同解碼步數下,CADRE-2×32×32 反應延遲僅 185 毫秒並維持 23.4 fps,而 Wan 2.2 autoencoder 需 317 毫秒、LTX-2 需 492 毫秒、Cosmos 需 605 毫秒。研究並歸納出四項可操作的壓縮設計準則:強壓縮下 diffusion 解碼器優於感知式迴歸解碼器;機器人操作場景中時間壓縮放在 autoencoder 比放在 world model 更有效;操作(通常靜止相機)與導航(通常移動相機)場景需要相反的壓縮策略;靜止相機下粗糙空間 token 對動作品質與動作遵循的傷害遠大於對影像品質的傷害。

- **結果是否公正**:論文在操作與導航兩大領域、各兩個環境上,於完全相同的訓練 recipe 下比較七個壓縮點,並與三個業界常用的既有 autoencoder(Wan 2.2、LTX-2、Cosmos)進行延遲與品質的直接對比,評測涵蓋影像品質(FVD)與動作遵循率(ARR)兩個面向,並在附錄中提供完整的逆動力學探測、長 horizon rollout、運動量分析等補充實驗,顯示作者對結論的穩健性有系統性驗證,而非僅依賴單一指標或單一環境的結果。

### Limitation

- **已知 limitation**:論文明確指出,每個 world model 僅針對單一環境訓練,這些壓縮設計準則是否能延伸至通用型(generalist)world model,以及是否能延伸至 policy 訓練與規劃任務,仍是open 問題。此外,論文使用的操作資料多採用靜止或近乎靜止的相機,但實務上手腕相機(wrist-mounted camera)是會移動的,作者推測這類移動相機場景應更偏好導航領域的壓縮策略,但此推論尚未直接驗證。

- **從 result 來看的弱項**:論文的核心結論建立在七個壓縮點、兩大領域、各兩個環境的實驗矩陣上,樣本環境數量相對有限,「操作偏好時間壓縮、導航偏好空間壓縮」這類二分類準則在更多樣化的真實場景(例如混合靜止與移動相機、多相機視角融合)下是否依然成立,仍需更大規模的環境覆蓋驗證;此外,1.2B 參數的 world model 規模與操作/導航資料集規模相對於當前業界最大規模的 world model(如 NVIDIA Cosmos)仍有相當差距,壓縮準則在更大規模模型與資料下是否依然成立也是未知數。

### Related work

- CADRE 與本頁「World Models as Data Engines / Simulators」「Model-Based RL」主題下已收錄的多篇論文(如 Cosmos Predict 2.5、CADRE 比較基線中的 Wan、LTX)同屬「video world model 基礎設施」這一方向,但切入點不同:既有工作多聚焦於 world model 本身的架構、訓練目標、或下游應用(policy 訓練、規劃),CADRE 的獨特貢獻在於明確將「autoencoder 選擇」本身拆解出來作為獨立研究對象,是目前同類工作中少見的「系統性拆解 world model 上游元件設計空間」的方法論研究。
- 論文呼應本頁「Interactive World Simulator」子主題下強調「低延遲互動反應」的設計哲學,與既有強調生成品質優先的 text-to-video world model(如 Cosmos、Wan 系列)形成互補視角——後者優化離線生成品質,CADRE 則專門針對「agent 正在等待」的互動情境優化延遲-品質權衡。
- 判斷值得 survey 的程度:高。CADRE 出自 Kyutai(具國際知名度的法國 AI 實驗室,與 UC Berkeley 合作)等機構,開源完整的 autoencoder 家族、程式碼、模型與線上展示,其「拆解壓縮設計空間」的研究方法論具備高度可複製性與延伸性,對於理解「如何為特定互動場景(操作 vs. 導航)挑選合適的 world model 壓縮策略」這一此前被業界視為既定事實的問題,提供了具體可操作的量化指引。

### Conclusion

- **綜合評價**:CADRE 針對互動式 world model 研究中一個長期被忽略的上游設計選擇——video autoencoder 的時空壓縮程度——提出了系統性的開源研究框架與具體可操作的設計準則。其核心創新不在於更強的 world model 架構本身,而在於首次將 autoencoder 壓縮本身拆解為可控的自由變數並開源整個家族,使「壓縮如何影響延遲與品質」這一問題得以被嚴謹地量化回答,為後續互動式 world model 的基礎設施設計提供了可直接遵循的量化依據。

- **與其他重要文章的關係**:CADRE 可與本頁「World Models as Data Engines / Simulators」主題下的 NVIDIA Cosmos 系列論文互補對照——Cosmos 聚焦於大規模通用型 world foundation model 的訓練與應用,CADRE 則聚焦於支撐這類 world model 的底層 autoencoder 設計選擇,兩者分屬 world model 技術棧中不同層級的貢獻。ROCm/AMD 在此領域尚待補強之處:CADRE 的 causal diffusion 解碼器透過自我蒸餾壓縮至一到數個去噪步驟以達成即時互動所需的低延遲(230 毫秒內、20 fps),這類對單步/少步 diffusion 解碼延遲高度敏感的推論工作負載,對底層算子函式庫的小型 batch 低延遲推論效能與 KV cache/causal attention 效率提出了具體要求;隨著互動式 world model 的「低延遲優先」設計理念逐漸從大型科技實驗室擴散至更廣泛的機器人與遊戲應用場景,驗證此類時間-因果(time-causal)diffusion 解碼管線在 ROCm 軟體棧上的低延遲推論效能,將是具體且具產業急迫性的生態系拓展方向。
