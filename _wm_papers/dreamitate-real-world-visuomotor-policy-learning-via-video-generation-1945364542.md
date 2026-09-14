---
layout: paper
title: "Dreamitate: Real-World Visuomotor Policy Learning via Video Generation"
section: wm
page_id: "1945364542"
permalink: /wm/dreamitate-real-world-visuomotor-policy-learning-via-video-generation-1945364542/
---

**Paper** : [Dreamitate: Real-World Visuomotor Policy Learning via Video Generation](https://arxiv.org/abs/2406.16862)  
**Source** : arXiv / CoRL 2024（Conference on Robot Learning）/ Columbia University, Toyota Research Institute, Stanford University  
**arXiv ID** : 2406.16862

### Abstract

機器人操作策略面對多樣視覺環境時的泛化能力是關鍵挑戰。Dreamitate 提出一個視覺運動（visuomotor）策略學習框架,利用在大規模網路影片上預訓練的視訊生成模型（video diffusion model）,針對特定任務的人類示範進行微調（fine-tune）。在測試時，模型根據新場景的影像生成一段「任務執行影片」,再將此合成影片直接用於控制機器人。其關鍵洞見是：使用常見工具（common tools）可以自然地橋接人類手部與機器人夾爪之間的具身差異（embodiment gap）。作者在四個複雜度遞增的任務上驗證，顯示利用網路規模生成模型能讓策略達到明顯優於現有行為克隆（behavior cloning）方法的泛化能力。

### Method

![Figure](/assets/images/1945364542_dreamitate_fig1.png) 

_Figure 1: Real-World Visuomotor Policy Learning via Video Generation - Dreamitate fine-tunes a video generative model to synthesize videos of tool-use demonstrations, which are tracked to extract robot actions._

![Figure](/assets/images/1945364542_dreamitate_fig2.png) 

_Figure 2: Method Overview - stereo camera recordings of human demonstrations, video model fine-tuning, and 3D trajectory extraction for closed-loop execution._

  * **要解決的問題** ：行為克隆類策略在面對訓練分布之外的視覺場景（新背景、新光照、新物件外觀）時泛化能力不足。
  * **Main method** ：先在人類示範影片上微調一個預訓練的視訊擴散模型，使其能根據新場景的起始影像生成「執行任務」的合成影片；再從生成影片中以視覺追蹤（3D tracking）工具軌跡,轉換為機器人的顯式動作序列來控制機械手臂。
  * **與以往方式的差異** ：不同於直接從影像回歸動作的行為克隆策略，Dreamitate 把「預測未來」與「動作生成」拆成兩階段——先用生成模型「想像」出任務執行過程的影片，再把影片轉譯為動作,藉此把網路規模影片資料中蘊含的視覺泛化能力遷移到機器人策略上。
  * **重要方法設計描述** ：策略流程為：(1) 輸入新場景觀測影像；(2) 微調後的視訊擴散模型生成一段以工具（如夾子、鏟子等常見工具）操作物件的未來影片；(3) 對生成影片中的工具進行3D追蹤，得到工具在空間中的運動軌跡；(4) 將該軌跡轉換為機器人末端執行器的動作命令，直接執行。使用「工具」作為人類示範與機器人執行之間的共同媒介，是橋接具身差異的核心設計。



### Result

  * 在四個複雜度遞增的操作任務上，Dreamitate 相較於現有行為克隆基線方法,展現出明顯更高的視覺泛化能力（能應對訓練時未見過的場景外觀變化）。
  * 論文是否公正：Columbia/TRI/Stanford 團隊提供了專案網站與程式碼（cvlab-columbia/dreamitate），具一定可重現性；但具體數值指標與基線比較細節摘要未詳述，需要查證全文與其他論文（例如後續的 video-generation-as-policy 相關工作，如 2508.00795 "Video Generators are Robot Policies"）的比較數據以確認結果一致性。



### Limitation

  * 方法依賴「常見工具」作為人類與機器人之間的媒介，對於不涉及工具操作、純粹徒手/夾爪直接操作物件的任務，此方法的適用性摘要未明確提及，需要進一步查證全文。
  * 依賴視訊生成模型推論以及後續3D追蹤，可能帶來較高的推論延遲，論文摘要未提及即時性（real-time）表現，此為實務部署上的潛在弱項。
  * 生成影片的品質與3D追蹤精度會直接影響最終動作準確性，屬於典型「生成式世界模型驅動策略」共通的誤差累積風險，但摘要未具體討論失敗模式。



### Related work

  * 屬於「video generation 驅動機器人策略」路線的早期代表作之一，與同一研究方向下更晚近的工作（如 2508.00795《Video Generators are Robot Policies》)有明顯延續關係,顯示這條路線持續受到關注並擴展。
  * 判斷 related work 值得 survey 的程度：高，Dreamitate 常被近期 world model / video-based policy 相關綜述引用，作為「以生成影片代理動作預測」範式的代表工作之一。



### Conclusion

  * 本文是連接「大規模視訊生成模型」與「機器人操作策略」的重要早期示範性工作，其「以工具為橋樑」的具身差異解決思路具有一定啟發性,值得作為 world model / video-based policy 研究的參考文獻。
  * 與其他重要文章的關係：可視為 MimicGen（幾何式資料生成）路線之外的另一種資料/策略生成範式,兩者分別代表「幾何重組」與「生成式影片模仿」；後續也與 world model 綜述（如本次清單中的多篇 survey）中討論的「video world model 驅動 policy」類別相呼應。
  * ROCm/AMD 關聯性：本方法核心依賴視訊擴散模型的訓練與推論，這類大型生成模型的訓練/推論在 ROCm 上的支援程度（如 PyTorch ROCm 對應的 diffusers 生態、3D tracking 工具鏈的 GPU 相容性）需要另行查證；摘要中未提及具體硬體或框架細節,無法判斷是否有明確關聯，誠實說明看不出明確關聯。