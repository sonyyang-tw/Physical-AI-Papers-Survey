---
layout: paper
title: "APT: Action Expert Pretraining Improves Instruction Generalization of Vision-Language-Action Policies"
section: vla
page_id: "2606123660"
permalink: /zh/vla/apt-action-expert-pretraining-improves-instruction-generalization-2606123660/
---

### Abstract

連續動作型 VLA policy(以生成式 action expert 搭配預訓練 VLM)在操作任務上已有亮眼表現,但對分佈外(OOD)語言指令的泛化能力仍然薄弱。作者指出根本原因在於 VLA 資料存在結構性失衡——每條軌跡的大量視覺-動作影格僅對應單一語言指令,使得視覺-動作的多樣性遠高於語言,讓隨機初始化的 action expert 傾向學會「視覺捷徑」而非真正依賴語言。離散動作範式可透過視覺-語言共訓練緩解此問題,但連續動作的 action expert 缺乏對應的保護機制,且來自捷徑學習的噪聲梯度會進一步污染 VLM 骨幹的語言表徵。作者從貝氏觀點出發,將 policy 分解為與語言無關的 Vision-Action(VA)先驗與語言條件化的 VLA 概似函數,提出 APT(Action Expert PreTraining)——一套強調「動作專家預訓練」的兩階段訓練方法。第一階段,action expert 僅以凍結 VLM 的視覺 token 為條件,在視覺-動作配對資料上預訓練出 VA 先驗;第二階段,引入語言 token 並以逐層閘控融合機制聯合微調整個 policy。APT 適用於主流連續動作 VLA 架構(包含 π 系列與 GR00T 風格架構),論文已於 2026 年 10 月 2 日修訂版確認獲 CoRL 2026 接受,作者團隊來自浙江大學、RobbyAnt、浙江人形機器人創新中心。

### Method

- **要解決的問題**:實現開放世界機器人操作的關鍵前提是 policy 能真正理解並依據語言指令行動,而非僅將指令當作任務識別碼。既有研究已指出 VLA 資料存在結構性失衡:一條含 T 個時間步的軌跡,視覺-動作配對的多樣性是語言多樣性的至少 T 倍,使得隨機初始化的連續 action expert 在訓練時傾向學習「僅憑視覺線索預測動作」的捷徑,繞過語言依賴。這類捷徑進一步產生噪聲梯度,污染原本具備良好語言能力的 VLM 骨幹表徵,導致近期工作(如 π0.5 的 Knowledge Insulation)選擇直接阻斷 action expert 到 VLM 的梯度回傳,但此作法僅能維持既有語言跟隨能力,無法真正改善對 OOD 指令與組合任務的泛化。

- **Main method**:APT 將 VLA policy 依貝氏公式分解為 π(a|v,ℓ) ∝ π^p(a|v) · L(ℓ|v,a),其中語言無關的 Vision-Action(VA)先驗 π^p(a|v) 可直接在原始 VLA 資料集中天然平衡的視覺-動作配對上訓練——每個視覺影格都對應唯一的動作標註,不存在語言失衡問題。訓練分兩階段進行:Stage 1(VA 先驗預訓練)僅啟動 action expert 一半的注意力層,語言 token 從自注意力計算中完全遮蔽,讓網路退化為純粹的視覺-動作函數,在此階段學習涵蓋多樣操作行為的動作流形;Stage 2(VLA 對齊)將 action expert 從 N/2 層擴展至 N 層,在原有層之間插入新的交錯注意力層,並移除語言遮罩,讓全部 token 參與區塊式因果自注意力——原有層由 Stage 1 checkpoint 初始化以繼承 VA 先驗,新插入層則負責引入語言條件,整個 N 層在完整預訓練資料集上聯合最佳化。action expert 採用新穎的逐層閘控融合設計:以 Qwen3-VL 為 VLM 骨幹,從中等間隔採樣 N 個中間層特徵,透過可學習純量閘門(經 sigmoid 函數)調變每層 VLM 特徵對 action expert 對應層的影響程度,使 action expert 能同時吸收淺層空間特徵與深層語意特徵,而不會對已學得的 VA 先驗造成劇烈擾動。

- **和以往方式的差異**:與直接聯合訓練(如 OpenVLA、π0)或僅靠 Knowledge Insulation 阻斷梯度(如 π0.5)的既有作法不同,APT 從「初始化」這一根本環節介入問題——既有方法要嘛任由隨機初始化的 action expert 在失衡資料上形成捷徑,要嘛僅被動切斷其對 VLM 的負面梯度影響,但 APT 直接讓 action expert 在平衡資料上預先習得連貫的視覺-動作先驗,再以語言條件精修。消融實驗證實,單純加入 Knowledge Insulation 而不做兩階段預訓練並無明顯增益,顯示「阻斷梯度」本身並非解方;唯有結合兩階段預訓練才能超越 π0.5,直接將增益歸因於動作專家預訓練本身。此外,相較於同期的 LangForce(以互資訊最大化強制語言依賴),APT 在「不改變語言但改變物體佈局」(Pos 擾動)與「改變語言對應新任務」(Task 擾動)兩類測試上取得更均衡的表現,顯示先建立良好視覺運動先驗再精修語言依賴,優於直接強化動作-語言耦合可能犧牲視覺適應力的作法。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示 APT 的核心效果:action expert pretraining 讓 policy 有效跟隨指令;第二張圖展示兩階段訓練總覽,呈現 Stage 1 僅以視覺 token 為條件預訓練 VA 先驗、Stage 2 引入語言 token 聯合微調整個 policy 以將預訓練動作分佈與任務指令對齊的完整流程。

![Figure]({{ site.baseurl }}/assets/images/2606.12366_teaser.png)

_Figure 1: Action expert pretraining (APT) 讓 policy 有效跟隨語言指令_

![Figure]({{ site.baseurl }}/assets/images/2606.12366_method.png)

_Figure 2: APT 總覽——Stage 1 僅以視覺 token 預訓練 VA 先驗,Stage 2 引入語言 token 聯合微調整個 policy,將預訓練動作分佈與任務指令對齊_

### Result

- **主要增強部分**:在 LIBERO-PRO 基準上(涵蓋 Spatial/Object/Goal/Long 四類任務各自的 Pos/Task 兩種擾動),OpenVLA 與 π0 在兩類擾動下成功率均為 0%,確認直接聯合訓練會完全崩潰為視覺捷徑;π0.5 透過 Knowledge Insulation 在 Pos 擾動上有所恢復,但 Task 擾動(真正的 OOD 語言泛化)上仍接近零;LangForce 在 Task 擾動上優於 π0.5,但在 Pos 擾動上大幅退化。APT 平均成功率達 19%,APT(Ft VLM,即聯合微調 VLM)進一步提升至 27%,同時在 Pos 與 Task 兩類擾動上都優於 π0.5 與 LangForce,顯示兩階段訓練能同時解決視覺適應與語言泛化的權衡。在 Rigid Object Pick-Place 基準的四個難度級別(Seen Object 至 Unseen Object & Unseen Environment)上,結合 Knowledge Insulation、兩階段訓練與聯合微調 VLM 的 APT 變體取得最佳結果(SO 98%、UO 84%、UC 92%、UOUE 58%),全面優於 π0.5(SO 84%、UO 70%、UC 86%、UOUE 50%)。真實世界評測中,APT 在 Pick-Place 任務(110 次試驗)與 Clutter Pick-Place 任務(80 次試驗)各 OOD 難度級別上均優於 π0.5,在組合任務評測中,π0.5 在「任務鏈接」(單一句子同時指定兩個任務)設定下幾乎完全失敗(過度執行第一個任務,無法轉換到第二個任務),而 APT 能成功無需顯式任務切分地依序執行鏈接任務。

- **結果是否公正**:論文在 OpenVLA、π0、π0.5、LangForce、CaP-X 等具代表性的既有連續/離散動作 VLA 基線與 agent 框架之間進行系統性比較,並透過四組設計維度(KI、2-Stage、Ft VLM)的消融實驗逐一拆解各技術元件的獨立貢獻,避免將增益籠統歸因於整體方法;同時在模擬(LIBERO-PRO、Rigid Object Pick-Place)與真實世界(Pick-Place、Clutter Pick-Place、組合任務)兩類環境下重複驗證,並額外測試方法在 π 風格與 GR00T 風格兩種主流架構上的可遷移性,顯示作者對結果穩健性有相對嚴謹的交代。

### Limitation

- **已知 limitation**:作者在結論明確指出,目前設計未明確建模長程記憶,限制了需要追蹤多步驟進度任務上的泛化能力;此外,評測範疇聚焦於桌面操作任務,尚未延伸至移動式操作或全身移動操作,這些方向留待未來工作探索。

- **從 result 來看的弱項**:在 LIBERO-PRO 的 Goal-Pos 子集上,APT 的表現低於 π0.5,作者分析指出 APT 多數情況能正確跟隨語言指令,但在該子集特別強調的「避障」能力上可能失誤,顯示方法對語言理解的強化不必然同步轉化為所有子任務維度(如空間避障)的能力提升;此外,真實世界組合任務的失敗案例顯示,APT 偶爾會在當前任務尚未完全完成前就提前推進到下一個任務,或將放置目標與視覺相似的干擾物混淆,顯示長程組合任務的精細控制仍有改進空間。

### Related work

- APT 與本頁「Architecture Paradigms」主題下已收錄的多篇論文(如 Discrete Diffusion VLA、AsyncVLA)同屬「改善 VLA 動作生成機制」範疇,但切入角度不同:既有收錄論文多聚焦於動作解碼機制本身(離散化、flow-matching 步數壓縮等),而 APT 聚焦於動作生成「初始化」環節本身——其核心洞察是將貝氏分解應用到預訓練策略設計上,而非修改動作解碼的底層數學形式,此一視角與本頁尚未收錄的 BayesVLA(APT 作者前作,提出貝氏分解診斷但凍結先驗、泛化受限於異質資料集)形成直接的方法論承接與延伸關係。
- APT 的「阻斷梯度是否必要」這一問題與既有收錄於「Efficiency」主題下聚焦推論效能的論文(Fast-VLA、REACT)視角互補:後者關注如何讓既有 VLA 架構跑得更快,APT 則關注如何讓訓練過程本身產生更具語言泛化能力的模型,兩者分屬「部署效率」與「訓練方法論」的不同改進維度,但同樣體現 VLA 領域正從「單純擴大規模」轉向「更精細的訓練流程設計」的趨勢。
- 判斷值得 survey 的程度:高。APT 已確認獲 CoRL 2026 接受,核心貢獻——將貝氏分解從診斷工具轉化為可操作的兩階段訓練方法,並驗證其可遷移至 π 與 GR00T 兩種主流架構——具備清晰的方法論創新性與廣泛適用性;論文在模擬與真實世界、OOD 語言與組合任務等多個維度上提供一致且有說服力的實驗證據,是近期少數從「資料失衡根源」而非「架構修補」切入 VLA 語言泛化問題的工作。

### Conclusion

- **綜合評價**:APT 從貝氏分解視角出發,精準定位連續動作 VLA policy 語言泛化失敗的根源在於 action expert 缺乏平衡資料預訓練,提出的兩階段訓練方法簡潔且具普適性,在模擬與真實世界評測中均取得一致增益,並透過系統性消融證明「動作專家預訓練」而非「阻斷梯度」才是改善語言泛化的關鍵機制。其「可遷移至主流 VLA 架構」的特性使其具備良好的工程實用性,而非僅針對特定架構的修補手法。

- **與其他重要文章的關係**:APT 可與本頁「Data, Benchmarks & Simulation」主題下的 LIBERO-Para(揭露 LIBERO 對指令改寫的脆弱性)互為補充——後者揭示問題的存在與嚴重性,APT 則提出針對性的訓練方法學解方,兩者共同勾勒出「診斷語言泛化缺陷→針對性訓練介入」的研究路徑。ROCm/AMD 在此領域尚待補強之處:APT 的兩階段訓練涉及在同一網路中動態切換注意力層遮罩模式與逐層插入新注意力層,這類訓練期間的動態網路拓撲調整(而非靜態架構的前向推論)對底層深度學習框架的計算圖彈性與記憶體管理提出要求;隨著「分階段預訓練搭配架構擴展」這類訓練策略在 VLA 領域逐漸普及,驗證此類動態訓練管線在 ROCm 軟體棧上的相容性與訓練效率,是值得關注的生態系拓展方向。
