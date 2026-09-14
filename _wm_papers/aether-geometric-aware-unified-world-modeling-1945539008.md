---
layout: paper
title: "Aether: Geometric-Aware Unified World Modeling"
section: wm
page_id: "1945539008"
permalink: /Physical-AI-Papers-Survey/wm/aether-geometric-aware-unified-world-modeling-1945539008/
---

**Paper** : [Aether: Geometric-Aware Unified World Modeling](https://arxiv.org/abs/2503.18945)  
**Source** : arXiv / ICCV 2025 & ICCV 2025 RIWM Outstanding Paper / Aether Team（Shanghai AI Laboratory 等）  
**arXiv ID** : 2503.18945

### Abstract

將幾何重建（geometric reconstruction）與生成式建模（generative modeling）整合，是開發具備類人空間推理能力 AI 系統的關鍵挑戰。Aether 提出一個統一框架，透過聯合優化三項核心能力——(1) 4D 動態重建、(2) 動作條件式影片預測、(3) 目標條件式視覺規劃——使世界模型具備幾何感知的推理能力。透過任務交錯式特徵學習（task-interleaved feature learning），Aether 在重建、預測、規劃三項目標之間達成知識協同共享。建立在影片生成模型之上，此框架即使完全未見過真實世界資料，也展現出零樣本（zero-shot）的「合成到真實」泛化能力，並在動作跟隨與重建任務上都達到零樣本泛化，重建效果甚至可與領域專屬模型相當或更優。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539008_aether_fig1.png) 

_Figure 1: An overview of Aether, trained entirely on synthetic data - highlighting 4D reconstruction, action-conditioned 4D prediction, and visual planning._

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539008_aether_fig2.png) 

_Figure 4: The overall pipeline of Aether - with different condition combinations, Aether can serve different tasks._

  * **要解決的問題** ：幾何重建（精確但缺乏生成/預測能力）與生成式影片模型（能生成但缺乏精確幾何一致性）長期被視為兩條分離的技術路線,如何統一兩者以支援具備空間推理的世界模型是核心問題。
  * **Main method** ：Aether 以影片生成模型為基礎，同時學習 4D 動態重建、動作條件式影片預測、目標條件式視覺規劃三項任務，透過任務交錯的特徵學習機制讓三者共享並互相強化彼此的表徵;並使用相機軌跡（camera trajectory）作為「幾何知情的動作空間」（geometry-informed action space），使動作條件預測與視覺規劃可以基於幾何一致的相機運動來驅動。
  * **與以往方式的差異** ：與只做重建（無生成/預測能力）或只做生成（缺乏精確幾何一致性）的既有方法不同，Aether 將三種能力放入同一個訓練框架中聯合優化，並且完全基於合成（synthetic）4D 資料訓練,搭配自動化資料標註管線取得精確的4D幾何知識,卻仍能零樣本泛化到真實世界。
  * **重要方法設計描述** ：整體架構建立於既有的影片生成骨幹上，透過在同一模型中交錯訓練「給定影片預測其4D幾何結構」「給定起始幀與相機軌跡動作預測未來影片」「給定起始與目標影像進行視覺路徑規劃」三種任務，共享底層特徵表示；相機軌跡本身被當作動作介面，讓模型在做動作條件生成與規劃時，天然地帶有幾何一致的約束。



### Result

  * 即使訓練時從未見過真實世界資料（僅使用合成4D資料），Aether 在動作跟隨（action following）與重建任務上都達到零樣本泛化，重建效果可與專門針對重建設計的領域模型相當或更好。
  * 論文獲 ICCV 2025 及 ICCV 2025 RIWM（Robotics in the Wild Models）Outstanding Paper 肯定,顯示在同行評審社群中獲得高度認可。
  * 是否公正：論文提供專案頁與程式碼（InternRobotics/Aether），具備可重現性；由於只根據摘要與已知資訊撰寫,對於其量化比較數據是否與其他 4D 重建/世界模型論文的報告結果一致，需要查證其他論文的比較數據。



### Limitation

  * 據已知資訊，作者自陳的限制包括：在高度動態場景（如大幅度運動或密集人群）中表現較弱；相機姿態估計在某些情況下不夠穩定；在做視覺規劃任務時，建議起始觀測與目標影像的空間/視覺距離不宜過遠,否則效果會下降。
  * 完全基於合成資料訓練，雖然展現出良好的零樣本遷移能力，但對於合成資料未能涵蓋的真實世界複雜物理現象（如可變形物體、精細接觸力學）,其表現上限尚待更多真實世界驗證,摘要未提供此類細節，需要進一步查證全文。



### Related work

  * Aether 代表了 world model 領域中「幾何 + 生成統一」路線的重要進展，與同期的空間智能模型（如 World Labs 的相關工作）、以及後續綜述（如本次清單中的多篇 2026 年 world model survey）都會將其列為代表性方法之一。
  * 判斷 related work 值得 survey 的程度：高，這類「4D 重建 + 動作預測 + 視覺規劃」三合一框架，是目前 world model for robotics 領域中被多篇綜述反覆提及的重要範式,值得投入時間追蹤其後續衍生工作。
  * 暫無發現比 Aether 更新、直接取代其定位的單一後續工作，但本次清單中的多篇 2026 survey（如 arXiv:2605.00080、2606.00113）很可能已將 Aether 納入其分類討論中，建議在閱讀這些綜述時交叉比對。



### Conclusion

  * 本文是 world model 領域中融合幾何重建與生成式預測/規劃的代表性工作,獲得 ICCV 2025 Outstanding Paper 肯定，具有較高的參考價值，特別適合作為理解「4D geometry-aware world model」設計思路的入門文獻。
  * 與其他重要文章的關係：本論文可視為對「純生成式 video world model（缺乏幾何一致性）」與「純幾何重建模型（缺乏預測/規劃能力）」兩條路線的整合與挑戰,填補了兩者之間的空白；它也常被後續 survey 論文（如清單中的 world model 綜述）引用作為關鍵技術節點。
  * ROCm/AMD 關聯性：論文建立在影片生成模型（可能基於 diffusion transformer 架構）之上，訓練與推論規模可能相當大;由於摘要未提及具體訓練框架或硬體細節，無法確認其對 ROCm 生態的相容性,誠實說明看不出明確關聯。若 AMD 團隊想在 ROCm 上復現此類統一世界模型，需要額外查證其開源程式碼對非 CUDA 環境（如 PyTorch ROCm 後端）的支援程度，這也是目前 ROCm 在大型影片生成/4D重建模型訓練上普遍面臨的生態成熟度落差。