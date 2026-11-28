---
layout: paper
title: "RynnVLA-Latent: Scaling Robotic Manipulation Foundation Models with 3D-Grounded Latent Actions"
section: vla
page_id: "2610343560"
permalink: /zh/vla/rynnvla-latent-scaling-robotic-manipulation-foundation-models-with-3d-ground-2610343560/
---

### Abstract

擴展 VLA 模型規模的核心瓶頸在於動作標註示範資料稀缺,且不同機器人具身之間的控制空間互不相容。本論文提出 RynnVLA-Latent,將異質互動影片轉化為可規模化的機器人 policy 預訓練監督訊號。其核心是 RynnLAM,一套無需原生機器人控制訊號、直接從視覺轉變中學習連續、3D 接地(3D-grounded)latent action 的方法,結合殘差未來特徵預測、相機補償 3D 光流監督、以及相機運動解耦三項機制,使表示聚焦於控制相關的運動而非單純外觀變化。作者將 RynnLAM 應用於 30.1K 小時的人類、機器人與模擬影片,產出 7.4552 億筆 latent action 描述子。RynnVLA-Latent 接著透過 flow matching 學習從視覺觀測與語言預測 latent action chunk,再將預訓練骨幹與 action expert 適配至具身專屬的機器人動作。最終 4B 參數的 policy 在 LIBERO 上達到 98.8% 成功率,在未經 benchmark 專屬調整的 LIBERO-Plus 上達到 84.7%,在 VLABench 五個賽道平均達到 51.9%,在 RoboTwin 2.0 雙臂 benchmark 上平均達到 88.6%,並在涵蓋靈巧手與移動夾爪平台的六項真實世界操作任務中,相較所有比較方法取得最高成功率。論文於 2026 年 10 月 25 日發佈於 arXiv,作者團隊來自 DAMO Academy(阿里巴巴集團)、Hupan Lab、Hong Kong Embodied AI Lab 與香港中文大學(CUHK),屬大型產業實驗室出品的 VLA 資料擴展代表作。

### Method

- **要解決的問題**:機器人操作知識最豐富的來源——人類影片、網路影片、模擬環境,以及異質機器人資料集——彼此並不共享同一套動作表示。機器人示範資料收集成本高昂,其原生控制訊號在維度、座標系、語意上各不相同,無法簡單地以單一原生動作預測目標池化訓練。既有 latent action 方法雖展示了轉變重建與特徵空間預測的價值,但視覺變化本身可能包含相機運動、靜態外觀等與控制無關的成分,因此一個影像重建良好的表示未必同樣適合預測低階操作動作。

- **Main method**:作者提出 RynnLAM,將一對影格編碼為運動 token、全域 action latent、以及相機 latent 三部分。殘差未來特徵預測在瓶頸中保留轉變資訊,相機補償 3D 光流偽標籤與對比式特徵扭曲(warping)鼓勵表示對運動敏感,相機姿態預測與梯度反轉則進一步促使自我運動(ego-motion)與操作相關線索分離。這些目標在不需人工標註機器人動作的前提下提供幾何接地。以 RynnLAM 作為離線標註器,作者為涵蓋人類互動、真實機器人、模擬環境的 25 個影片來源建立共享 latent action 監督,語料庫約含 30.1K 小時、1663 萬個 episode、30.57 億影格,產出 7.4552 億筆 latent action 描述子。RynnVLA-Latent 本身是一個 Mixture-of-Transformers policy,耦合預訓練視覺語言骨幹與窄幅 action expert,透過 flow matching 從多視角觀測與語言預測 latent action chunk,不需原生動作或本體感覺監督;在機器人後訓練階段,重用骨幹與 action expert trunk,引入本體感覺,並將輸出投影重新定位至具體機器人指令。

- **和以往方式的差異**:LAPA、Moto、IGOR 等既有 latent action 方法已證實視覺轉變可作為規模化的類動作監督來源,UniVLA、villa-X 等後續工作則致力於讓這類表示更利於控制。RynnVLA-Latent 的差異在於明確引入幾何監督(3D 光流、相機姿態)與相機運動解耦機制,使 latent action 描述子更聚焦於控制相關運動而非相機/外觀變化;同時將「影片動作監督」與「具身專屬動作對齊」拆分為兩個階段——預訓練階段完全不需任何機器人動作標籤,僅在最終適配階段才需要成本高昂的動作標註示範,大幅降低了跨具身規模化所需的標註成本。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示多具身影片語料庫的資料整理管線(影片字幕、光流估計、深度估計三重標註流程);第二張圖展示 RynnVLA-Latent 的整體架構,呈現 RynnLAM 離線標註器如何產生 latent action 描述子,以及 Mixture-of-Transformers policy 如何透過 flow matching 從視覺觀測與語言預測這些描述子,並在後訓練階段重新定位至具體機器人動作空間。

![Figure]({{ site.baseurl }}/assets/images/2610.34356_rynnlam_overview.png)

_Figure 1: RynnVLA-Latent 資料整理管線——多具身影片語料庫經 Qwen3-VL 字幕生成、DPFlow 光流估計、Depth Anything 3 深度估計三重標註後產出 latent action 監督_

![Figure]({{ site.baseurl }}/assets/images/2610.34356_rynnlam_arch.png)

_Figure 2: RynnLAM 與 RynnVLA-Latent 架構——離線標註器產生 3D 接地 latent action 描述子,policy 透過 flow matching 從多視角觀測與語言預測 latent action chunk,再適配至具身專屬機器人動作_

### Result

- **主要增強部分**:在凍結表示探測實驗(LARY)中,完整描述子達到平均相對動作 MSE 0.38,顯示該表示本身具備低階控制預測力。經原生動作後訓練後,4B policy 在 LIBERO 達到 98.8% 成功率,在未經 benchmark 專屬調整的 LIBERO-Plus 達到 84.7%,在 VLABench 五個賽道平均達到 51.9%,在 RoboTwin 2.0 Native 協定下平均達到 88.3%(摘要中另提及雙臂 benchmark 整體達 88.6%)。這些 benchmark 分別評測任務執行、擾動穩健性、語意接地、雙臂操作四個面向。在涵蓋靜態靈巧手與移動夾爪平台的六項真實世界操作任務中,RynnVLA-Latent 在所有比較方法中取得最高成功率。

- **結果是否公正**:論文同時提供表示層級(凍結探測)與 policy 層級(模擬 benchmark 與真實世界任務)的雙重驗證,涵蓋 LIBERO、LIBERO-Plus、VLABench、RoboTwin 2.0 四套公開 benchmark,並額外提供資料規模化趨勢與元件消融研究(RynnLAM 消融、RynnVLA-Latent policy 變體消融),顯示作者對各環節的效用與限制皆有系統性交代,而非僅報告單一端到端數字。

### Limitation

- **已知 limitation**:論文明確指出,深度、相機姿態、光流皆為估計所得的偽標籤,因此幾何監督並不保證經過校準的度量運動,也不保證相機與操作資訊完全分離;低階控制探測衡量的是可預測性,解碼光流提供的是定性詮釋,而非因果動作可識別性的證明。Policy 表現因任務與擾動設定而異,RoboTwin 分數仍低於部分最強基線。目前結果並未建立通用的 scaling law,也未將預訓練資料量與優化曝光量的差異完全隔離。

- **從 result 來看的弱項**:RoboTwin 2.0 benchmark 上的表現雖具競爭力,但仍落後於部分列出的最強基線,顯示在雙臂複雜操作場景下,純粹依賴 latent action 預訓練尚無法完全取代針對特定具身的直接動作監督;部署至新機器人仍需要具身專屬的動作標註示範資料,這意味著「免動作標籤預訓練」的優勢主要體現在大規模前期知識獲取階段,而非完全消除下游標註需求。

### Related work

- RynnVLA-Latent 與本頁「Data, Benchmarks & Simulation」「Architecture Paradigms」主題下已收錄的多篇論文(如 EgoScale、HuRo)同屬「擴大可用訓練資料來源」這一方向,但切入點不同:EgoScale 驗證第一人稱人類影片資料規模與下游表現之間的 scaling law,HuRo 透過機器人化管線將人類影片轉換為機器人對齊格式,而 RynnVLA-Latent 的獨特貢獻在於提出一套具備顯式幾何監督與相機解耦機制的 latent action 學習方法(RynnLAM),並將其系統性應用於包含人類、機器人、模擬在內的 25 個異質影片來源,規模達 30.1K 小時,是目前同類工作中資料規模與驗證完整度都相當突出的嘗試。
- 論文作者團隊同期發表的姊妹研究 RynnWorld-Latent(本頁同日收錄於 World Model 類別)使用同一套 RynnLAM 描述子作為 cross-embodiment video world model 的條件介面,兩篇論文共同構成「latent action 作為統一監督/條件介面」這一完整敘事的兩面:一面用於 policy 預訓練監督目標,另一面用於可控視覺動態生成與資料生成引擎。
- 判斷值得 survey 的程度:高。RynnVLA-Latent 出自 DAMO Academy(阿里巴巴集團)等大型產業實驗室,在四套業界常用公開 benchmark 與六項真實世界任務上均取得具競爭力或最佳表現,資料規模化與消融實驗設計完整,對於理解「如何在缺乏原生動作標籤的前提下規模化利用異質影片資料訓練 VLA」這一核心議題具有高度參考價值。

### Conclusion

- **綜合評價**:RynnVLA-Latent 針對 VLA 規模化訓練中「動作標籤稀缺、跨具身控制空間不相容」這一結構性瓶頸,提出了以幾何接地 latent action 作為統一監督介面的解法,並在 30.1K 小時規模的異質影片語料上完成系統性驗證。其核心創新不在於更強的 policy 架構本身,而在於重新設計「監督訊號從何而來」,透過將大規模免動作標籤影片轉化為可規模化的 policy 預訓練訊號,為降低機器人學習的資料標註成本提供了具體且經過驗證的路徑。

- **與其他重要文章的關係**:RynnVLA-Latent 可與本頁「Data, Benchmarks & Simulation」主題下聚焦資料規模化的論文(如 EgoScale、HuRo)互補對照——後者關注「如何取得更多可用的人類/機器人影片資料」,RynnVLA-Latent 則關注「如何將這些異質資料轉化為統一可用的監督訊號」,兩者分屬資料擴展管線中不同環節的貢獻。ROCm/AMD 在此領域尚待補強之處:論文的大規模影片標註(Qwen3-VL 字幕、DPFlow 光流、Depth Anything 3 深度估計)與 RynnLAM 離線標註管線涉及大量視覺基礎模型推論與 250 個 shard 的平行處理,此類資料前處理與 latent action 標註的工作負載具備高度平行性與批次推論特性;隨著「latent action 作為統一監督介面」逐漸成為業界降低 VLA 訓練資料成本的標準手法,驗證此類大規模多模態離線標註與 Mixture-of-Transformers policy 訓練管線在 ROCm 軟體棧上的相容性與吞吐效能,將是具體且具產業急迫性的生態系拓展方向。
