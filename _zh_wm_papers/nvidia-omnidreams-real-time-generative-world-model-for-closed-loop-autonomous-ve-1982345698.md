---
layout: paper
title: "NVIDIA OmniDreams: Real-Time Generative World Model for Closed-Loop Autonomous Vehicle Simulation"
section: wm
page_id: "1982345698"
permalink: /zh/wm/nvidia-omnidreams-real-time-generative-world-model-for-closed-loop-autonomous-ve-1982345698/
---

### Abstract

隨著自駕系統能力提升，如何安全評測長尾（long-tail）場景下的駕駛策略，仍是關鍵瓶頸。以重建為基礎（reconstruction-based）的神經模擬器（如 3DGS/NeRF）雖具高擬真度，卻受限於原始擷取資料，難以泛化至高度動態或未曾出現的場景。為克服此限制，作者提出 OmniDreams：一個從 Cosmos 擴散模型中期訓練（mid-trained）與後期訓練（post-trained）而來的基礎生成式 world model，能即時、自迴歸地生成以動作為條件的影片。透過運用 Cosmos 豐富的視覺先驗，並在 21,000 小時的駕駛場景上進行中/後期訓練，OmniDreams 能合成傳統模擬器難以捕捉的複雜未見現象（如極端天氣、不可預測的動態代理行為）。其關鍵設計是以自迴歸方式，將過去影格、當前模擬器狀態與即時駕駛動作作為條件，持續生成逼真感測器輸出。OmniDreams 已與 Alpamayo 1 policy 及 AlpaSim 協調器整合為閉環系統，作為高度響應、可互動的環境，為下一代自駕策略提供可擴展且完整的訓練與評測解決方案。此外，論文展示初步結果：從 OmniDreams 後期訓練而得的 World-Action Model（WAM）在 Physical AI Autonomous Vehicles NuRec 資料集上的表現超越以 VLA 為基礎的 Alpamayo 1.5 研究型 policy 模型，且僅使用其五分之一的參數量。

### Method

- **要解決的問題**：閉環（closed-loop）自駕模擬需要一個具互動性、可擴展的模擬器——當 policy 的動作改變下一步觀測時，模擬器必須即時、動態地更新場景。以重建為基礎的神經模擬器（如 NVIDIA NuRec 所採用的 3DGS/NeRF）雖具高擬真度，卻被錨定在原始擷取資料上：既無法泛化至擷取路徑以外的新視角，也難以合成從未被記錄過的現象（極端天氣、罕見物件、複雜動態代理行為）。而基於大規模影片訓練的生成式 world model 雖能合成此類長尾現象，卻必須同時具備即時速度（低延遲）與足夠的可控性（以動作為條件），才能真正作為閉環模擬器使用，而非僅是離線影片生成工具。

- **Main method**：OmniDreams 建立在 Cosmos-Predict 2.5 擴散骨幹之上，以四種訊號為條件：(1) 首幀 RGB（乾淨 latent）、(2) 文字提示（透過 Cosmos 文字編碼器做 cross-attention）、(3) 抽象「世界場景地圖」（world-scenario map，由車道線、行人穿越道、3D 偵測/追蹤的動態物件立方體投影至各相機視角後，經輕量 MLP 編碼為控制 token 與視覺 token 拼接，較 ControlNet 式旁路網路更省算力）、(4) 先前生成 token 的記憶/KV 快取。模型有單視角（SV，前視單相機）與多視角（MV，4 相機同步）兩種版本，MV 版本將注意力機制拆解為「逐視角時間注意力」（透過因果 KV 快取）加上「跨視角注意力」，把複雜度從 O(N²T²) 降至 O(NT²)+O(N²)。訓練分多階段進行：先在 RDS（16,600 小時，涵蓋 15 國）上對 Cosmos-Predict 2.5 做自駕領域中期訓練；接著加入跨視角注意力做多視角中期訓練；再加入零初始化的世界場景控制分支，以 flow matching 在雙向教師模型上訓練；然後透過 Diffusion Forcing（因果遮罩自注意力、每影格獨立取樣噪聲層級）轉換為因果/自迴歸模型；最後以 Self Forcing 蒸餾（結合自迴歸自我 rollout 與 Distribution Matching Distillation, DMD 的整體反向 KL 分佈匹配損失）大幅提速，並透過「以更長 context 教師模型持續蒸餾」的漸進式訓練策略，緩解滾動 KV 快取超出訓練 context 時產生的畫面漂移偽影。推論階段則採用局部窗口時間注意力、串流式靜態形狀 KV 快取、torch.compile 加 CUDA graphs、輕量 VAE/decoder（LightTAE）替換，以及跨相機/時間/空間軸的階層式 context-parallel 切分（透過 ring-attention），並打包為開源的 FlashDreams 服務框架。整套系統整合進 NVIDIA AlpaSim（基於 gRPC/Docker 的自駕模擬器微服務），取代原有的 NuRec 相機渲染器，並以「預取生成」（pre-fetch generation）機制讓 policy/交通模型在區塊邊界時間點預測多步軌跡，維持事件順序一致性。

- **和以往方式的差異**：與 GAIA-1/GAIA-2、DriveDreamer 等既有生成式自駕 world model 相比，OmniDreams 的關鍵區隔在於「即時、自迴歸、可作為真正閉環模擬器」的工程實現——透過 Self Forcing 蒸餾與漸進式長 context 教師策略解決長 rollout 畫面漂移問題，並透過 FlashDreams 服務堆疊達成單視角 68 FPS、多視角 105 FPS 的即時效能，而非僅止於離線高品質影片生成；此外，論文額外驗證同一個 OmniDreams 骨幹可後期訓練為端到端 World-Action Model（WAM）直接輸出軌跡，將「世界模型」與「動作生成」統一在單一架構中，這與既有將重建式模擬器與獨立動作策略分離的做法形成明確區隔。

- **關鍵方法圖**：見下方嵌入圖片——Figure 1 展示 OmniDreams 在閉環模擬中的角色：policy 透過 AlpaSim 與 OmniDreams 互動，動作驅動下一步感測器影格生成，形成完整迴圈；另一張圖展示 OmniDreams 同時以首幀影像、文字提示與世界場景地圖三種訊號作為條件輸入的架構設計。

![Figure]({{ site.baseurl }}/assets/images/2606.03159_teaser.png)

_Figure 1: OmniDreams 閉環模擬工作流程——policy 透過 AlpaSim 與 OmniDreams 互動生成感測器影格，形成完整閉環_

![Figure]({{ site.baseurl }}/assets/images/2606.03159_input_output.png)

_Figure 2: OmniDreams 架構圖——同時以首幀影像、文字提示與世界場景地圖三種訊號作為生成條件_

### Result

- **主要增強部分**：即時效能方面，單視角 2B 參數模型在單顆 GB300 GPU 上於 720p 解析度達 68 FPS，四相機多視角模型在 16 顆 GB300 GPU 上達 105 FPS。生成品質消融（FVD 指標）顯示：雙向自駕適配教師模型 FVD 為 26.8，因果 Diffusion-Forcing 學生模型品質下降至 31.7，而經 Self Forcing 蒸餾的學生模型 FVD 反而達到最佳的 24.8（因蒸餾資料經過精心篩選，甚至優於雙向教師模型）。長 rollout 穩定性方面，20 秒 rollout 切分為四個 5 秒窗口後，短 context 教師模型平均 FVD 為 240.0（首尾窗口差距達 299.9，漂移嚴重），而漸進式長 context 教師模型平均 FVD 降至 179.4（差距僅 172.9），大幅改善長 horizon 穩定性。最關鍵的下游驗證是：以 OmniDreams 後期訓練的 World-Action Model 在 574 個場景的 PAI NuRec 資料集閉環評測中，相較於以 VLA 為基礎的 Alpamayo 1.5（約 100 億參數），僅用約 20 億參數（五分之一）就將整體碰撞率從 6.9% 降至 4.2%、後方碰撞率從 5.3% 降至 3.0%。此外，在 NuRec 與 OmniDreams 兩種模擬器間切換閉環評測時，policy 的相對排名保持一致，且相較於 NuRec 的 FVD 會隨偏離原始擷取路徑而急遽上升，OmniDreams 在偏離路徑時仍能維持穩定的視覺品質，凸顯其作為「可信代理模擬器」的優勢。

- **結果是否公正**：論文提供了完整的生成品質消融（比較雙向教師、因果學生、蒸餾學生三個階段）、解碼器取捨分析（原始 VAE vs. 輕量 LightTAE）、長 rollout 穩定性對照實驗，以及跨模擬器（NuRec vs. OmniDreams）policy 排名一致性驗證，方法論設計嚴謹。作者也坦承 WAM 評測結果為「初步」（preliminary），並非決定性結論，展現出合理的科學謹慎態度。FlashDreams 服務堆疊額外驗證於 Wan2.1 系列骨幹（Self Forcing、Lingbot-World）上均取得加速，顯示其通用性而非僅針對 OmniDreams 特化。

### Limitation

- **已知 limitation**：作者明確指出，以影片生成為基礎的模擬相較於重建式模擬器天生需要遠高得多的運算資源，存在品質與運算成本的明確取捨；目前系統以固定長度的「區塊」（chunk）為單位生成，policy/交通模型無法在區塊內部即時修改軌跡，論文將「縮小區塊尺寸、最終達成逐影格生成」列為未來世代 world model 的目標；目前的網路整合仍依賴 gRPC 進行影格編碼/解碼傳輸（而非 RDMA/NCCL 直接傳輸），也被列為待改進的複雜度與資訊損失來源。

- **從 result 來看的弱項**：論文提及直接插入分佈外物件而不做特殊的動態立方體丟棄式後期訓練，會導致視覺偽影與動態不一致；WAM 相較 VLA 的效能提升雖顯著，但作者自陳此評測仍屬初步性質，尚待更完整的下游驗證。

### Related work

- OmniDreams 與本頁已收錄的自駕 world model 基礎模型（GAIA-1、GAIA-2）及 NVIDIA 自身的 Cosmos 平台一脈相承，是「以重建式模擬器為主流」轉向「生成式 world model 作為閉環模擬器」的具體實踐；論文亦援引 DriveGAN、DriveDreamer、Vista、MagicDrive、Drive-WM、GenAD 等既有生成式自駕 world model，以及 Cosmos-Drive-Dreams（提供 RDS-HQ 資料集脈絡）與同期的 Waymo World Model 作為比較基準。在即時串流影片擴散技術上，OmniDreams 直接採用 Self Forcing 與 CausVid 的訓練-測試落差橋接技術，以及 DMD 蒸餾方法；在閉環模擬基礎設施方面，論文將 OmniDreams 定位為在 Waymax、CARLA、MetaDrive、DriveArena、HUGSIM 等既有系統之外開啟「第四層感知擬真度」。論文也將其 WAM 後期訓練結果與機器人操作領域「以 world model 為基礎的 policy」研究（如本頁 Robot-Specific Action-Conditioned World Models 主題下的多篇論文）相互呼應，驗證同一範式從機器人操作遷移至自駕領域同樣有效。
- 判斷值得 survey 的程度：高。OmniDreams 代表 NVIDIA 將 Cosmos 平台延伸至「即時閉環自駕模擬器」的重要里程碑，其 Self Forcing 蒸餾與漸進式長 context 教師策略、以及將同一骨幹同時用於模擬與 WAM 動作生成的設計，對本頁「World Models for Autonomous Driving」與「Robot-Specific Action-Conditioned World Models」兩個主題都有直接參考價值，後續若有更多閉環評測或第三方驗證，值得持續追蹤。

### Conclusion

- **綜合評價**：OmniDreams 標誌著自駕模擬從「以重建為基礎」邁向「以生成式 world model 為基礎」的關鍵轉折，其工程貢獻（即時速度、多視角一致性、長 rollout 穩定性）與科學驗證（WAM 以五分之一參數超越既有 VLA policy）都相當扎實；作為 NVIDIA 大規模團隊產出的技術報告，訓練資料規模（21,000 小時）與工程複雜度都屬工業級投入，對整個自駕 world model 領域具有指標意義。

- **與其他重要文章的關係**：OmniDreams 與本頁基礎模型 GAIA-1/GAIA-2（Wayve）同屬自駕生成式 world model 譜系，但更進一步強調「即時閉環」與「同一骨幹身兼模擬器與 WAM policy」兩項特性；其 WAM 後期訓練結果也與本頁「Robot-Specific Action-Conditioned World Models」主題下的機器人操作 WAM 研究（如 DreamZero、Cosmos Policy）形成跨領域呼應，顯示 world-action model 範式正同時在機器人操作與自動駕駛兩條路線上收斂。ROCm/AMD 在此領域尚待補強之處：OmniDreams 的 FlashDreams 服務堆疊高度依賴 NVIDIA 特定的工程堆疊（torch.compile + CUDA graphs、ring-attention 的 context-parallel 切分、GB300/H100 叢集），且明確以 NVIDIA Cosmos 擴散骨幹為基礎；若 AMD 欲切入自駕/機器人即時生成式 world model 的推論服務市場，驗證 ROCm 上的串流擴散模型蒸餾（Self Forcing/DMD）與多 GPU context-parallel 切分效能，將是切入此一新興市場區隔的具體技術驗證方向。
