---
layout: paper
title: "From Pixels to Actions: Towards Native Vision-Language-Action Policies"
section: vla
page_id: "2611069180"
permalink: /zh/vla/from-pixels-to-actions-towards-native-vision-language-action-policies-2611069180/
---

### Abstract

現有 VLA 模型普遍建立在一個簡單前提上:感知先由視覺編碼器壓縮,動作推理之後才開始。然而操作任務的成敗,往往繫於這種抽象過程中最容易流失的視覺訊號——局部幾何、邊界、深度、細微狀態變化。這引出一個根本性問題:動作 policy 應該繼承一個固定的視覺終點,還是直接存取演化中的視覺運算?作者提出 NEO-VLA,一個結構上完全無編碼器(encoder-free)的 VLA 框架:影像由輕量級 patch 卷積層 tokenize,並與語言在整個 backbone 中共同演化,使 flow-matching 動作專家得以從不同深度的指令條件化視覺表徵中汲取資訊。這個簡單改動揭露了一致的模式——在受控比較下原生架構優於編碼器式架構;完整微調縮小但未能消除此差距,單純擴大模型規模也無法彌補;更令人意外的是,逐層探測顯示動作關鍵訊號往往在最終視覺表徵形成之前就已達到峰值。論文於 2026 年 11 月 4 日首次發佈於 arXiv(2026 年 11 月 9 日修訂至 v3),作者團隊來自新加坡南洋理工大學 S-Lab、商湯科技研究院(SenseTime Research)與 Ropedia,通訊作者為劉子緯(Ziwei Liu)教授。

### Method

- **要解決的問題**:主流 VLA 模型(如 OpenVLA、π0、GR00T)普遍沿用「預訓練視覺編碼器(CLIP、SigLIP、DINOv2)先將影像壓縮為固定特徵,再交給語言 backbone 與動作模型」的架構慣例。這個介面只暴露編碼器的最終輸出,卻隱藏了產生該輸出的視覺運算層級。近期證據顯示這種分離可能限制具身控制表現:視覺處理品質是 VLA 效能的關鍵瓶頸,視覺相關元件對剪枝特別敏感,而動作微調過程也可能損害預訓練視覺表徵的品質。換言之,動作 policy 究竟應該只依賴最終視覺表徵,還是也應該存取中間層的視覺運算,是一個此前未被充分檢驗的架構選擇。

- **Main method**:NEO-VLA 延續 NEO 系列的「結構原生」(structurally native)設計哲學,以步幅 32 的輕量雙階段卷積 patch embedder 直接將原始像素投影至 backbone token 空間(每 32×32 像素區域對應一個視覺 token),完全不經過任何獨立預訓練的視覺編碼器、影像 codebook 或 autoencoder。影像與語言 token 在 40 層的 2B 參數 decoder backbone 中共同處理,backbone 採用模態感知式注意力機制:文字 token 使用因果注意力,視覺 token 則在各自視覺區塊內採雙向互動,搭配 Native Rotary Position Embedding 將位置因子化為時間、高度、寬度三軸座標。一個獨立、窄而淺、隨機初始化的 flow-matching 動作專家,透過可配置的「層映射」(layer map)機制,同時注意來自 backbone 選定層的快取 key/value,以及自身動作 token 的 key/value,預測涵蓋雙臂與身體動作區塊的速度場。這使得「動作專家該從 backbone 哪個深度讀取視覺資訊」成為一個明確的架構選擇,而非被固定編碼器終點所限制。backbone 以三階段訓練:先以大規模圖文資料建立視覺感知能力並保留語言模型原有能力,再以多樣化的標註、對話、OCR、偵測資料深化視覺語言對齊,最後進行高品質多模態指令微調。

- **和以往方式的差異**:與既有 VLA 普遍保留獨立視覺編碼器、僅在動作生成端創新的做法不同,NEO-VLA 改變的是視覺介面本身——讓動作生成得以直接運用 backbone 內部演化中的視覺表徵,而非被下游固定於一個視覺終點。論文透過系統性的層映射消融實驗(first-28、skip-28、end-28、full-40 四種讀取深度設定)與注意力接入點介入實驗(替換不同觀測的 key/value、遮蔽腕部影像或指令),直接驗證「動作關鍵資訊在 backbone 的哪個深度浮現」,發現凍結 backbone 時及早層讀取持續優於僅讀取後段層,且這項優勢並非單純來自存取中間層特徵(論文另外在 Qwen3-VL 上直接路由至視覺塔中間特徵的對照實驗顯示效果不升反降),而是源自編碼器自由的預訓練方式本身就將視覺表徵塑造為「控制就緒」(control-ready)的形式。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示 NEO-VLA 的整體架構:多視角觀測影像保留原始長寬比後進入跨時間與視角共享的 patch embedder(完全不使用視覺 transformer、autoencoder 或向量量化 codebook),相機內參與旋轉由共享 MLP 編碼,機器人狀態由獨立 MLP 編碼,這些 token 與描述控制頻率、具身類型、座標參考系、任務指令的結構化提示共同組成前綴;獨立的窄幅動作專家聯合注意選定 backbone 層的快取 key/value 與自身動作 token,由 flow matching 訓練以預測涵蓋雙臂與身體的速度場。第二張圖展示真實世界 policy 執行的關鍵影格:涵蓋拿紙杯倒水、將網球放上罐子、將膠帶捲放入碗中再放入網球、將橫放罐子轉正插入膠帶捲、依序夾取四片軍艦壽司擺盤等多樣操作序列。

![Figure]({{ site.baseurl }}/assets/images/2611.06918_neovla_overview.png)

_Figure 1: NEO-VLA 整體架構——像素輸入、連續動作輸出,視覺路徑不含任何視覺 transformer、autoencoder 或向量量化 codebook,動作專家可配置讀取 backbone 不同深度的 key/value_

![Figure]({{ site.baseurl }}/assets/images/2611.06918_neovla_keyframes.png)

_Figure 2: NEO-VLA 真實世界操作關鍵影格——涵蓋精準放置、物體重新定向、多步驟序列操作等多樣互動模式_

### Result

- **主要增強部分**:在 LIBERO 基準上,凍結 backbone、僅訓練動作專家時,NEO-VLA 平均成功率達 90.9%,顯著優於同等設定下的 Qwen3-VL-2B(79.5%)與 Gemma-3-4B(84.5%),甚至在 LIBERO-Long 子集上以 85.4% 超越兩者完整微調後的表現;完整微調後進一步提升至 95.3~97.4%(不同訓練步數下)。在評測七種分布偏移軸線的 LIBERO-Plus 上,NEO-VLA 以 89.7 分的總分,在所有程式碼與權重皆公開的模型中排名第一,尤其在相機與語言擾動下分別達到 94.5 與 91.7 分。在 RoboTwin 2.0 的 Clean-to-Randomized 評測中,NEO-VLA 以 69.40 分在公開模型中取得最佳穩健性表現。真實世界評測涵蓋三項任務(精準放置、長horizon多步驟執行、物體重新定向),僅以 50 筆示範微調後,NEO-VLA(2B 參數)在三項任務上的成功率(12/20、17/20、13/20)全面超越 StarVLA(3B)並與 π0.5(3B)相當或更優,顯示其在更小模型規模下達成具競爭力甚至更強的表現。

- **結果是否公正**:論文明確將「原生 backbone 的優勢」與「單純存取中間層特徵」區分開來驗證——額外的 Qwen3-VL 對照實驗顯示直接路由至視覺塔中間特徵反而使凍結骨幹表現從 79.5% 降至 64.9%,排除了「只要能看到中間層特徵就有效」的簡單解釋,增加了論文核心主張(編碼器自由預訓練本身塑造了控制就緒表徵)的說服力。同時論文也坦承 LIBERO 基準上與 EO-1、MMaDA-VLA、Qwen-RobotManip 等頂尖模型的差距已經很小,誠實地指出該基準已難以區分當前最強 policy 之間的優劣,避免誇大單一基準上的名次。

### Limitation

- **已知 limitation**:論文承認其訓練資料、相機設置、模擬器版本與既有工作存在差異,跨論文比較的數字應被視為基準脈絡參考,而非嚴格受控比較。

- **從 result 來看的弱項**:在 LIBERO-Pro 的物體位置(Position)與任務目標(Task)擾動軸線上,NEO-VLA 表現大幅下降(分別僅 3.0 與 6.3 分),顯示該模型對視覺外觀與指令措辭變化具穩健性,但在需要適應陌生空間配置或動作目標的情境下仍有明顯弱點;同時 RoboTwin 2.0 的乾淨(clean)分割表現(75.78)落後於部分未公開權重的閉源模型(如 Qwen-RobotManip 的 89.58),顯示原生架構的穩健性優勢並未完全轉化為同等的峰值表現。

### Related work

- NEO-VLA 與本頁「Architecture Paradigms」主題下聚焦動作生成機制創新的論文(如 Discrete Diffusion VLA、DFM-VLA)方向不同——這些論文改動的是動作解碼端,NEO-VLA 改動的是視覺輸入端的介面本身,兩者可視為互補而非競爭的架構創新方向。
- 論文的逐層讀取分析與本頁「Interpretability & Diagnostics」主題下的 Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models、Not All Features Are Created Equal 等機制分析類論文有相通的研究精神,都試圖打開 VLA 的黑盒子理解其內部表徵如何驅動動作決策,但 NEO-VLA 更進一步地將分析結論直接轉化為架構設計決策(動作專家該讀取哪些層)。
- 判斷值得 survey 的程度:中高。雖然截至目前尚未見明確的頂會接受公告,但論文由 SenseTime Research 與南洋理工大學 S-Lab 聯合出品,屬於 NEO 系列原生多模態模型(前作已確認 ICLR 2026 接受)的延伸工作,方法論創新清晰且具系統性消融驗證,對於理解「VLA 視覺介面設計」這一尚未被充分探討的架構維度具有參考價值。

### Conclusion

- **綜合評價**:NEO-VLA 挑戰了現代 VLA 設計的一個常見假設——動作應該運作於已經為語義理解而蒸餾過的視覺表徵之上。論文的系統性層映射消融與介入實驗指出,保留對尚未坍縮為最終語義表徵之前的視覺運算的存取,能帶來更強健的控制表現;凍結狀態下原生 backbone 已高度可遷移至動作任務,及早層的存取持續有價值,而單純讓編碼器式 VLM 暴露中間層特徵並不能複製這項優勢——真正關鍵的是編碼器自由的預訓練方式本身如何塑造出控制就緒的表徵。
- **與其他重要文章的關係**:NEO-VLA 可視為對「VLA 視覺介面該如何設計」這一此前較少被獨立探討的架構維度提出的系統性研究,補充了本頁「Architecture Paradigms」主題中多數聚焦動作解碼機制創新論文的空白。ROCm/AMD 在此領域尚待補強之處:NEO-VLA 的核心優勢之一來自於推論時對 backbone 多層 key/value 快取的彈性讀取與 torch.compile 編譯優化(使前向傳播從 515.4ms 降至 282.5ms),這類「多層級聯合推論快取 + 圖編譯優化」的工作負載模式,對底層深度學習框架的記憶體管理與算子融合效率提出要求;隨著原生多模態 VLA 架構逐漸普及,驗證此類跨層注意力讀取模式在 ROCm 軟體棧上的編譯與推論效能,是值得關注的生態系拓展方向。
