---
layout: paper
title: "GR00T N1: An Open Foundation Model for Generalist Humanoid Robots"
section: vla
page_id: "1945393079"
permalink: /zh/vla/gr00t-n1-an-open-foundation-model-for-generalist-humanoid-robots-1945393079/
---

**Paper** : [GR00T N1: An Open Foundation Model for Generalist Humanoid Robots](https://arxiv.org/abs/2503.14734)  
**Source** : arXiv / NVIDIA  
**arXiv ID** : 2503.14734

### Abstract

通用機器人需要一個多用途的身體與一個智慧的大腦。近期人形機器人的進展展現了作為建構「人類世界通才自主性」硬體平台的巨大潛力。一個在大規模、多樣資料來源上訓練的機器人基礎模型,對於讓機器人能推理新情境、穩健處理真實世界的變異性、並快速學習新任務至關重要。為此,作者提出 GR00T N1,一個開源的人形機器人基礎模型。GR00T N1 是一個具雙系統架構的視覺-語言-動作(VLA)模型:視覺-語言模組(System 2)透過視覺與語言指令理解環境;隨後的擴散變換器模組(System 1)即時生成流暢的運動動作。兩個模組緊密耦合並端到端聯合訓練。作者以真實機器人軌跡、人類影片、以及合成生成的資料集的異質混合來訓練 GR00T N1。作者展示其通才機器人模型 GR00T N1 在標準模擬基準上、跨多種機器人本體,均優於最先進的模仿學習基線。此外,作者將模型部署於 Fourier GR-1 人形機器人上,執行語言條件式雙臂操作任務,以高資料效率達成優異表現。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945393079_groot_fig2.png) 

_Figure 2: GR00T N1 Model Overview — dual-system VLA design converting image/language into action tokens_

![Figure]({{ site.baseurl }}/assets/images/1945393079_groot_fig3.png) 

_Figure 3: GR00T N1 Model Architecture — trained across embodiments from single-arm robots to bimanual humanoid hands_

  * 要解決的問題:如何建構一個能同時處理「高層語意理解(看懂場景、聽懂指令)」與「低層即時動作生成(流暢、高頻的馬達控制)」兩種不同時間尺度需求的通才人形機器人基礎模型。
  * 主要方法:採用雙系統(dual-system)架構,借鑑認知科學中「系統一/系統二」的概念——System 2(視覺-語言模組)負責較慢但語意豐富的環境理解與指令解析;System 1(擴散變換器,diffusion transformer)負責即時、高頻的動作生成。兩者緊密耦合、端到端聯合訓練,而非分開訓練後拼接。
  * 與以往方式的差異:先前多數 VLA 模型使用單一整合架構同時處理語意理解與動作生成(如 RT-2 的單一 token 序列生成,或 π0 的 VLM+動作專家),GR00T N1 更明確地將「語意理解」與「動作生成」拆分為兩個不同時間尺度運作的系統,並使用擴散變換器(而非 flow matching 或自回歸 token)作為動作生成模組;此外訓練資料首次系統性地混合真實機器人軌跡、人類影片與合成資料三種異質來源(所謂的「資料金字塔」)。
  * 重要方法設計描述:視覺-語言骨幹採用 NVIDIA Eagle-2 VLM 編碼語言與影像輸入;後續的 DiT(diffusion transformer)-based flow-matching 策略模組輸出高頻動作;公開釋出的 GR00T-N1-2B 模型總參數量 2.2B(其中 VLM 部分 1.34B),在 L40 GPU 上以 bf16 精度採樣 16 個動作的 chunk 僅需 63.9ms;訓練資料呈現「資料金字塔」結構——資料量從底層到頂層遞減,但機體專屬性(embodiment-specificity)遞增,底層為大量通用人類影片與合成資料,頂層為少量但高度貼合特定機體(如 Fourier GR-1)的真實示範。



### Result

  * 主要增強:GR00T N1 在標準模擬基準上、跨單臂、雙臂、人形等多種機器人本體,均優於最先進的模仿學習基線;在真實 Fourier GR-1 人形機器人上執行語言條件式雙臂操作任務時,展現出高資料效率下的優異表現。推論速度方面,2B 參數模型在 L40 GPU 上採樣 16 步動作僅需 63.9ms,顯示其在實用部署上具有相當的即時性。
  * 是否公正:論文由 NVIDIA 發表,比較基準為「最先進的模仿學習基線」,具體基線名稱與數值需要查證全文以確認比較公正性;由於模型與 GitHub 程式碼已開源(Isaac GR00T,並持續更新至 N1.7),具有較高的可驗證性,一定程度佐證了其結果的可信度。



### Limitation

  * 論文摘要未明確列出限制章節,但可推測的弱項:(1)「資料金字塔」概念意味著頂層(最貼合真實特定機體的資料)數量最少,對於全新、未涵蓋在資料金字塔頂層的機體本體,遷移效果需要查證全文;(2) 雙系統架構雖然分工明確,但兩系統之間的協調延遲、以及 System 2 語意理解結果如何有效傳遞給 System 1 動作生成,其設計細節與潛在瓶頸需要查證全文;(3) 目前公開的 GR00T-N1-2B 為縮小版模型,完整版模型的效能與資源需求可能有落差。



### Related work

  * GitHub 上的 Isaac GR00T 專案已持續演進至 N1.7,加入全身人形控制與大規模人類影片預訓練等新特性,顯示此系列模型仍在快速迭代中。
  * GR00T(N1 系列)已被多篇 2026 年 VLA 機制可解釋性論文(如 Not All Features Are Created Equal, 2603.19233)列為分析對象之一(與 π0.5、SmolVLA 並列為多路徑架構代表),顯示其架構設計具有代表性。
  * 值得 survey 的程度極高:GR00T N1 是 NVIDIA 在人形機器人基礎模型領域的旗艦工作,其雙系統架構與資料金字塔訓練策略對理解當前人形機器人 VLA 的技術路線具有重要參考價值。



### Conclusion

  * 綜合評價:GR00T N1 透過雙系統架構與異質資料混合訓練,針對人形機器人這一更複雜的具身型態提出了系統性的解決方案,並以開源方式釋出模型與程式碼,對整個人形機器人 VLA 生態系有重要推動作用,值得深入參考。
  * 與其他重要文章的關係:GR00T N1 與 π0.5、SmolVLA 同屬「多路徑(VLM + 專家/動作模組分離)」架構陣營,並被 Not All Features Are Created Equal(2603.19233)等論文用作分析對象,證實其專家路徑與 VLM 路徑確實編碼不同資訊(動作程式 vs 目標語意)。這與 Helix(Figure AI)的「System 1 / System 2」設計理念高度相似,顯示雙系統架構已成為人形機器人 VLA 的主流設計範式之一。對 ROCm/AMD 而言,GR00T N1 公開的推論效能數據(L40 GPU 上 63.9ms/16-step chunk)提供了一個具體的效能參照點,若 AMD 欲評估自家 GPU 在人形機器人 VLA 推論上的競爭力,可將此作為基準比較對象;但論文本身僅提及 NVIDIA 自家 GPU(L40)的測試數據,未提及 ROCm 或 AMD 硬體上的表現,此為延伸判斷而非論文明文比較。