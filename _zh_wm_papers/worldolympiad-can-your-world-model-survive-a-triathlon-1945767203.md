---
layout: paper
title: "WorldOlympiad: Can Your World Model Survive a Triathlon?"
section: wm
page_id: "1945767203"
permalink: /zh/wm/worldolympiad-can-your-world-model-survive-a-triathlon-1945767203/
---

**Paper** : [WorldOlympiad: Can Your World Model Survive a Triathlon?](https://arxiv.org/abs/2606.11129)  
**Source** : arXiv (cs.CV)  
**arXiv ID** : 2606.11129

### Abstract

WorldOlympiad 是一個用來全面診斷「影片式世界模型」(video-based world models) 的評測基準，聚焦三個互補面向：物理真實性 (physical faithfulness)、幾何一致性 (geometric consistency)、以及互動保真度 (interaction fidelity)。現有基準大多只評估視覺品質、語意對齊或短期時間連貫性，難以判斷生成影片是否遵守物理規則、維持一致的 3D 結構、以及在長時間範圍內維持可控互動。WorldOlympiad 將世界模型評測拆解成三條賽道（物理、幾何、互動），並涵蓋遊戲、機器人、一般真實世界影片三大下游場景，藉此揭露一般影片品質指標無法捕捉的失敗模式。作者在多個當前最先進的世界模型上做實驗，發現在物理推理、3D 一致性、長時間互動上都存在明顯落差。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767203_worldolympiad_fig1.png) 

_Figure 1: Overview of the WorldOlympiad pipeline for data collection, long-video generation, and multi-dimensional evaluation._

![Figure]({{ site.baseurl }}/assets/images/1945767203_worldolympiad_fig2.png) 

_Figure 3: Data standardization pipeline from raw videos to refined action-caption annotations._

  * **要解決的問題** ：現有世界模型評測基準太偏重視覺品質/語意對齊/短期連貫性，無法回答「生成的影片是否物理正確、幾何一致、且能長時間維持可控互動」這個更根本的問題。
  * **Main method** ：提出三條評測賽道
    * Physical track：使用物體分割 (object segmentation) 搭配 MLLM-as-judge，評估生成影片是否遵循力學、熱現象、材料特性等可解釋的物理規則。
    * Geometry track：用 Gaussian Splatting 對生成影片做 3D 重建，評估結構一致性、跨視角連貫性、相機軌跡對齊程度。
    * Interaction track：評估生成的 rollout 是否遵循複雜的動作提示 (action prompt)，並在連續影片片段之間維持平滑連貫的轉場。
    * 三條賽道再交叉覆蓋三大下游場景（遊戲、機器人、通用真實世界影片），形成可擴展、可解釋的評測套件。
  * **與以往方式的差異** ：以往世界模型評測（如 FVD、CLIP score 等）多是整體視覺/語意層面的指標，WorldOlympiad 把評測拆成物理/幾何/互動三個可解釋的子面向，並針對每個面向設計專門的量測手段（分割+MLLM判斷、3D重建、動作-影片對齊），使失敗模式可被定位到具體原因,而非只給單一分數。
  * **重要設計描述** ：整體架構是一個「診斷式」評測流程：輸入待測世界模型 → 產生多場景 rollouts → 分別送入三條賽道的獨立分析管線（物理判別器、3D重建器、動作對齊評估器）→ 各自輸出子指標 → 匯總成可解釋的能力剖繪 (capability profile)，而非單一總分。



### Result

  * 對多個最先進的世界模型做實驗後，發現它們在物理推理、3D一致性、長時間互動上都有實質差距（substantial gaps），代表視覺品質好的模型不一定物理正確或幾何一致。
  * 摘要未提供具體數值分數或模型排名，需要查證全文或 project page（https://alibaba-damo-academy.github.io/WorldOlympiad/）取得詳細結果表。
  * 是否公正：由於這是一個新提出的基準，其評測方法（MLLM-as-judge、Gaussian Splatting重建）本身也可能帶有偏差（例如MLLM判斷的一致性、重建誤差），論文摘要未討論這些評測工具本身的可靠性驗證，需要查證全文的驗證章節。
  * 需要查證其他論文（如 iWorld-Bench）是否對相同模型有不同的排名結果。



### Limitation

  * 摘要未明確提及作者自陳的limitation章節內容。
  * 從方法設計推測，潛在弱項可能包括：MLLM-as-judge 的判斷穩定性與偏差、Gaussian Splatting 重建品質本身對生成影片的偽影敏感、以及基準覆蓋場景（遊戲/機器人/通用影片）是否足以代表真實部署場景，這些都需要查證全文確認。



### Related work

  * 同期還有 iWorld-Bench (arXiv:2605.03941)，同樣是針對互動式世界模型的基準，但更聚焦距離感知、記憶等互動能力與統一動作生成框架，二者可以互相對照參考。
  * 暫無發現明確的更新後續研究（如針對 WorldOlympiad 基準做二次分析或擴展的論文）。
  * 值得 survey 的程度：中高。這類評測基準論文本身通常會被後續世界模型論文引用作為評測工具，建議追蹤其 GitHub repo（alibaba-damo-academy/WorldOlympiad）及排行榜更新。



### Conclusion

  * 整體評價：這是一篇對 embodied AI / world model 研究者很有參考價值的評測基準論文，尤其是把物理正確性和3D一致性獨立出來評測，補足了過去只看視覺品質的盲點，值得參考。
  * 與其他重要文章的關係：延伸/補強了過去以 FVD、CLIP 等指標為主的世界模型評測方法，並與同期的 iWorld-Bench 形成互補（前者偏物理/幾何/互動三維度，後者偏距離感知/記憶/動作生成統一框架）。
  * ROCm/AMD 待補強部分：這篇論文本身不涉及硬體或訓練框架，看不出與 ROCm 的直接關聯；但若 AMD 要建立自己的世界模型評測/驗證流程（例如驗證在 MI300 系列上訓練或推論的世界模型是否物理一致），此基準的三軌評測方法論可作為評測框架設計的參考基礎。