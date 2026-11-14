---
layout: paper
title: "Vision-Language-Delta-Action: Learning Compact Deltas as Actionable Transition Interfaces for Robotic Manipulation"
section: vla
page_id: "2610258740"
permalink: /zh/vla/vision-language-delta-action-learning-compact-deltas-as-actionable-transition-i-2610258740/
---

### Abstract

機器人操作的本質並非單純的「觀測到動作」映射,而是實現任務指定的物理狀態轉變。現有 VLA 方法直接學習觀測到動作的映射,因語意理解與動作執行之間存在巨大鴻溝而施加了沉重的學習負擔;雖然 world-action models(WAMs)透過未來預測改善控制能力,但它們針對完整未來狀態做最佳化,而非僅針對任務相關的變化,因而在靜態外觀或與動作無關的抽象內容上浪費了模型容量。本論文提出 Vision-Language-Delta-Action(VLDA),將完整未來預測重新建構為緊湊的可操作轉變建模(actionable transition modeling)。其核心是引入一個緊湊的 Delta 變數,作為捕捉潛在世界狀態變化的中介決策變數,在視覺語言理解與動作生成之間擔任統一的表徵介面。論文作者來自哈爾濱工業大學(深圳)、百度與深圳河套學院,於 2026 年 10 月 19 日發佈於 arXiv,並將 VLDA 實作於百度開源的 LoongForge 大規模基礎與具身模型訓練框架之中(該框架亦用於 π0.5、GR00T-N1.7、Cosmos3 等知名模型的訓練管線),屬於產業實驗室出品且方法論具有實質創新性的代表作。

### Method

- **要解決的問題**:現有 VLA 模型多半仍遵循觀測到動作的建模方式,將任務相關物件識別、期望物理狀態變化推論、可執行動作序列生成,全部糾纏在單一 policy 內部完成。由於缺乏對任務相關狀態變化的專門建模,policy 必須僅從動作監督訊號中隱式推斷預期的物理轉變,在語意理解與動作執行之間留下巨大的表徵鴻溝。雖然 WAM 透過預測未來觀測、視覺 latent 或動作條件化動態提供額外的時間線索,但它們通常將未來表示為另一個完整狀態,導致任務相關的轉變線索仍與靜態場景內容、動作無關的變化糾纏在一起,且未來預測往往僅作為輔助目標,缺乏能直接引導動作生成的結構化中介變數。

- **Main method**:VLDA 將動作預測問題重新建構為一個理解-轉變-執行(understanding-transition-execution)的閉環。核心是一個低維度的 Delta 介面,透過兩項互補約束學習:(1)Local Transition Filter(LT-Filter)從密集的「現在到未來」視覺差異中萃取稀疏、以操作為中心的轉變證據,抑制靜態場景內容與動作無關的變化,避免 Delta 偏向靜態 patch 重建;(2)Global Transition Anchor(GT-Anchor)以未來演化的粗粒度摘要對 Delta 做正則化,防止轉變建模過度局部化,同時保留狀態變化的整體方向。在此基礎上,Delta-Driven Action Refinement(DDAR)進一步將 Delta 錨定於動作流形(action manifold)之中,透過 Delta-action 對齊,並將其作為結構化種子注入動作去噪流程(action flow),讓動作專家(action expert)基於此轉變條件,將種子精煉為可執行的動作序列。整套系統採兩階段最佳化(two-stage optimization),並以百度 LoongForge 開源框架的模組化、分散式基礎設施實現訓練。

- **和以往方式的差異**:既有 VLA 方法將語意理解、狀態變化推論與動作生成全部糾纏於單一 policy,未提供專門的轉變表徵;既有 WAM 方法雖嘗試以未來預測彌合此鴻溝,卻將未來建模為「另一個完整狀態」,使任務相關轉變線索與靜態外觀、動作無關變化糾纏,且未來預測通常只是輔助目標而非直接可操作的介面。VLDA 的關鍵差異在於:不追求預測完整未來狀態,而是用一個選擇性(selective)、預測性(predictive)、可操作性(actionable)的緊湊轉變介面取而代之——它只萃取任務相關的稀疏變化、同時與未來演化的整體方向保持一致、並直接錨定於可執行動作流形。消融實驗證實,以 Delta 建模取代「完整未來預測(Full-Future Prediction)」可將 LIBERO 平均成功率從 97.8% 提升到 98.5%,驗證了狀態變化建模比完整未來預測更適合做為動作介面。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示 VLDA 的動機與範式比較,說明機器人操作主要由稀疏的任務相關狀態變化所主導,多數視覺內容保持靜態,而 VLDA 從現在到未來的轉變中學習緊湊 Delta,作為引導動作精煉的可操作介面,形成理解-轉變-執行閉環;第二張圖呈現既有觀測到動作與完整未來預測範式的侷限,對比 VLDA 的轉變介面設計動機。

![Figure]({{ site.baseurl }}/assets/images/2610.25874_vlda_teaser.png)

_Figure 1: VLDA 動機與範式比較——機器人操作由稀疏任務相關狀態變化主導,VLDA 學習緊湊 Delta 作為可操作轉變介面,形成理解-轉變-執行閉環_

![Figure]({{ site.baseurl }}/assets/images/2610.25874_vlda_intro.png)

_Figure 2: 既有觀測到動作與完整未來狀態預測範式的侷限性說明,對照 VLDA 的轉變介面設計動機_

### Result

- **主要增強部分**:在 LIBERO 標準基準上,VLDA 達到 98.5% 的平均成功率,相較 π0.5 backbone 在 Spatial(+1.0)、Object(+1.4)、Goal(+1.4)、Long(+2.8)各子任務上均有提升,超越包括 InternVLA-M1、GR00T-N1、OpenVLA-OFT、VLA-Adapter、UniVLA、CronusVLA 在內的多個近期方法,建立新的 SOTA。在 LIBERO-Plus 零樣本泛化評測上,VLDA 達到 84.5% 平均成功率,超越 π0.5 backbone 10.9 點、超越最強基線 GuidedVLA 9.1 點,在更具挑戰性的 Long 任務套件上差距擴大至 13.4 與 12.1 點。在 RoboTwin 2.0 的零樣本困難模式評測中,VLDA 達到 62.9% 平均成功率,較 π0.5 backbone 提升 20.2 點,於全部 10 項任務中排名第一,在複雜狀態轉變任務(如 Put Bottles Dustbin +46、Stacking Three +30、Place Dual Shoes +27、Open Microwave +27)上增益尤其顯著。在真實世界四項長 horizon 任務上(GALAXEA R1 Lite 與 AgileX Cobot Magic 平台),VLDA 達到 73.0% 的最佳表現,較 π0.5 提升 17.0 點;在測試空間泛化能力的 Basket Relocation 任務中(隨機化 mat 位置、分佈外目標位置),VLDA 保留 72% 成功率(+24),顯示對未見佈局具有穩健適應能力。

- **結果是否公正**:作者透過詳盡的消融實驗誠實呈現了各模組的獨立貢獻——將 Delta 建模替換為完整未來預測會使 LIBERO 表現從 98.5% 降至 97.8%,從起始就聯合最佳化各模組(而非分階段)則降至 97.3%,這些對照清楚界定了 Delta 建模與分階段訓練策略各自的實際效益邊界,而非籠統歸功於整體架構。LT-Filter 與 GT-Anchor 的個別消融也顯示兩者對真實世界任務成功率的貢獻程度不同(單用 LT-Filter 在 Basket Relocation 達 68%,單用 GT-Anchor 達 60%,兩者合併達 72%),這種細粒度的歸因分析增加了論文的可信度。

### Limitation

- **已知 limitation**:作者在附錄討論部分指出三項未來工作方向:(1)對無關視覺動態的敏感性(Sensitivity to Unrelated Visual Dynamics)——Delta 表徵仍可能受到與任務無關的場景動態干擾;(2)固定 horizon 的狀態轉變建模(Fixed Horizon State Transition Modeling)——目前 Delta 建模基於固定的轉變時間窗口,未探討可變 horizon 的適應性;(3)跨具身轉變遷移(Cross-Embodiment Transition Transfer)——目前驗證侷限於特定機器人平台,尚未系統性驗證 Delta 介面在不同具身形態間的可遷移性。

- **從 result 來看的弱項**:真實世界實驗僅在兩個機器人平台(GALAXEA R1 Lite、AgileX Cobot Magic)上收集了 100-150 筆示範、每任務每平台 25 次評測試驗,樣本規模相對有限;論文也未探討 Delta 介面在更多樣化真實環境光照、背景、物件類型組合下的穩健性邊界,僅在 LIBERO-Plus 的 Camera/Light/Background/Noise 四種擾動類型上做了系統性驗證。

### Related work

- VLDA 與本頁「World Models Integration」主題(World Action Models、Do World Action Models Generalize Better than VLAs、In-Context World Modeling)同樣處理「VLA vs. WAM」的張力,但切入點明確不同:既有 WAM 論文多半驗證「預測完整未來狀態是否優於直接動作預測」,而 VLDA 的核心論點是兩者皆非最優解——完整未來預測浪費容量在任務無關內容上,直接動作預測則缺乏中介轉變表徵;其提出的「緊湊 Delta 轉變介面」可視為介於兩個既有範式之間的第三條路線,此定位使其成為「World Models Integration」主題下一個具有明確差異化價值的新興分支。
- 判斷值得 survey 的程度:高。VLDA 出自百度 LoongForge 訓練框架(該框架已被用於訓練 π0.5、GR00T-N1.7、Cosmos3 等業界知名模型,顯示其工程基礎設施的產業級成熟度),且在三個模擬基準(LIBERO、LIBERO-Plus、RoboTwin 2.0)與兩個真實機器人平台上做了全面驗證,消融實驗設計嚴謹(涵蓋轉變範式、LT-Filter/GT-Anchor、DSAF、DAMG 等模組的逐一拆解),對於理解「中介轉變表徵」這一介於 VLA 與 WAM 之間的新興設計空間具有重要參考價值。

### Conclusion

- **綜合評價**:VLDA 針對「VLA 直接動作預測 vs. WAM 完整未來預測」這組既有張力,提出了一個簡潔但經過充分驗證的第三條路線——緊湊可操作 Delta 轉變介面。其核心創新在於明確區分「任務相關的稀疏轉變」與「完整未來狀態」,並透過 LT-Filter/GT-Anchor 雙重約束、DDAR 動作流形錨定機制,將這一表徵設計轉化為跨模擬與真實平台均可驗證的效能增益,尤其在長 horizon 一致性與分佈外泛化上的提升幅度相當顯著(RoboTwin 2.0 困難模式 +20.2 點、真實世界 +17.0 點)。

- **與其他重要文章的關係**:VLDA 可與本頁「Architecture Paradigms」主題下聚焦動作生成機制的論文(如 Discrete Diffusion VLA、AsyncVLA)互補對照——後者關注「動作如何被解碼」,VLDA 則關注「動作生成前應建立何種中介表徵」,兩者分屬動作生成管線的不同環節。ROCm/AMD 在此領域尚待補強之處:VLDA 的訓練管線建構於百度 LoongForge 框架之上,實驗以 8 張 NVIDIA A800-SXM4(80GB)GPU 完成訓練、真實世界推論則使用單張 32GB 消費級 GPU 部署,顯示其訓練與推論基礎設施預設鎖定於 NVIDIA CUDA 生態;隨著 LoongForge 這類大規模具身模型訓練框架逐漸成為業界共享基礎設施(已承載 π0.5、GR00T-N1.7、Cosmos3 等多個重量級模型),若 AMD 欲切入下一代具身 AI 訓練基礎設施市場,驗證此類分散式二階段最佳化訓練管線在 ROCm 上的相容性與效能表現,將是具體且有產業急迫性的生態系拓展方向。
