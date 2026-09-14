---
layout: paper
title: "V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning"
section: wm
page_id: "1945474552"
permalink: /wm/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planni-1945474552/
---

**Paper** : [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning](https://arxiv.org/abs/2506.09985)  
**Source** : arXiv（Meta FAIR / Mila）  
**arXiv ID** : 2506.09985

### Abstract

V-JEPA 2 是 Meta FAIR 提出的自監督影片模型，結合網路規模的影片資料與少量機器人互動資料，用以理解、預測並規劃物理世界中的行為。研究團隊先在超過 100 萬小時的網路影片與圖片資料上，預訓練一個不需動作標籤的聯合嵌入預測架構（joint-embedding-predictive architecture, JEPA），使其在動作理解（Something-Something v2 上 top-1 準確率 77.3）與人類動作預期（Epic-Kitchens-100 上 recall-at-5 達 39.7）上取得優於過往任務專用模型的表現；對齊大型語言模型後，也在多個影片問答任務上於 80 億參數規模達到當時最佳表現。接著,團隊以少於 62 小時的無標籤機器人影片（來自 Droid 資料集）後訓練出一個以動作為條件的潛在世界模型 V-JEPA 2-AC，並在兩個不同實驗室的 Franka 機械手臂上實現零樣本（zero-shot）的抓取與放置任務規劃，完全不需在部署環境中蒐集資料或進行任務特定訓練與獎勵設計。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474552_vjepa2_fig1.png) 

_Figure: V-JEPA 2 Abstract 概論圖 — 影片與圖片自監督預訓練，結合少量機器人資料訓練 action-conditioned world model。_

![Figure]({{ site.baseurl }}/assets/images/1945474552_vjepa2_fig2.png) 

_Figure 1: V-JEPA 2 Overview — 以 1M 小時網路影片與 1M 圖片預訓練 visual mask denoising 影片模型架構。_

  * 要解決的問題：現代 AI 的一大挑戰是如何主要透過觀察（observation）來學習理解世界並學習行動，而非依賴大量帶標籤的監督式動作資料或大規模的機器人真實互動資料（後者成本高昂且難以規模化）。
  * Main method：分兩階段——(1) 以不含動作標籤的 JEPA 架構在超過 100 萬小時網路影片與圖片上做自監督預訓練，得到 V-JEPA 2 編碼器，學習對可預測的場景內容做表徵，同時忽略生成式模型會強調的不可預測像素細節；(2) 凍結 V-JEPA 2 編碼器後，用少於 62 小時的無標籤機器人影片訓練一個新的、以動作為條件的預測器 V-JEPA 2-AC，讓模型能根據機器人本體感覺（proprioception）與動作，預測下一影格的表徵。
  * 與以往方式的差異：不同於以像素級重建為目標的生成式影片模型（如擴散模型），JEPA 架構在學習到的表徵空間中做預測，只關注場景中可預測的部分而忽略不可預測的視覺雜訊細節，因此能更有效地利用網路規模、無動作標籤的影片資料；此外訓練 V-JEPA 2-AC 所需的機器人資料量（不到 62 小時）遠少於典型模仿學習或強化學習所需的機器人資料規模。
  * 重要方法設計：V-JEPA 2-AC 訓練時結合了標準的單步教師強制（teacher-forcing）損失與多步 rollout 損失，用以降低多步規劃時的誤差累積（error accumulation）問題；部署時，模型可用影像目標（image goals）作為規劃依據，在未經任務特定訓練或設計獎勵函數的情況下，直接透過模型推理完成抓取與放置任務。



### Result

  * 結果：V-JEPA 2 在動作理解與人類動作預期任務上超越先前的任務專用模型（Something-Something v2 top-1 77.3；Epic-Kitchens-100 recall-at-5 39.7）；對齊語言模型後在 PerceptionTest（84.0）、TempCompass（76.9）等影片問答任務於 80 億參數規模達到當時最佳表現。V-JEPA 2-AC 在兩個不同實驗室的 Franka 機械手臂上實現零樣本抓取放置，在使用未校正、低解析度 RGB 相機並將取樣動作限制在特定半徑內的測試中，相較於影片-語言-動作基準模型 Octo（15% 成功率），V-JEPA 2-AC 平均達到 80% 的杯子抬起與移動成功率；規劃速度也顯著更快，每個動作僅需 16 秒，相較於以影片生成為基礎的 Cosmos 模型需要 4 分鐘。
  * 主要增強部分：資料效率（僅需少量機器人資料即可獲得可規劃的世界模型）、跨環境零樣本泛化能力、以及規劃速度（相較影片生成式世界模型快非常多）是本文最主要的貢獻。
  * 是否公正/需查證處：與 Octo、Cosmos 的比較數據來自論文本身的實驗設計（特定任務、特定測試環境），是否能推廣到更廣泛的機器人操作任務與更複雜的場景，仍需要查證後續獨立復現或第三方評測研究；「4 分鐘 vs. 16 秒」的規劃時間比較，也需確認兩者在相同硬體與相同任務設定下進行,以確保比較公正性。



### Limitation

  * 論文摘要中雖未列出詳細限制段落，但從方法設計可看出：V-JEPA 2-AC 目前的驗證任務集中在抓取與放置（pick-and-place）等相對簡單的操作任務,且動作取樣被限制在特定半徑內，暗示模型在更複雜、大範圍動作空間或精細操作（fine manipulation）任務上的能力仍待驗證。
  * 依賴凍結的 V-JEPA 2 編碼器進行後訓練，代表模型的表徵品質高度取決於預訓練階段學到的視覺表徵是否涵蓋目標機器人任務所需的視覺與物理概念，若目標任務涉及預訓練資料中罕見的物體或互動型態，可能影響零樣本泛化效果，此點需要進一步查證全文與後續研究是否有討論。



### Related work

  * V-JEPA 2 延續 Yann LeCun 提出的 JEPA（joint-embedding predictive architecture）理念，是 V-JEPA 系列的延伸版本；Meta 提及後續有 V-JEPA 2.1 於 2026 年釋出，改善了密集特徵學習（dense feature learning），值得後續追蹤查證其技術細節。
  * 與 Cosmos（NVIDIA）等基於影片生成的世界模型相比，V-JEPA 2 代表了「非生成式、表徵預測式」世界模型路線的重要代表作，兩種路線（生成式 vs. 表徵預測式）在物理世界建模與機器人規劃上的優劣比較，是一個值得深入 survey 的方向。
  * 判斷 related work 值得 survey 的程度：高，V-JEPA 2-AC 的規劃效率與零樣本泛化能力對 embodied AI／機器人策略學習的實務應用具有高度參考價值，且與 DreamerV3（RL 式想像規劃）、Cosmos（生成式世界模型規劃）在方法論上構成有意義的三方對照。



### Conclusion

  * 綜合評價：V-JEPA 2 及其 V-JEPA 2-AC 世界模型展示了「自監督表徵學習 + 少量機器人資料」即可產生具備零樣本規劃能力的世界模型，這對於資料稀缺的機器人應用場景具有重要意義，值得認真參考，尤其其相較生成式世界模型（如 Cosmos）在規劃速度上的顯著優勢，是一個值得關注的效率面向。
  * 與其他文章的關係：V-JEPA 2-AC 與論文中直接比較的 Octo（模仿學習式 VLA 模型）、Cosmos（生成式世界模型）構成方法論上的三方比較；與 DreamerV3 相比，兩者都追求「以世界模型支援規劃/控制」，但 V-JEPA 2 採用非重建式的聯合嵌入預測，DreamerV3 則採用類別表徵重建式建模，是世界模型方法論光譜上的兩個代表性端點。
  * ROCm/AMD 關聯：論文正文（本次僅讀取摘要與部分技術細節）未提及具體訓練硬體平台，但其提及「相較 Cosmos 模型需要 4 分鐘生成規劃，V-JEPA 2-AC 僅需 16 秒」，隱含規劃效率對於機器人即時控制應用的重要性；若 AMD/ROCm 想在 embodied AI 規劃推論這塊尋求切入點，V-JEPA 2 這類輕量、非生成式的表徵預測模型（相較於大型生成式世界模型）在推論延遲與硬體資源需求上可能更適合中小規模部署，但這僅為推測，論文本身未討論任何特定硬體平台的支援情況。