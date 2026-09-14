---
layout: paper
title: "LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks"
section: vla
page_id: "1945538792"
permalink: /vla/lohovla-a-unified-vision-language-action-model-for-long-horizon-embodied-tasks-1945538792/
---

**Paper** : [LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks](https://arxiv.org/abs/2506.00411)  
**Source** : arXiv  
**arXiv ID** : 2506.00411

### Abstract

真實世界的具身智能代理（embodied agents）常面臨長時程（long-horizon）任務——高層目標需要多步驟才能完成，而非單一動作即可達成。要成功處理這類任務，需要同時具備高層任務規劃（把目標拆解成子任務）與低層動作控制（生成精確機器人動作）的能力。既有的 VLA 模型常在規劃上表現不佳，而階層式架構又容易出現協調問題。本文提出 LoHoVLA，一個統一的 VLA 框架，利用大型預訓練視覺語言模型（VLM）作為骨幹，同時生成語言 token（用於子任務生成）與動作 token（用於機器人動作預測），並搭配階層式閉環控制機制來降低高層規劃與低層控制各自產生的誤差。作者同時建構了 LoHoSet 資料集（基於 Ravens 模擬器，20 個長時程任務，每個任務 1000 筆專家示範）用於訓練與驗證。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945538792_lohovla_fig1.png) 

_Figure 1: LoHoVLA 概論圖與方法架構圖 ——上方對比 vanilla VLA 與階層式架構的差異，下方展示 LoHoVLA 統一模型同時生成語言子任務 token 與動作 token 的整體架構。_

  * **要解決的問題** ：長時程具身任務需要同時做「任務規劃」與「動作控制」，標準 VLA 模型常在規劃階段失敗，而階層式（規劃器+控制器分離）架構又容易發生兩層之間的協調不一致問題。
  * **Main method** ：LoHoVLA 用單一大型預訓練 VLM 作為共享骨幹，同時輸出語言 token（子任務描述）與動作 token（機器人動作），讓兩者共享同一份表示（representation），以提升跨任務的泛化能力；並加入「階層式閉環控制（hierarchical closed-loop control）」機制，讓上層規劃結果與下層執行結果能互相回饋、修正誤差。
  * **和以往方式的差異** ：標準單體 VLA 模型通常直接把語言指令映射到動作，缺乏顯式的子任務規劃步驟；傳統階層式架構則將規劃器與控制器分開訓練/部署，容易產生模組間不一致。LoHoVLA 用「統一模型、共享表示」的方式合併兩者，同時保留閉環修正機制。
  * **架構/流程描述** ：輸入視覺觀察與語言目標後，VLM 骨幹先生成語言 token 形式的子任務（sub-task），再由同一模型接續生成對應的機器人動作 token；執行過程中透過閉環回饋（觀察執行結果並反饋給規劃/控制模組）持續修正子任務與動作，降低因規劃錯誤或控制誤差累積導致的失敗。



### Result

  * 實驗顯示 LoHoVLA 在 Ravens 模擬器的長時程具身任務上，顯著超越階層式方法與標準 VLA 方法。
  * 摘要並未提供具體數值（如成功率百分比），僅以「significantly surpasses」描述其優勢，需要查證全文以取得量化比較數據。
  * 是否公正：目前評測僅限於作者自建的 LoHoSet 資料集（基於 Ravens 模擬器），並非在通用公開基準（如 LIBERO）上驗證，其泛化性與跨基準比較需要查證其他論文的比較數據。



### Limitation

  * 論文本身（摘要層級）沒有明確自陳限制段落。
  * 從方法設計看，評測資料集為作者自建（LoHoSet），任務種類（20 個）與模擬器（Ravens）范圍相對有限，可能存在對自建資料集「量身打造」而導致結果偏樂觀的風險。
  * 摘要未提及是否有真實機器人（real-robot）驗證，僅限於模擬器內實驗，實際部署可行性需要查證全文。



### Related work

  * 摘要提及與「既有 VLA 模型」及「階層式架構」相比，但未列出具體比較論文名稱。
  * 暫無發現更新的相關研究可直接引用比較（此論文發表於 2025 年 5 月，後續是否有直接延伸工作需要進一步查證）。
  * Related work 值得 survey 的程度：中等，此文提出的「統一語言+動作 token 生成」思路與 DeepThinkVLA、LaRA-VLA 等「CoT/推理注入」論文的核心議題（如何在動作生成中融入高層語意規劃）相關，值得放在同一脈絡下比較閱讀。



### Conclusion

  * 本文是較早期（2025年5月）提出「統一模型同時處理長時程規劃與動作控制」思路的代表作之一,對理解 VLA 領域「規劃-控制一體化」設計脈絡有參考價值,但因為只在自建模擬資料集驗證，工程落地前建議先查證全文的真實機器人結果與更廣泛基準比較。
  * 與其他重要文章的關係：本文屬於「統一 VLA 框架處理長時程任務」路線的先驅工作之一，後續如 DeepThinkVLA、LaRA-VLA 等論文在「如何讓模型做多步推理再行動」議題上可視為同一大方向的延伸（雖然具體技術路徑不同：LoHoVLA 走子任務語言 token 生成，DeepThinkVLA/LaRA-VLA 走顯式或潛在 CoT 推理）。
  * 對 ROCm/AMD 的關聯：摘要未提及訓練/推理硬體或框架細節，看不出與 ROCm/AMD 的明確關聯，需要查證全文的實作環境。