---
layout: paper
title: "PhyGround: Benchmarking Physical Reasoning in Generative World Models"
section: wm
page_id: "1945539592"
permalink: /Physical-AI-Papers-Survey/wm/phyground-benchmarking-physical-reasoning-in-generative-world-models-1945539592/
---

**Paper** : [PhyGround: Benchmarking Physical Reasoning in Generative World Models](https://arxiv.org/abs/2605.10806)  
**Source** : arXiv (cs.CV / cs.AI / cs.LG)，Preprint，專案頁：<https://phyground.github.io/>  
**arXiv ID** : 2605.10806

### Abstract

PhyGround 是一個針對「生成式世界模型（影片生成模型）是否真正理解物理規律」而設計的評測基準（benchmark）。作者指出，現有的物理導向影片評測基準雖已有進展，但仍面臨三大挑戰：評測框架過於粗略而掩蓋了特定物理定律層面的失敗、標註者的回應偏差與疲勞影響判斷的有效性、以及自動化評測器對物理不夠敏感或難以稽核。PhyGround 包含 250 個經策劃的 prompt，每個都附有預期的物理結果，並涵蓋固體力學、流體力學與光學共 13 類物理定律的分類法（taxonomy），每個定律都被拆解為可觀察的子問題以支援逐定律的診斷。作者透過大規模、品質控管的人類研究（借鑑社會科學實驗設計）評估 8 個現代影片生成模型，共有 459 名標註者提供 5,796 份完整標註與超過 37,400 個細粒度標籤；品質控管後保留的標註呈現高度的 split-half 模型排名相關性（Spearman's rho > 0.90）。為支援可重現的自動化評測，作者也釋出 PhyJudge-9B，一個開源的、物理專用的視覺語言模型（VLM）評判器，其整體相對偏差顯著低於 Gemini-3.1-Pro（3.3% 對 16.6%）。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539592_phyground_fig1.png) 

_Figure 1: Overview of PhyGround - 將每個影片生成模型的整體物理推理分數拆解為13種物理定律的個別分數,由459位標註者進行大規模、有品質控管的人工評估。_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539592_phyground_fig5.png) 

_Figure 5: Annotation design workflow - PhyGround人工標註流程設計架構圖。_

  * 要解決的問題：如何嚴謹、細粒度地評估影片生成／世界模型是否遵守真實世界的物理規律，而非僅憑粗略的整體評分掩蓋特定物理定律上的失敗；同時要解決人類標註品質不穩定（偏差、疲勞）與自動化評判器物理知識不足、難以稽核的問題。
  * Main method：PhyGround 建立一套「準則導向（criteria-grounded）」的基準，核心設計包括：
    * 250 個經策劃的 prompt，每個都標註了預期物理結果（expected physical outcome）。
    * 13 類物理定律的分類法，橫跨固體力學、流體動力學與光學。
    * 每個定律拆解為可觀察的子問題（sub-questions），使評測能做到逐定律（per-law）的診斷，而非單一整體分數。
    * 借鑑社會科學實驗設計方法，控管大規模人類標註（459 人、5,796 份標註、37.4K 細粒度標籤）的品質，並用 split-half 方法驗證標註可靠性。
    * 釋出 PhyJudge-9B，一個經物理知識強化訓練的開源 VLM 評判器，用以自動化複現評測。
  * 與以往方式的差異：以往的物理向影片基準常將多個物理概念/定律糾纏在單一測試題中評分，難以定位具體失敗原因；PhyGround 透過「定律拆解成子問題」的設計做到解耦（disentangled）評測，並用社會科學等級的實驗設計來控管人類標註品質，同時提供比通用 VLM（如 Gemini-3.1-Pro）偏差更低的專用評判模型。
  * 重要方法設計描述：可以想像整個評測流程分三層——(1) Prompt 層：250 個 prompt 覆蓋 13 類物理定律，每個 prompt 附帶明確的「預期物理結果」描述；(2) 生成層：8 個現代影片生成模型分別依 prompt 生成影片；(3) 評測層：對每部生成影片，標註者針對該定律下的一組可觀察子問題（例如「物體是否維持恆定體積」、「液體是否符合黏度預期行為」）逐項打分，形成細粒度標籤；同時 PhyJudge-9B 作為自動化替代評判器，經過品質控管的人類標籤訓練/校準後，可在無需大規模人類標註的情況下重現評測結果。



### Result

  * 主要成果：完成了對 8 個現代影片生成模型的大規模人類評測（5,796 份標註、37.4K 細粒度標籤），標註品質經 split-half 驗證達到高相關性（Spearman's rho > 0.90），顯示評測結果穩定可信；同時 PhyJudge-9B 相較於 Gemini-3.1-Pro 有更低的評判偏差（3.3% 對 16.6%）。
  * 增強部分：主要增強「物理推理評測的細粒度診斷能力」（逐定律分析而非整體評分）與「自動化評判的物理準確度／可稽核性」（PhyJudge-9B 優於通用大型 VLM）。
  * 是否公正：摘要中提供的 PhyJudge-9B vs Gemini-3.1-Pro 偏差比較（3.3% vs 16.6%）是作者自己的評測結果，屬於自我報告的比較；由於這是一個新發布的 benchmark（2026年5月），目前需要查證是否已有其他論文使用 PhyGround 對相同或不同模型集合重新評測、驗證排名一致性。



### Limitation

  * 論文中自陳的限制：僅根據 arXiv abstract 頁面資訊，摘要本身未詳列 limitation 章節內容（全文56頁、39圖、40表，需要查證全文的 limitation/discussion 章節）。
  * 從結果推測的弱項：
    * 僅評測了 8 個現代影片生成模型，覆蓋範圍可能無法代表所有主流模型（尤其新模型更新速度快，benchmark 可能很快過時）。
    * 大規模人群標註（459 人）雖經品質控管，但人類對「物理正確性」的主觀判斷仍可能存在文化/背景差異，論文雖借鑑社會科學實驗設計以控管，但無法完全消除主觀性。
    * PhyJudge-9B 作為 9B 規模的專用模型，其物理知識覆蓋範圍是否能推廣到 PhyGround 未涵蓋的物理現象（例如電磁學、熱力學等未列入 13 類定律的領域），摘要未說明。



### Related work

  * 需要查證其他論文的比較數據：PhyGround 與同期（2601, 即 2026 年 1 月發表）的 WorldBench（arXiv:2601.21282，本次同時處理的另一篇論文）主題高度相似，皆聚焦物理定律的解耦評測，值得交叉比較兩者的分類法設計、評測規模與發現的模型失敗模式是否一致。
  * Related work 值得 survey 的程度：高。物理推理評測是目前 world model / 影片生成領域的熱門子方向（PhyGround、WorldBench 等benchmark 密集出現於 2026 上半年），建議整理成一個小型 survey 專門比較各基準的分類法與發現。



### Conclusion

  * 綜合評價：PhyGround 是一個方法論嚴謹（借鑑社會科學實驗設計）、規模龐大（37.4K 標籤）且提供可重現自動化評測工具（PhyJudge-9B）的物理推理基準，對於想要系統性評估或改進世界模型物理一致性的研究者，具有高度參考價值；其對「解耦式」評測的設計理念也值得其他 benchmark 借鏡。
  * 與其他重要文章的關係：與 WorldBench（同樣是 2026 年出現的物理解耦評測基準）構成直接的方法論競爭/互補關係，兩者都指出現有影片生成模型在物理一致性上普遍不足；建議兩篇一起研讀比較其分類法差異。
  * ROCm/AMD 待補強部分：論文未提及訓練/推論所用硬體平台，看不出與 ROCm/AMD 的明確關聯。若 AMD 團隊要使用 PhyGround 評測自家（或以 ROCm 訓練/推論的）世界模型，可直接採用其公開的 prompts、人類標註與 PhyJudge-9B 評判器，但論文本身未涉及 ROCm 相關內容，不宜臆測。