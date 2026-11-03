---
layout: paper
title: "Agentic World Action Models"
section: wm
page_id: "2610301360"
permalink: /zh/wm/agentic-world-action-models-2610301360/
---

### Abstract

近期的 world action model（WAM）為機器人操作提供視覺前瞻與未來預測能力，但缺乏明確的機制支援可組合技能的重複使用；而 agentic robotics 結合以程式碼為基礎的規劃與推理、搭配可重用技能，卻往往缺乏對物理動態的預測性 grounding。本論文提出 AW-0，一套整合程式碼規劃與聯合影片/動作預測的 agentic world action model 框架：將程式碼、未來影片、機器人動作共同建模為統一 mixture-of-transformers 架構下三個耦合的生成流——程式碼專家（code expert）生成參數化的技能常式與控制邏輯，影片與動作專家則生成未來視覺狀態與低階動作指令。程式碼在此扮演雙重角色：既在 world model 內部結構化多步驟預測與控制，也作為後續 agentic 執行階段可重複使用的程式。作者進一步提出一套自動化資料整理管線，為機器人與人類影片軌跡標註對齊的程式，並將重複出現的常式整併為可重用技能庫。在 RoboTwin 2.0 與真實雙臂操作任務上的評測顯示，AW-0 相較 VLA 與 WAM 基線皆有效能提升，同時在語言遵循、語意推理與穩健性上也有所增益。論文由 UC Berkeley、NVIDIA、賓夕法尼亞大學於 2026 年 10 月 21 日發佈於 arXiv，作者群涵蓋 Ken Goldberg、Trevor Darrell（UC Berkeley）與 Linxi "Jim" Fan、Yuke Zhu、Guanzhi Wang（NVIDIA）等業界與學界知名研究者。

### Method

- **要解決的問題**：World Action Model（WAM）透過耦合視覺預測與動作生成，將控制 grounding 於物理世界如何演化的表徵之中，這對需要預判物件運動、接觸與低階動作後果的複雜操作任務尤其重要。然而，預測出的影片與動作片段本身並不能說明一個長 horizon 任務該如何被分解——該呼叫哪些可重用技能、如何參數化、如何跨子任務組合。另一方面，agentic robot 系統雖然能以程式化的方式選擇可重用技能與工具、綁定當前場景、追蹤進度並隨觀測變化重新規劃，卻往往缺乏對真實物理動態的預測性 grounding，也未能利用對世界如何隨機器人動作而改變的學習模型。

- **Main method**：AW-0 將程式碼、未來影片、機器人動作定義為三個耦合的條件生成流，分別描述結構化技能計畫、未來場景動態、連續機器人動作。模型採用 Mixture-of-Transformers（MoT）架構，三個專家（程式碼、影片、動作）各自保有獨立的注意力投影、layer normalization 與 FFN，並透過每層的 masked joint attention 相互溝通；注意力遮罩在各專家內部為雙向、跨專家之間則依「程式碼→影片→動作」的順序呈 block-wise causal。程式碼專家以凍結的 Qwen3-VL ViT 搭配 LLaDA 風格的 masked-token diffusion 處理離散程式碼 token；影片專家以 Cosmos-Predict2.5 初始化的 video DiT 建模 VAE 編碼的未來影格；動作專家則以獨立的 action DiT 生成連續動作片段，影片與動作皆採用 continuous flow matching 訓練。作者並提出一套自動化標註管線：先以 Gemini 3.1 Pro 為少量取樣 episode 撰寫子任務層級的技能程式，再以 Claude Opus 4.8 擔任協調者蒸餾出跨任務通用的技能庫，凍結技能庫後對其餘語料進行快取式重複使用或新程式生成的標註，最終建立可供聯合預訓練使用的程式-影片-動作對齊資料。

- **和以往方式的差異**：既有 WAM 論文（如 DreamZero、τ0-WM）提供視覺前瞻與動作生成的耦合，但未提供明確的技能組合結構；既有 agentic robotics 方法（Code-as-Policies 等）提供程式化的技能結構，卻缺乏對物理動態的預測性 grounding。AW-0 的關鍵差異在於首次將「程式碼即規劃」直接整合進 world action model 的聯合去噪過程之中——程式碼不只是外部呼叫的工具，而是與影片、動作一同在同一個擴散/遮罩去噪迴圈中被生成，使規劃結構能直接引導影片與動作專家的生成內容。此外，論文提出的混合執行策略（hybrid actions）允許系統在「直接執行 action expert 生成的動作片段」與「執行解碼出的程式化技能」之間動態仲裁，這是既有純 VLA 或純 WAM 方法都不具備的部署彈性。

- **關鍵方法圖**：見下方嵌入圖片——第一張圖為 AW-0 整體概覽，展示其如何將程式碼為基礎的規劃與 world action modeling 統一，透過聯合去噪技能程式、未來影片與控制軌跡運作，並以 agentic 管線發掘可重用技能、為機器人與人類示範標註程式；第二張圖展示 AW-0 的 Mixture-of-Transformers 框架細節，呈現程式碼、影片、動作三專家如何分別以離散遮罩擴散與連續 flow matching 聯合去噪。

![Figure]({{ site.baseurl }}/assets/images/2610.30136_aw0_teaser.png)

_Figure 1: AW-0 整體概覽——統一程式碼規劃與 world action modeling，聯合去噪技能程式、未來影片、控制軌跡，並以 agentic 管線發掘可重用技能_

![Figure]({{ site.baseurl }}/assets/images/2610.30136_aw0_method.png)

_Figure 2: AW-0 Mixture-of-Transformers 框架——程式碼、影片、動作三專家分別以離散遮罩擴散（程式碼）與連續 flow matching（影片、動作）聯合去噪_

### Result

- **主要增強部分**：在 RoboTwin 2.0 的 Clean 與 Random 兩種設定下（50 個任務、每任務 50 次 rollout 平均），AW-0 達到 80.8%（Clean）與 20.6%（Random）成功率，平均 50.7%，優於 π0.5（平均 41.3%）、DreamZero（平均 25.6%）、EgoScale（平均 14.5%）等基線；混合執行模式（AW-0 hybrid）在 Random 設定下達到 29.2% 成功率，為所有方法中最高，顯示程式化技能執行在分佈偏移情境下具有額外的穩健性增益。在涵蓋平行夾爪與靈巧手兩種具身形態的 8 項真實世界雙臂操作任務上，AW-0 同樣超越 π0.5、EgoScale、DreamZero 等基線，且在語言遵循與語意推理能力上展現額外增益。消融實驗（Figure 5、Table 3、Table 4）進一步拆解了「程式碼專家」與「注意力結構」、「視覺條件化方式」、「程式碼生成範式」各自的獨立貢獻。

- **結果是否公正**：作者在模擬（RoboTwin 2.0）與真實世界（8 項任務、2 種具身形態）雙軌評測中，皆與四個具代表性的強基線（π0.5、EgoScale、DreamZero、WLA）直接比較，並提供詳盡的消融實驗拆解程式碼專家、注意力結構、視覺條件化、程式碼生成範式各自的效益邊界。作者也誠實呈現混合執行模式的權衡——在 Clean 設定下混合模式成功率（63.1%）略低於純 AW-0（80.8%），顯示程式化技能執行雖提升 Random 設定下的穩健性，卻並非在所有情境下都絕對優於直接動作生成，這種對取捨邊界的清楚揭露增加了論文的可信度。

### Limitation

- **已知 limitation**：作者在附錄 L 明確列出三項限制：(1)「程式 grounding 與技能覆蓋」——程式碼流的規劃品質高度依賴自動標註的準確性與技能庫覆蓋範圍，生成的程式可能選對技能卻填入錯誤參數，語法有效性並不保證執行正確性；(2)「預測穩健性與混合執行的權衡」——結構化規劃雖提升 WAM 效能，卻未能完全消除對視覺分佈偏移的敏感性，混合執行雖提升 RoboTwin 隨機化設定下的穩健性，卻會降低乾淨設定下的效能，這反映出目前僅依驗證有效性、而非估計相對於直接動作片段的優勢來做仲裁的侷限；(3)「邁向持續 agentic 學習」——真實世界的混合評測因缺乏靈巧手的 code-as-policy 系統而僅限於 YAM 平台，且系統目前並不會從自身互動中線上學習。

- **從 result 來看的弱項**：預訓練資料規模相對有限（約 2,000 小時 YAM 機器人資料與 1,000 小時第一人稱人類操作資料），技能庫僅涵蓋 50 個技能條目（YAM 23 個、人類示範 27 個），技能覆蓋的廣度與真實世界長尾操作任務的多樣性相比仍有落差；Random 設定下的絕對成功率（AW-0 最佳為 29.2%）顯示即便加入程式化規劃結構，分佈外穩健性仍是一個尚未解決的核心挑戰。

### Related work

- AW-0 與本頁「Robot-Specific Action-Conditioned World Models」主題下已收錄的多篇論文（DreamZero、τ0-WM、Pelican-Sim、GE-Act 2.0）同屬「動作條件化世界模型」範疇，但切入點明確不同：既有論文聚焦於世界模型本身的架構設計、資料規模化或跨具身泛化，而 AW-0 的獨特貢獻在於首次將「程式碼即規劃」整合進 WAM 的聯合去噪過程，使程式化技能規劃與影片/動作預測在同一生成迴圈中相互引導，填補了「WAM 提供物理 grounding 但缺乏技能組合結構」與「agentic robotics 提供技能結構但缺乏物理 grounding」之間的方法論空白。其影片專家初始化自 NVIDIA Cosmos-Predict2.5，與本頁已收錄的 Cosmos Policy、DreamZero 同屬「以 Cosmos 系列影片基礎模型為骨幹」的技術譜系，可視為 NVIDIA 在「影片模型即 policy」路線上持續擴展的最新進展。
- 判斷值得 survey 的程度：高。AW-0 由 UC Berkeley、NVIDIA、賓夕法尼亞大學聯合發表，作者群涵蓋 Ken Goldberg、Trevor Darrell、Linxi "Jim" Fan、Yuke Zhu 等機器人學習領域具高度影響力的研究者，在模擬與真實世界雙軌評測中均展現具競爭力的效能提升，並開源專案頁面；其「程式碼-影片-動作」三流聯合生成的架構設計對於理解「如何讓 world action model 具備可組合技能結構」這一新興研究方向具有重要參考價值。

### Conclusion

- **綜合評價**：AW-0 針對 WAM 與 agentic robotics 兩條此前平行發展的技術路線——前者提供物理動態的預測性 grounding、後者提供可組合的技能規劃結構——提出了一個將兩者統一在同一生成框架內的具體實現。其核心創新在於讓程式碼規劃與影片/動作預測透過聯合去噪相互引導，而非僅將程式碼作為外部呼叫的獨立模組，並透過自動化標註管線解決了程式-軌跡對齊資料稀缺的實務瓶頸，在模擬與真實世界評測中均取得具說服力的效能提升。

- **與其他重要文章的關係**：AW-0 可與本頁「World Models as Data Engines」主題下聚焦資料生成與標註自動化的論文互補對照，其自動化程式標註管線（結合 Gemini 3.1 Pro 撰寫技能程式、Claude Opus 4.8 擔任協調者蒸餾技能庫）也呼應了近期「以大型語言模型作為資料標註引擎」的趨勢。ROCm/AMD 在此領域尚待補強之處：AW-0 的影片專家建構於 NVIDIA Cosmos-Predict2.5 之上，程式碼專家則初始化自 SDAR-1.7B 並搭配凍結的 Qwen3-VL 視覺塔，整體訓練管線深度綁定 NVIDIA 的 Cosmos 系列基礎設施與 CUDA 生態；隨著「程式碼-影片-動作」聯合生成逐漸成為 agentic WAM 研究的新興範式，若 AMD 欲切入此一融合規劃與物理 grounding 的下一代機器人基礎模型賽道，驗證 Mixture-of-Transformers 跨模態聯合去噪架構在 ROCm 軟體棧上的訓練與推論相容性，將是具體且有產業急迫性的生態系拓展方向。
