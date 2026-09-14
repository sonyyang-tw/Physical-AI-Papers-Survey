---
layout: paper
title: "World Action Models: The Next Frontier in Embodied AI"
section: vla
page_id: "1945392639"
permalink: /Physical-AI-Papers-Survey/vla/world-action-models-the-next-frontier-in-embodied-ai-1945392639/
---

**Paper** : [World Action Models: The Next Frontier in Embodied AI](https://arxiv.org/abs/2605.12090)  
**Source** : arXiv (cs.RO / cs.CL / cs.CV)，survey 性質論文  
**arXiv ID** : 2605.12090

### Abstract

本論文是一篇系統性綜述，正式定義並命名了「World Action Models (WAMs)」這個新興範式：一種將「預測性狀態建模（world model）」與「動作生成」統一起來的具身基礎模型，目標是對「未來狀態與動作的聯合分布」建模，而非像傳統 VLA 只學習觀察到動作的反應式映射。作者指出，VLA 雖然在具身策略學習上具有強大的語意泛化能力，但缺乏對物理世界如何在介入下演化的顯式建模；越來越多研究透過整合 world model 來彌補這個不足。由於此領域文獻在架構、學習目標與應用場景上高度分散，缺乏統一的概念框架，本文提出正式定義、釐清相關概念、追溯 VLA 與 world model 研究的源流融合，並將現有方法整理為「Cascaded WAMs」與「Joint WAMs」兩大分類，再依生成模態、條件機制與動作解碼策略進一步細分。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945392639_wam_survey_fig1.png) 

_Figure 1: World Action Models (WAMs) 代表性研究的時序演進與分類。左側分支呈現 Joint WAM 架構的發展，將世界預測與動作生成緊密耦合，並進一步分歧為自回歸（Autoregressive）與擴散式（Diffusion-based）表徵方案，其中連續式方法再細分為 Unified Stream 與 Multi-Stream 骨幹；右側分支總結 Cascaded WAM 管線的發展，其中世界建模與動作執行主要解耦，沿著顯式（Explicit）與隱式（Implicit）表徵對齊路線演進。_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945392639_wam_survey_fig2.png) 

_Figure 2: 本綜述回顧之 World Action Models (WAMs) 全景路線圖與分類。文獻被系統性歸類為四大核心維度：背景（Background）、架構（Architecture）、訓練資料（Training data）、評測協定（Evaluation）。_

  * **要解決的問題** ：VLA 模型學習的是反應式的「觀察 → 動作」映射，沒有顯式建模物理世界在動作介入下如何演化，導致其世界理解能力有限；同時，將 world model 整合進動作生成管線的研究快速增長但高度分散，缺乏統一分類與命名。
  * **主要方法（本質是分類與概念框架，而非單一模型）** ：
    * **正式定義 WAMs** ：明確界定 WAM 為「同時對未來狀態與動作的聯合分布建模」的具身基礎模型，並與相關概念（如純粹的 world model、傳統 VLA）做區隔。
    * **分類體系（taxonomy）** ：將現有方法分為兩大類——Cascaded WAMs（世界模型與動作生成器級聯，先預測未來狀態再生成動作）與 Joint WAMs（世界模型與動作生成聯合建模），再依生成模態、條件機制、動作解碼策略進一步細分。
    * **資料生態系統分析** ：系統性分析支撐 WAM 發展的資料來源——機器人遠端操作（teleoperation）、可攜式人類示範、模擬環境、網路規模的第一人稱（egocentric）影片。
    * **評測協定整理** ：歸納新興的評測方式，圍繞視覺保真度（visual fidelity）、物理常識（physical commonsense）、動作合理性（action plausibility）三個面向。
  * **與以往方式的差異** ：以往文獻中，「world model 整合進 VLA」的研究各自為政，用詞與分類不一致；本文首次系統性統一命名（WAM）、提出跨架構的二元分類（Cascaded vs. Joint），並將資料與評測協定納入同一個框架下討論。



### Result

  * 作為 survey 論文，其「結果」是提供了第一個系統性的 WAM 全景整理，釐清了關鍵架構典範（Cascaded / Joint）及其取捨（trade-offs），並指出開放挑戰與未來研究方向。
  * 是否公正：作為分類與命名型 survey，其分類是否被社群廣泛採用仍需觀察；由於是綜述而非實驗論文，不涉及具體 benchmark 數據對比，因此不適用「其他論文結果是否相符」的問題，但其分類框架本身的完整性與涵蓋面是否公正、全面，需要查證全文所涵蓋的論文清單是否有明顯遺漏。



### Limitation

  * 論文自陳的限制：摘要中提及該領域「文獻仍然分散、缺乏統一框架」，這是論文試圖解決的問題本身，摘要未進一步說明本綜述分類法本身的侷限性（例如是否有方法無法乾淨地歸入 Cascaded/Joint 二元分類）。
  * 從內容推測的弱項：任何分類型 survey 都可能存在分類邊界模糊、新方法快速湧現導致分類法過時的風險；需要查證全文以了解作者對此的討論。



### Related work

  * 本論文本身即是對相關研究的大範圍整理，涵蓋 VLA 與 world model 的源流演進；由於是 2026 年 5 月的綜述，其涵蓋範圍應包含清單中「Do World Action Models Generalize Better than VLAs?」等同時期論文，但兩者關係（是否互相引用）需要查證全文確認。
  * 值得 survey 的程度：高。作為命名與分類此新興範式的首篇系統性綜述，是快速了解 WAM 領域全貌的重要入口文獻，建議作為研究此方向的起手式閱讀材料。



### Conclusion

  * 綜合評價：非常值得參考。此文為 World Action Models 這個新興且快速發展的範式提供了統一命名、分類與資料/評測整理，是進入該領域的重要地圖型文獻，適合作為系列閱讀的起點。
  * 與其他論文關係：此文的分類框架（Cascaded / Joint WAMs）可作為理解清單中其他 WAM 相關論文（如「Do World Action Models Generalize Better than VLAs?」、「Robots Need More than VLA and World Models」）的共通詞彙與參照座標；它本身是「傘型」綜述，統攝了其餘 WAM 相關工作。
  * ROCm/AMD 關聯：從摘要內容看不出與 ROCm/AMD 有明確關聯，論文未涉及具體硬體或訓練框架討論；但由於 WAM 通常涉及大規模影片生成式模型（video generation），對於 AMD/ROCm 而言，值得留意的是此類模型對大規模影片預訓練與擴散式生成的運算需求，是否有對應的 ROCm 生態系統支援（如影片擴散模型的訓練/推論優化）需要另外查證，論文本身未提及。