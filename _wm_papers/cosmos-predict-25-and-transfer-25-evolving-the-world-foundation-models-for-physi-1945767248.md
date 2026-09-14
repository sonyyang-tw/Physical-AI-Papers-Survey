---
layout: paper
title: "Cosmos Predict 2.5 and Transfer 2.5: Evolving the World Foundation Models for Physical AI"
section: wm
page_id: "1945767248"
permalink: /wm/cosmos-predict-25-and-transfer-25-evolving-the-world-foundation-models-for-physi-1945767248/
---

**Paper** : [Cosmos Predict 2.5 & Transfer 2.5: Evolving the World Foundation Models for Physical AI](https://huggingface.co/blog/nvidia/cosmos-predict-and-transfer2-5)  
**Source** : NVIDIA 官方技術部落格 / 技術報告（非傳統同儕審查論文）；相關研究頁面：<https://research.nvidia.com/labs/cosmos-lab/cosmos-predict2.5/> 、 <https://research.nvidia.com/labs/cosmos-lab/cosmos-transfer2.5/> ；GitHub：nvidia-cosmos/cosmos-predict2.5、nvidia-cosmos/cosmos-transfer2.5  
**arXiv ID** : 無正式 arXiv 論文連結可確認（相關基礎研究可能對應 arXiv:2511.00062「World Simulation with Video Foundation Models for Physical AI」，但本篇處理的 Predict 2.5 / Transfer 2.5 版本資訊主要來自官方部落格與 GitHub repo，非本次核實的 arXiv 論文本身，需要查證兩者的確切對應關係）

### Abstract

Cosmos Predict 2.5 與 Cosmos Transfer 2.5 是 NVIDIA Cosmos 世界基礎模型 (World Foundation Models, WFMs) 家族的次世代版本，設計目標為物理 AI 應用（機器人、自動駕駛等）。Cosmos Predict 2.5 將原本分離的三個模型（Text2World、Image2World、Video2World）合併為單一統一架構，能從多種輸入模態生成一致且可控的影片世界，提供 2B 與 14B 兩種模型規模，以 2 億支高品質預訓練影片片段訓練，並採用模型合併與新的強化學習演算法提升品質，可生成長達 30 秒的序列，在針對專屬/領域特定資料做後訓練 (post-training) 時，長尾場景生成準確度最高提升 10 倍。Cosmos Transfer 2.5 建立在 Cosmos Predict 2.5 之上，是具備自適應多模態控制的條件式世界生成模型，能依據邊緣圖、模糊影片、分割圖、深度圖等多種控制輸入（可能來自 IsaacSim 等物理模擬引擎或真實世界影片）生成高品質世界模擬，相較前代 Cosmos-Transfer1-7B，Transfer2.5-2B 模型體積縮小 3.5 倍，但在長影片的品質衰減（hallucination/error accumulation）上表現更佳。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767248_cosmospredict25_fig1.svg) 

_Figure 1: 影片資料整理 (curation) pipeline 總覽 — 將原始多源真實世界影片轉換為高品質、標註、去重的訓練資料集。_

![Figure]({{ site.baseurl }}/assets/images/1945767248_cosmospredict25_fig2.png) 

_Figure 2: Cosmos-Predict2.5 整體架構 — 在潛在空間中反覆堆疊自注意力與交叉注意力區塊，統一 Text2World / Image2World / Video2World 生成流程。_

  * **要解決的問題** ：物理 AI（機器人、自動駕駛）需要大量涵蓋長尾場景（罕見天氣、罕見交互事件等）的高品質模擬訓練資料，同時需要世界模型能根據多種控制訊號（文字、影像、深度圖、分割圖等）生成一致且可控的未來世界狀態，而先前版本的 Cosmos 模型在架構上是分離的 (Text2World/Image2World/Video2World)，且大模型（Transfer1-7B）推論成本高。
  * **Main method** ：
    * Cosmos Predict 2.5：把 Text2World、Image2World、Video2World 三個原本獨立的模型合併為單一統一架構，可接受多模態輸入生成一致的未來世界影片；提供 2B 與 14B 兩種規格；使用 2 億支影片預訓練；引入模型合併 (model merging) 與新的強化學習演算法來提升生成品質；可生成長達 30 秒的連續序列；針對特定領域資料做後訓練時能大幅提升長尾場景生成準確度（最高10倍）。
    * Cosmos Transfer 2.5：建立在 Predict 2.5 之上的條件式生成模型，支援「自適應多模態控制」，可用邊緣圖、模糊化影片、分割圖、深度圖等多種控制輸入（可源自 IsaacSim 等物理模擬引擎，也可源自真實世界影片）來引導世界生成，模型體積比前代（Transfer1-7B）縮小 3.5 倍，卻在長影片生成中維持更好的品質（減少幻覺與誤差累積）。
  * **與以往方式的差異** ：相較 Cosmos 前代版本，Predict 2.5 用單一統一架構取代三個分離模型，簡化了 pipeline 並可能提升跨模態一致性；Transfer 2.5 則在大幅縮小模型體積（3.5倍）的同時提升長影片品質穩定性，顯示效率與品質可以同時改善，而非傳統「縮小模型必然犧牲品質」的取捨。此外還新增了針對邊緣裝置的蒸餾版本 (Distilled Edge model)，支援低延遲推論部署。
  * **重要設計描述** ：Predict 2.5 架構可理解為一個統一的多模態條件生成骨幹，輸入可以是純文字、單張影像、或影片片段，輸出皆為未來世界狀態的影片；訓練流程包含大規模預訓練（2億影片）加上模型合併與RL微調兩階段強化品質。Transfer 2.5 則在此骨幹上疊加一個「自適應多模態控制」模組，能同時或選擇性地吃進多種空間控制訊號（如深度、分割、邊緣），並將這些訊號與模擬引擎（IsaacSim）或真實影片的控制條件對齊，生成物理上合理的世界模擬影片，可用於 sim-to-real 資料增強。



### Result

  * Predict 2.5：後訓練 (post-training) 於專屬/領域資料後，長尾場景生成準確度最高提升 10 倍（相較未後訓練或前代版本，具體對照基準需要查證原始技術報告以確認）。
  * Transfer 2.5：模型體積比 Cosmos-Transfer1-7B 縮小 3.5 倍，且在長影片生成中的品質分數衰減程度（quality score reduction across video chunks）顯著較少，意味著幻覺與誤差累積問題減輕。
  * 後續時間軸更新：2026年2月23日發布了 Transfer2.5 蒸餾版 Edge 模型，支援低延遲邊緣部署，並同步發布對應的 Predict2.5 robot/policy 版本；3月13日的更新提到 Cosmos Transfer 2.5 可支援可擴展、基於物理的照片級真實模擬，涵蓋多樣環境與光照條件，Predict 2.5 則能從多模態輸入生成真實的未來世界狀態並改善長尾場景準確度。
  * 是否公正：以上數據均來自 NVIDIA 官方部落格與技術報告，並非經過同儕審查的獨立第三方驗證，「最高10倍」與「3.5倍縮小、品質更佳」等宣稱需要查證官方 GitHub repo 或 research 頁面上的詳細基準測試表格以了解具體測試場景與對照基準，也需要留意這是廠商自我報告的效能宣稱。
  * 需要查證其他論文/團隊是否有對 Cosmos Predict/Transfer 2.5 做獨立的第三方基準比較。



### Limitation

  * 官方資訊中並未列出明確的「limitation」章節內容（因為這是技術部落格/產品發布性質的文件，而非學術論文），需要查閱 Cosmos Cookbook 或原始技術報告以確認是否有自陳限制。
  * 一個重要的時程限制是：截至 2026 年 6 月 1 日，NVIDIA 已推出下一代 Cosmos 3（統一語言/影像/影片/音訊/動作的全模態世界基礎模型），Cosmos-Transfer2.5 與 Cosmos-Predict2.5 的 GitHub repo 已宣布「不再積極開發，僅提供有限維護更新」，未來新功能將集中在 Cosmos 3 上，這代表 Predict/Transfer 2.5 版本目前已是「過渡世代」產品，其長期支援性有限，選型時需納入考量。



### Related work

  * 更新的相關研究：NVIDIA 已於 2026 年 6 月推出 Cosmos 3，是統一語言、影像、影片、音訊、動作的下一代全模態世界基礎模型，取代 Predict/Transfer 2.5 成為目前最新的旗艦產品，GitHub 組織也已遷移至 github.com/NVIDIA/Cosmos。另外還有相關基礎研究論文 arXiv:2511.00062「World Simulation with Video Foundation Models for Physical AI」可能是 Cosmos 系列的學術對應文獻，值得查證其與 Predict/Transfer 2.5 的具體對應關係。
  * 值得 survey 的程度：高。Cosmos 系列是業界（尤其在物理 AI/機器人 sim-to-real 領域）具指標性的商用世界基礎模型產品線，其技術演進（Predict/Transfer 2.5 → Cosmos 3）代表產業趨勢方向，值得持續追蹤，但因為已快速被 Cosmos 3 取代，建議後續研究重心轉向 Cosmos 3 的技術細節。



### Conclusion

  * 整體評價：Cosmos Predict 2.5 / Transfer 2.5 是 NVIDIA 在物理 AI 世界模型領域的重要商用里程碑產品，展示了統一架構、模型縮小同時提升品質、以及可支援 sim-to-real 資料增強的多模態控制能力，對於想了解業界大規模世界模型產品化路線的工程師有參考價值；但因已快速被 Cosmos 3 取代，其技術生命週期短，實務部署上應優先評估遷移至 Cosmos 3 的可行性。
  * 與其他重要文章的關係：Cosmos 系列代表了與本清單中學術論文（如 Interactive World Simulator、WoVR）不同的技術路線——後者聚焦特定機器人任務的輕量化、可控世界模型，而 Cosmos 走的是大規模、通用化、以 IsaacSim 等模擬引擎整合為核心的工業級世界基礎模型路線，兩者可視為學術界與工業界世界模型研究的互補視角。
  * ROCm/AMD 待補強部分：Cosmos 系列目前的訓練與推論生態（GitHub repo、蒸餾/邊緣部署、Diffusers 支援）明顯以 NVIDIA 自家硬體與 CUDA 生態系為核心（包括對 Blackwell 架構的專門支援），完全沒有提及 ROCm 或 AMD 硬體的相容性。這代表若 AMD 想在物理 AI/世界模型這個新興且快速成長的市場中競爭，Cosmos Predict/Transfer 2.5（及即將主導市場的 Cosmos 3）在 ROCm 上的移植與效能驗證是明確且尚待補強的空白，值得作為 ROCm 生態系優先投入的方向之一。