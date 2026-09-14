---
layout: paper
title: "MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations"
section: wm
page_id: "1945473767"
permalink: /Physical-AI-Papers-Survey/wm/mimicgen-a-data-generation-system-for-scalable-robot-learning-using-human-demons-1945473767/
---

**Paper** : [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations](https://arxiv.org/abs/2310.17596)  
**Source** : arXiv / CoRL 2023（7th Conference on Robot Learning）/ NVIDIA  
**arXiv ID** : 2310.17596

### Abstract

模仿學習（imitation learning）需要大量人類示範資料，但收集成本極高。MimicGen 提出一套資料生成系統，能從少量（約200筆）人類示範中自動合成大規模、多樣化的機器人示範資料集，透過將原始示範適應（adapt）到新的場景配置、物件實例與機器人手臂組合，產生超過5萬筆跨18個任務的示範資料。論文顯示以此生成資料訓練的模仿學習策略,能在長時程（long-horizon）與高精度任務（如多零件組裝、咖啡調製）上達到良好表現，效果可與收集更多真人示範相比擬,是一種擴充機器人學習資料的經濟方案。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945473767_mimicgen_fig1.png) 

_Figure 1: MimicGen Overview - generating large diverse datasets from a small number of human demonstrations by re-purposing them for new settings._

![Figure](/Physical-AI-Papers-Survey/assets/images/1945473767_mimicgen_fig2.png) 

_Figure 2: MimicGen System Pipeline - parsing source demos into object-centric subtask segments and adapting them to generate new demonstrations._

  * **要解決的問題** ：人類示範資料的收集成本高、耗時,限制了模仿學習的可擴展性。
  * **Main method** ：MimicGen 從一小組人類示範出發，將示範中的物件互動片段（object-centric subsegments）依據新場景中的物件姿態進行幾何變換（transform），重新拼接生成適用於新場景配置的完整示範軌跡，再以逆向運動學（IK）求解器轉換為機器人可執行的動作序列。
  * **與以往方式的差異** ：與需要大量人工遠端操作（teleoperation）收集示範的傳統方法不同，MimicGen 不需要額外人力即可大規模擴增資料,且可以跨物件實例、場景佈局、甚至跨機器人手臂形態生成新資料。
  * **重要方法設計描述** ：系統把示範拆解成以物件為中心的動作片段（例如「抓取」「放置」等子任務），針對新的初始場景中物件的位置與姿態，計算座標變換,將片段中相對於物件的軌跡重新對應到新場景，再串接不同片段組成完整任務示範；此流程可反覆執行以生成大量多樣化資料，並可透過篩選機制（例如僅保留任務成功的生成示範）確保資料品質。



### Result

  * 使用 MimicGen 從約200筆人類示範生成超過5萬筆示範，涵蓋18個任務、多種場景配置與機器人手臂;以此訓練的模仿學習策略在長時程、高精度任務（多零件組裝、咖啡調製等）上表現良好,且能應對較廣的初始狀態分布。
  * 論文比較了「用 MimicGen 生成等量資料」與「額外收集等量人類示範」兩種方案，顯示生成資料的效益可與收集更多人類示範相比擬,证明其為經濟可行的資料擴增方式。
  * 論文是否公正：本論文提供了公開的資料集、模擬環境與程式碼（NVlabs/mimicgen），可供社群驗證；是否有其他論文結果與此不符，需要查證其他論文的比較數據（例如後續是否有工作指出生成資料在特定任務類型上品質不足）。



### Limitation

  * 論文中的方法依賴人類示範的物件中心分割（object-centric segmentation）與精確的物件姿態估計，若場景物件偵測/姿態估計不準確,生成軌跡品質可能下降。
  * 主要在模擬環境中驗證,真實世界的感知雜訊、物理接觸建模等因素未必能完全被此資料生成方式覆蓋，摘要與可得資訊未明確提及大規模真實機器人部署的結果，需要進一步查證全文。
  * 生成的資料仍受限於原始人類示範所涵蓋的技能種類與物件互動模式,對於原始示範未涵蓋的全新技能類型可能無法直接生成。



### Related work

  * MimicGen 是資料生成 / 資料增強（data generation/augmentation）路線的代表性早期工作，與後續許多結合生成式模型（video diffusion、world model）的資料合成方法（如 Dreamitate）在目標上有相似之處，但方法路線不同：MimicGen 走的是幾何/運動學層面的軌跡重組，而非影像生成。
  * 暫無發現更新的相關研究（在本次調查範圍內未進一步搜尋其後續引用工作）。
  * 判斷 related work 值得 survey 的程度：中高，作為 robot data generation 領域的重要 baseline，經常被後續 world model / video generation 資料合成論文引用比較。



### Conclusion

  * 本文是機器人學習資料生成領域的重要基準（baseline）工作，方法簡潔、開源且具備可重現性,值得作為理解「非生成式模型路線」資料擴增的重要參照點。
  * 與其他重要文章的關係：常被用作與生成式世界模型驅動的資料合成方法（例如利用 video diffusion 生成示範的 Dreamitate、以及更近期的 world model 資料生成方法）比較的基準,兩者代表了「幾何重組」與「生成式合成」兩種不同的資料擴增哲學。
  * ROCm/AMD 關聯性：本論文以 NVIDIA 模擬環境（robosuite/MuJoCo 系）與 IK 求解器為主，屬於通用機器人學習基礎設施,並未涉及特定加速器優化；在 ROCm 上復現需要注意的是模擬環境（Isaac/robosuite 等）目前多依賴 NVIDIA 生態,若要在 AMD 平台部署,需要評估模擬環境對 ROCm/非CUDA 環境的相容性,這是 ROCm 在 embodied AI 模擬鏈路上尚待補強的部分。