---
layout: paper
title: "Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines"
section: vla
page_id: "1945392329"
permalink: /zh/vla/vision-language-action-in-robotics-a-survey-of-datasets-benchmarks-and-data-engi-1945392329/
---

**Paper** : [Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines](https://arxiv.org/abs/2604.23001)  
**Source** : arXiv (cs.RO, cs.AI); TMLR (peer-reviewed, OpenReview: https://openreview.net/forum?id=tAaWFpvnmm)  
**arXiv ID** : 2604.23001

### Abstract

儘管 Vision-Language-Action（VLA）模型已取得顯著進展，但一個核心瓶頸長期未被充分檢視:支撐具身學習（embodied learning）的資料基礎設施。本篇 survey 主張，VLA 未來的進展將較少取決於模型架構，而更取決於高保真資料引擎（data engine）與結構化評估協議的協同設計。作者提出一個以資料為中心的系統性分析框架，圍繞三大支柱：資料集（datasets）、基準測試（benchmarks）與資料引擎（data engines）。在資料集方面，依據具身多樣性、模態組成與動作空間形式，對真實世界與合成語料進行分類，揭露一個持續存在的保真度-成本權衡（fidelity-cost trade-off），根本性地限制了大規模資料收集。在 benchmark 方面，同時分析任務複雜度與環境結構，揭露既有評估協議在組合泛化（compositional generalization）與長時程推理評估上的結構性缺口。在資料引擎方面，檢視模擬式、影片重建式與自動任務生成式三類範式，指出它們在物理真實性（physical grounding）與 sim-to-real 遷移上的共同限制。綜合以上分析，作者歸納出四個尚待解決的開放挑戰:表徵對齊（representation alignment）、多模態監督（multimodal supervision）、推理評估（reasoning assessment），與可擴展資料生成（scalable data generation）。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392329_survey2_fig2.png) 

_Figure 2: Survey scope overview._

  * 要解決的問題：VLA 領域普遍聚焦於模型架構創新,但資料基礎設施（datasets、benchmarks、data engines）作為背後真正的瓶頸卻長期被忽視;本文試圖系統性梳理這個被低估的問題領域。
  * Main method：這是一篇 survey,其方法是提出一套三支柱分類框架（datasets / benchmarks / data engines）,並沿著多個維度（具身多樣性、模態組成、動作空間形式、任務複雜度、環境結構、資料生成範式）對現有文獻進行系統性歸納與比較分析,而非提出新模型或新演算法。
  * 和以往方式的差異：以往許多 VLA 相關 survey 多以模型架構或訓練方法為主軸,本文則刻意將視角轉向資料層,並將 benchmark 設計與 data engine 一併納入同一分析框架,強調三者需要協同設計（co-design）而非分開討論。
  * 重要方法設計描述：全文的分析邏輯可以想像成三層結構——最底層是資料集層,沿具身類型 x 模態 x 動作空間三個軸分類,指出真實資料保真度高但收集成本高、合成資料成本低但保真度受限的權衡關係;中層是 benchmark 層,同時檢視任務的組合複雜度與環境結構,找出現有協議在組合泛化與長時程推理評估上的系統性空白;最上層是 data engine 層,比較模擬引擎、以影片重建動作標籤的方法,以及自動任務生成方法三種資料生成路徑,並指出它們共同面臨物理真實性不足與 sim-to-real gap 的問題。最終將三層分析收斂為四個開放挑戰的討論。



### Result

  * 由於這是 survey 論文,並無傳統意義上的實驗 result;其成果在於系統性地識別出四個開放挑戰（表徵對齊、多模態監督、推理評估、可擴展資料生成）,並揭露現有 datasets/benchmarks/data engines 在保真度-成本權衡、組合泛化評估、sim-to-real 遷移上的結構性缺口。
  * 是否公正：survey 類論文的公正性取決於其文獻涵蓋的全面性與分類是否有代表性偏誤;本文已通過 TMLR 同行評審,具一定的學術把關,但摘要本身未列出具體涵蓋了多少篇文獻或涵蓋時間範圍,需要查證全文的方法論章節以評估其系統性程度。
  * 需要查證其他論文的比較數據：由於是 survey,其結論是否與其他同類 survey 的判斷一致,需要進一步比對,摘要未提供相關對照資訊。



### Limitation

  * 摘要中沒有明確自陳的 limitation 段落,需要查證全文（通常 survey 論文會討論其文獻覆蓋範圍的時間截止點、分類框架的主觀性、以及未涵蓋的新興子領域）。
  * 從內容主軸推測,其潛在限制可能包括：三支柱框架雖然系統化,但可能無法完全涵蓋 VLA 資料基礎設施的所有面向（例如資料標註品質控管、隱私與資料授權議題等）,且作為 survey 必然存在文獻截止時間的局限,可能無法涵蓋 2026年4月之後發表的最新資料集/benchmark。



### Related work

  * 此 survey 本身即是對 related work 的系統性整理,其涵蓋的 benchmark 議題（組合泛化、長時程推理評估缺口）與同批次論文中的 VLABench（強調長時程推理任務）、vla-eval（強調評估流程工程化）、VLA-REPLICA（強調真實世界可重現性）高度呼應,可視為這些具體 benchmark/工具論文背後的問題脈絡說明。
  * 暫無發現比本文更新且同等系統性的 VLA 資料基礎設施 survey。
  * Related work 值得 survey 的程度高：作為一篇經同行評審的系統性 survey,非常適合作為研究 VLA 資料/benchmark 議題的入門與地圖式參考文獻,特別是對於想要規劃資料收集或評估策略的團隊。



### Conclusion

  * 綜合評價：這是一篇有明確問題意識且經過同行評審把關的高品質 survey,對於想要系統性理解 VLA 資料基礎設施現況與挑戰的讀者（尤其是規劃資料收集/評估策略的工程團隊）非常值得參考。
  * 與其他重要文章的關係：此 survey 為同批次的 VLABench、vla-eval、VLA-REPLICA 等具體 benchmark/工具論文提供了更高層次的問題脈絡,說明這些工具分別在解決 survey 中提及的哪些結構性缺口。
  * 對 ROCm/AMD：survey 聚焦於資料與評估基礎設施,而非底層運算硬體/加速器選型,因此看不出與 ROCm/AMD 有明確的直接關聯;不過其中提及的大規模資料生成與模擬對運算資源需求很高,若 AMD 想在此領域切入,可能的機會點在於為模擬式 data engine 提供 ROCm 加速的模擬/渲染管線,但摘要本身並未提供支持此判斷的具體細節,此為推測方向,需要進一步查證。