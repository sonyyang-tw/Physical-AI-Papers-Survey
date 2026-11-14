---
layout: paper
title: "FR-VLA: Implicit Force Reasoning VLA for Contact-Rich Manipulation"
section: vla
page_id: "2610259810"
permalink: /zh/vla/fr-vla-implicit-force-reasoning-vla-for-contact-rich-manipulation-2610259810/
---

### Abstract

將力覺整合進 Vision-Language-Action(VLA)模型,並非單純將力矩量測編碼為額外模態,而是要決定物理互動何時、以多強的程度影響機器人動作生成。既有的力覺感知 VLA 通常透過固定路徑注入力訊號,並未明確判斷該力訊號對當前動作是否相關。作者提出 FR-VLA,一套 Vision-Language Force-Reasoning Model,以可學習的力查詢 token(force query tokens)從視覺語言情境中推導出力許可訊號(force admission signal),並用此訊號調節一條外部 tokenized 力路徑以生成動作。在涵蓋兩個機器人平台的五項接觸豐富操作真實世界實驗中,FR-VLA 在六個評測階段皆取得最高成功率,軌跡視覺化亦顯示其力許可訊號會隨互動階段而變化。論文已於 2026 年 10 月 19 日發佈於 arXiv,並已確認獲 CoRL 2026 接受,作者團隊來自新加坡南洋理工大學(NTU)電機與電子工程學院,以及新加坡科技研究局(A*STAR)旗下新加坡製造技術研究院(SIMTech)。

### Method

- **要解決的問題**:現代 VLA 透過預訓練 VLM 骨幹,將機器人動作生成植基於視覺觀測與語言指令,已成為有效的通用型 policy。然而接觸豐富操作(如插入、組裝、擦拭、鎖緊)暴露出這種視覺語言基礎的侷限:插入、組裝等任務中的互動狀態往往僅能從影像中部分觀測,使力覺回饋成為精密操作不可或缺的訊號。力覺回饋的重要性會隨任務階段與接觸狀態演變而改變,這促使作者思考:如何讓 policy 利用視覺語言情境,動態決定力覺回饋何時、以多強程度影響動作生成?既有力覺感知 VLA 架構主要差異在於力訊號注入的位置——注入 VLM token 串流可能在高維視覺語言表徵中稀釋低維力矩訊號,而將力調節移至 action expert 雖避免此表徵失衡問題,卻繞過了 VLM 推斷任務進展與互動階段的核心表徵空間。兩種做法都只提供「力的曝光」而非「力的接地」:policy 能對量測到的力矩變化做出反應,卻未被明確監督該在何時決定讓力影響動作生成。

- **Main method**:FR-VLA 將力覺整合明確框架為一個模態接地(modality grounding)問題。其核心為 Implicit Force Reasoning Module:力查詢 token 作為 VLM 內部介面推斷力許可程度,但本身不攜帶量測到的力矩數值——它們被優化以從視覺語言情境推斷互動階段狀態,而非重建力量測值或直接預測動作,這使 VLM 得以獲得力覺感知能力,同時將原始物理回饋保留在 token 串流之外。力查詢狀態推斷出一個階段機率分佈,再據此以 entropy 加權的 tanh 函式推導出一個帶正負號的力許可訊號(normalized entropy 越高,代表階段不確定性越大,調整幅度就越趨近於零)。訓練時,作者從機器人 6 維力矩量測與夾爪狀態離線產生階段標籤(以夾爪開合事件切分示範片段,再依據相對於非接觸參考值的力偏移偵測接觸事件),為階段預測提供輔助監督。在動作側,Force Tokenizer Module 以凍結的 VQ-VAE 將短期力矩歷史分派至重複出現的接觸動態模式碼本,再透過 FiLM 機制產生尺度與偏移參數調製原始力 token,使動作模型既能捕捉重複接觸模式、又保留細緻的力矩資訊。力許可最終透過一個仿照 VLA-Adapter 動作橋接架構的 admission-conditioned attention 機制實現,讓力查詢推斷出的許可訊號直接調節動作生成過程中對力訊號的注意力強度。

- **和以往方式的差異**:既有力覺感知 VLA(如將力矩注入 VLM token 串流,或將力調節移至 action expert)皆只提供「力的曝光」而非「力的接地」——policy 可以對測得的力矩變化作出反應,但沒有被明確監督何時該讓力訊號影響動作決策。FR-VLA 的關鍵差異在於明確分離「力相關性判斷」與「力表徵」:力查詢 token 只負責估計力該被許可的程度,Force Tokenizer 則負責在動作側表徵量測到的力矩。消融實驗進一步驗證,相較於單純依測得力矩幅度門控(wrench magnitude gating)的簡化基線,FR-VLA 的階段接地力許可機制在 Gear Assembly 任務上達到 90% 成功率,遠高於幅度門控基線的 70%,顯示力矩幅度本身不足以反映力對動作選擇的相關性——無論是受限插入時的高力矩,或修正動作時逐漸下降的力矩,都可能具有決策相關性,而非只有力矩峰值才重要。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示 FR-VLA 的整體概念對比:既有力覺感知 VLA 設計將力直接注入 VLM token 串流或 action expert,而 FR-VLA 的 Switch Cable Connection 軌跡範例則展示同步的相機觀測、六維力矩量測與力許可訊號如何隨任務階段演變;第二張圖展示 FR-VLA 的詳細架構,呈現 Implicit Force Reasoning Module 如何從視覺語言情境推斷力許可訊號,再透過 Force Tokenizer 與 admission-conditioned attention 將該訊號整合進動作生成流程。

![Figure]({{ site.baseurl }}/assets/images/2610.25981_fr-vla_teaser.png)

_Figure 1: FR-VLA 概念總覽——既有力覺感知 VLA 設計將力訊號注入 VLM token 串流或 action expert,FR-VLA 的 Switch Cable Connection 範例展示相機觀測、六維力矩與力許可訊號隨任務階段的同步演變_

![Figure]({{ site.baseurl }}/assets/images/2610.25981_fr-vla_pipeline.jpg)

_Figure 2: FR-VLA 架構——Implicit Force Reasoning Module 從視覺語言情境推斷力許可訊號,經 Force Tokenizer 與 admission-conditioned attention 調節動作生成中的力訊號貢獻程度_

### Result

- **主要增強部分**:FR-VLA 在配備 UR5e 與 UR3e 兩台 Universal Robots 機械臂、各自搭載第三視角與手腕視角 Intel RealSense 相機的真實世界評測中,涵蓋 Gear Assembly、Switch Cable Connection(含視覺遮蔽的側邊電源連接器階段)、Curved Surface Cleaning、Screw Tightening、Seat Belt Buckle Insertion 五項接觸豐富任務,在全部六個評測階段皆取得最高成功率,平均成功率 58.3%,較最強基線高出 20.8 個百分點。主要增益來自力訊號僅在正確任務情境下才具資訊性的階段——例如 Switch Cable Connection 中視覺證據在側邊電源連接器插入階段變得不可靠,此時接觸回饋至關重要,但若 policy 僅被動對接觸瞬間的力矩陡升做出反應則容易卡死而無法恢復,FR-VLA 則依推斷出的互動階段許可力訊號,在真正具資訊性時才利用瞬時接觸線索。在 Screw Tightening 任務中,有效訊號並非力矩絕對幅度,而是對準、嚙合、鎖緊三階段間的轉換,顯示 FR-VLA 透過判斷「何時」該讓力矩動態影響動作生成而非單純依賴力矩幅度而取得改善。

- **結果是否公正**:FR-VLA 與四個基線方法(VLA-Adapter、VLA-Adapter w/F、採用力感知 MoE 融合的 ForceVLA、decoder 端力矩-動作聯合擴散的 TA-VLA)在相同資料與環境條件下進行比較,確保公平性。消融研究進一步拆解了力許可與 Force Tokenizer 各自的貢獻:移除力許可機制使平均成功率從 58.3% 降至 35.0%,移除 Force Tokenizer 則降至 40.0%,兩項消融在全部六個評測階段皆造成成功率下降,支持兩個元件的互補角色。此外,論文報告各任務的階段推斷平衡準確率(介於 80.6% 至 93.7% 之間),顯示大多數階段預測錯誤發生在接觸起始與釋放的邊界附近,這類視覺觀測漸變導致階段邊界難以辨識的區域,提供了額外的透明度而非僅報告單一端到端數字。

### Limitation

- **已知 limitation**:論文明確指出,儘管 FR-VLA 改善了力許可與力表徵,精密操作中的細緻力條件修正動作仍然具有挑戰性。人類示範常利用細微的力變化引導非常小幅的動作調整,但在行為克隆過程中,這類細微動作差異相對於整體軌跡可能被稀釋。作者建議未來工作應引入更結構化的動作側機制(如力敏感殘差頭或聚焦轉變的訓練目標),以提升對細微但決策關鍵的力變化的敏感度,並在更大規模資料集上評估跨多個視覺影格的時序變化是否有助於預判更細緻的力互動狀態。

- **從 result 來看的弱項**:論文的評測任務數量(五項)與每任務示範數(70–90 筆)規模相對有限,且評測平台侷限於兩台 Universal Robots 機械臂,跨機器人形態與更大規模任務集合的泛化能力尚待驗證。此外,階段標籤產生依賴啟發式規則(夾爪開合事件切分、基於自適應參考值的接觸事件偵測),這類規則在不同任務類型下的穩健性,以及其對最終力許可品質的敏感度,仍需更系統性的壓力測試。

### Related work

- FR-VLA 與本頁「Architecture Paradigms」主題下聚焦動作生成機制設計的論文不同,其貢獻聚焦於「額外模態(力覺)何時該接地進入動作生成」這一問題,與現有力覺感知 VLA 工作(如 ForceVLA 的 MoE 融合、TA-VLA 的力矩-動作聯合擴散)相比,FR-VLA 首次明確將「力相關性判斷」與「力表徵」分離為兩個獨立機制,填補了既有方法僅提供「力曝光」而非「力接地」的方法論空白。
- 論文以視覺語言情境驅動動態調節機制的設計精神,與本頁「Architecture Paradigms」主題下的 FocusVLA(以預測未來互動意圖驅動動態視角路由)有相通之處——兩者都透過階段感知訊號調節某一輸入模態對動作生成的貢獻程度,但 FocusVLA 聚焦於多視角視覺路由,FR-VLA 則聚焦於力覺模態的接地問題。
- 判斷值得 survey 的程度:中高。FR-VLA 已確認獲 CoRL 2026 接受,並在兩個真實機器人平台、五項任務上進行嚴謹的真實世界評測與消融研究,其「force admission」機制對理解「如何讓 VLA policy 妥善整合非視覺模態」這一日益重要的子問題具有參考價值,尤其對於 AMD/ROCm 關注的精密製造與組裝應用場景具有實務意義。

### Conclusion

- **綜合評價**:FR-VLA 將力覺整合進 VLA 這一問題重新框架為「模態接地」問題而非單純的感測或融合問題,透過分離力許可與力表徵,在維持量測力矩於動作側路徑的同時,利用視覺語言情境決定力覺回饋何時該影響動作生成。真實世界結果顯示,這種分離確實改善了接觸豐富操作表現,且學習到的力許可訊號遵循任務階段互動機制,而非僅反應瞬時力矩幅度。
- **與其他重要文章的關係**:FR-VLA 可視為本頁「Efficiency」與「Memory, History-Awareness & Long-Horizon Control」主題下強調「讓 policy 具備階段感知能力」這一設計哲學在力覺模態上的延伸應用。ROCm/AMD 在此領域尚待補強之處:FR-VLA 的 Implicit Force Reasoning Module 與 Force Tokenizer 涉及 VQ-VAE 量化、FiLM 調製與 admission-conditioned attention 等多種輕量級、高頻率條件化運算,這類涉及多模態融合的細粒度算子組合,對底層算子函式庫的動態控制流與小型運算核效能提出要求;隨著接觸豐富操作與力覺整合在工業裝配場景的應用日益增加,驗證此類多模態條件化推論管線在 ROCm 軟體棧上的相容性與效能,是值得關注的生態系拓展方向。
