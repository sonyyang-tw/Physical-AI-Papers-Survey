---
layout: paper
title: "How Cosmos 3 Helps Physical AI Think Before It Acts"
section: wm
page_id: "1945539515"
permalink: /zh/wm/how-cosmos-3-helps-physical-ai-think-before-it-acts-1945539515/
---

**Paper** : [How Cosmos 3 Helps Physical AI Think Before It Acts](https://blogs.nvidia.com/blog/cosmos-3-physical-ai-open-world-foundation-model/)（另可參考 [NVIDIA Cosmos 3 技術報告](https://research.nvidia.com/labs/cosmos-lab/cosmos3/technical-report.pdf) 與 [NVIDIA Cosmos 產品頁](https://www.nvidia.com/en-us/ai/cosmos/)）  
**Source** : 官方技術部落格／技術報告（NVIDIA，2026 年 6 月於 GTC Taipei / COMPUTEX 發布）  
**arXiv ID** : 無正式 arXiv 論文，來源為官方技術報告

### Abstract

NVIDIA Cosmos 3 是 NVIDIA 於 2026 年 6 月發布的開放式「世界基礎模型」（world foundation model），鎖定物理 AI（physical AI）應用，如機器人、自動駕駛車輛與視覺 AI 代理人。其核心是一個結合視覺推理（vision reasoning）、多模態生成（文字、影像、影片、環境音、動作）與動作預測的混合式 Transformer（mixture-of-transformers）架構，讓模型能先「理解」場景中的物體互動、運動與時空關係，再生成對應的影片與動作軌跡，目標是幫助物理 AI 系統「先思考、後行動」。模型以 20 兆 token 的多模態資料（近十億張圖片、四億支真實與合成影片、環境音、文字及人類與機器人動作資料）訓練而成，並以 super／nano／edge 三種規模釋出。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539515_cosmos3_fig1.png) 

_Figure 1: Cosmos 3 作為 Physical AI 的通用骨幹模型，統一建模語言、影像、影片、音訊與動作，涵蓋理解與生成任務。_

![Figure]({{ site.baseurl }}/assets/images/1945539515_cosmos3_fig3.svg) 

_Figure 5: Cosmos 3 的 Mixture-of-Transformers (MoT) 架構 — 單一 transformer 同時處理自回歸（AR）與擴散（DM）子序列，透過共享自注意力機制連結兩者。_

  * 要解決的問題：機器人、自駕車、工廠安全系統等物理 AI 應用需要大量涵蓋各種場景（尤其是罕見或危險的長尾情境，如倉庫中未見過的物件配置、行人突然從停放車輛間走出、堆高機移動路徑預測）的訓練資料，但在真實世界中蒐集這類資料緩慢、昂貴且往往難以重複再現。
  * Main method：Cosmos 3 採用「mixture-of-transformers」架構，將一個推理用 Transformer（reasoning transformer）與一個專責生成的專家 Transformer（expert generation transformer）配對，讓模型能先對物體互動、運動、時空關係進行推理，再生成對應的影片畫面與動作軌跡；模型同時支援文字、影像、影片、環境音與動作等多種模態的輸入與生成（所謂「omnimodal」）。
  * 與以往方式的差異：相較於單純的影片生成模型，Cosmos 3 強調「先推理、後生成」的流程，並將動作預測直接整合進同一個模型架構中，使其不僅能生成逼真的物理場景影片，還能直接產出可用於機器人策略訓練的動作條件資料（action-conditioned data）；此外採用 OpenMDW 1.1（Linux Foundation 的開放模型授權）釋出權重、架構、文件、資料集、基準與程式碼，強調開放生態。
  * 重要方法設計：架構上分為「super」（高物理精準度，適合訓練機器人與自駕車）、「nano」（可在極短時間內生成結果的輕量版）、以及後續釋出的「edge」（40 億參數，適合記憶體受限的邊緣裝置高吞吐推論）三種模型規模，並透過 NVIDIA Cosmos Coalition（結合 Agile Robots、Black Forest Labs、Generalist、LTX、Runway、Skild AI 等業界夥伴）共同推動生態發展。



### Result

  * 結果與增強部分：官方部落格展示了多個應用案例，包括：Agile Robots 使用 Cosmos 3 為其人形機器人與 Thor 3、FR3 等機型生成動作條件式訓練資料；NVIDIA GEAR 團隊用其開發跨遊戲、模擬與真實機器人環境的影片動作模型；Cosmos 3 Nano 的後訓練策略在 RoboLab（模擬中的語言引導任務基準）與 RoboArena（DROID 機器人真實環境策略比較基準）上取得領先成績；模型同時可用於智慧城市／空間場景的推理（識別移動物體、預測路徑交會、生成密集場景描述）以及生成罕見長尾碰撞情境的物理合理影片。官方宣稱 Cosmos 3 在 Physics-IQ、R-Bench、PAI-Bench 等世界生成相關基準上排名第一，並在 Artificial Analysis 開放權重榜單上領先。
  * 是否公正／需查證處：以上排名與領先結果均來自 NVIDIA 官方部落格與新聞稿的自我宣稱，缺乏獨立第三方復現或跨模型的公正比較數據；「Physics-IQ」「R-Bench」「PAI-Bench」等基準的評測方法論、與其他世界模型（如 Genie 3、GAIA 系列）的直接對比細節，仍需要查證官方技術報告全文或第三方評測研究來確認客觀性。



### Limitation

  * 官方部落格與新聞稿並未明確條列 Cosmos 3 的技術限制或失敗案例（自陳限制較少）。
  * 從模型設計與應用場景描述可推測潛在弱項：Nano／Edge 等輕量版本在追求速度與記憶體效率的同時，可能在物理精準度上有所取捨（官方將「高物理精準度」需求明確歸類給 super 版本，暗示 nano/edge 版本在精細物理模擬上可能不如 super 版本）；此外，模型高度依賴大規模多模態資料（20 兆 token），對算力與資料基礎設施要求極高，中小型團隊或研究單位可能難以復現或微調。
  * 需要進一步查證技術報告全文，以了解模型在長時間序列生成一致性、多代理人複雜互動、以及跨具身（cross-embodiment）泛化能力上的具體限制。



### Related work

  * Cosmos 3 是 NVIDIA Cosmos 系列世界基礎模型的最新一代，可與 Cosmos 早期版本比較架構演進（例如是否首次引入 mixture-of-transformers 與 omnimodal 生成）；因未取得早期 Cosmos 版本論文詳細內容，此處無法給出具體版本間差異，需要進一步查證。
  * 與 Google DeepMind 的 Genie 3、Wayve 的 GAIA 系列同屬「世界基礎模型」浪潮下的代表性工作，三者分別代表不同陣營（NVIDIA 硬體與物理 AI 生態、DeepMind 通用互動世界、Wayve 自動駕駛專用）對世界模型的布局，值得橫向比較其架構取向與商業定位。
  * 判斷 related work 值得 survey 的程度：高，Cosmos 3 明確鎖定機器人與自駕車的實務落地（RoboArena、RoboLab 等基準與 Cosmos Coalition 生態聯盟），對於關注 embodied AI 與硬體平台（含 AMD/ROCm）落地機會的讀者具有高度參考價值。



### Conclusion

  * 綜合評價：Cosmos 3 是目前少數明確定位為「開放」世界基礎模型並鎖定物理 AI（機器人、自駕車、視覺 AI 代理人）實務應用的旗艦級專案，其多規模釋出策略（super/nano/edge）與開放授權（OpenMDW 1.1）對產業與研究社群具有實際可用性，值得作為了解「世界模型如何落地為工業基礎設施」的重要案例；但目前資訊來源以官方宣傳材料為主，量化評測的客觀性仍待第三方查證。
  * 與其他文章的關係：Cosmos 3 與 Genie 3、GAIA 系列同屬世界模型「基礎設施化」的趨勢，但明確以 NVIDIA 自身硬體生態（GPU、CUDA 相關工具鏈）為核心進行推廣；對於 AMD/ROCm 而言，這代表了一個重要的競爭與潛在缺口——目前看不到 Cosmos 3 官方資料中有任何關於 ROCm 或非 NVIDIA 硬體支援的描述，暗示這類大規模 omnimodal 世界基礎模型的訓練與推論生態目前高度綁定 NVIDIA 軟硬體棧（CUDA、TensorRT 等）；若 AMD 欲在物理 AI／世界模型這波浪潮中站穩腳步，可能需要評估 ROCm 對 mixture-of-transformers 架構、大規模多模態資料管線、以及邊緣推論（對應 Cosmos edge 模型）的支援與效能表現，這是一個值得深入調查的潛在缺口，但目前僅為推測，需要進一步查證 ROCm 生態現況與 Cosmos 3 生態系是否有任何互通性。