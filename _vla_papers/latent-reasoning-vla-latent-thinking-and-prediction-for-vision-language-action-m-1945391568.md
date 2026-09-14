---
layout: paper
title: "Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models"
section: vla
page_id: "1945391568"
permalink: /vla/latent-reasoning-vla-latent-thinking-and-prediction-for-vision-language-action-m-1945391568/
---

**Paper** : [Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models](https://arxiv.org/abs/2602.01166)  
**Source** : arXiv, Accepted by ICML 2026  
**arXiv ID** : 2602.01166

### Abstract

Vision-Language-Action (VLA) 模型能從 Chain-of-Thought (CoT) 推理中受益，但既有作法會產生高推理延遲開銷，且依賴離散的推理表示（文字/視覺 token），與連續的感知和控制訊號不匹配。本文提出 Latent Reasoning VLA (LaRA-VLA)，一個統一的 VLA 框架，將多模態 CoT 推理內化為連續的潛在表示（latent representation）用於具身動作生成。LaRA-VLA 在潛在空間中同時完成推理與預測，推論時完全不需要顯式生成 CoT 文字，因而能實現高效率、以動作為導向的控制。為了實現這種潛在具身推理，作者提出「課程式（curriculum-based）」訓練範式，逐步從顯式的文字/視覺 CoT 監督過渡到潛在推理，最終讓潛在推理動態去條件化動作生成。作者建構了兩個結構化 CoT 資料集，並在模擬基準與長時程真實機器人操作任務上驗證，結果顯示 LaRA-VLA 持續優於當前最先進的 VLA 方法，同時相較顯式 CoT 方法能降低最多 90% 的推理延遲。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391568_lara_vla_fig1.png) 

_Figure 1: CoT 形式比較 ——(a) 文字CoT顯式生成推理token；(b) 多數視覺CoT以離散視覺目標token表示推理；(c) LaRA-VLA 將文字與視覺推理內化為連續潛在表示（latent）。_

![Figure]({{ site.baseurl }}/assets/images/1945391568_lara_vla_fig2.png) 

_Figure 2: LaRA-VLA 方法架構總覽 ——訓練分三階段：(i) 顯式CoT微調並對齊視覺預測潛在與逆動力學表示、(ii) 潛在化階段、(iii) 動作學習階段。_

  * **要解決的問題** ：顯式 CoT-VLA 方法（如生成文字推理鏈）雖然有效，但會拖慢推理速度，且文字/離散 token 形式的推理與連續的視覺感知、連續動作控制在表示形式上不匹配。
  * **Main method** ：LaRA-VLA 把多模態 CoT 推理「內化」成連續的潛在向量表示，讓模型在潛在空間中同時做「思考」（latent thinking）與「預測」（prediction），推論時跳過顯式文字 CoT 生成步驟，直接從潛在推理狀態產生動作。
  * **和以往方式的差異** ：既有 CoT-VLA（如 DeepThinkVLA 走顯式文字CoT + RL對齊路線）仍需要在推理時真的生成一段文字或視覺推理鏈，帶來延遲；LaRA-VLA 選擇讓推理「隱性化」，僅在訓練時借助顯式 CoT 監督逐步引導模型學會用潛在向量表達推理過程，推論時不再需要文字化輸出。
  * **架構/流程描述** ：訓練採用課程式（curriculum）三階段：(1) 先用顯式文字與視覺 CoT 監督進行訓練，讓模型學會「該如何推理」；(2) 逐步將這些顯式推理過渡、壓縮為連續的潛在表示；(3) 最後階段讓潛在推理動態直接條件化（condition）動作生成模組，完成端到端的「潛在思考→動作」流程。訓練資料包含作者自建的兩個結構化 CoT 資料集。



### Result

  * LaRA-VLA 在模擬基準與長時程真實機器人操作任務上，全面優於當前最先進（state-of-the-art）VLA 方法。
  * 相較於顯式 CoT-based 方法，推理延遲最多降低 90%。
  * 摘要未提供具體任務成功率等量化數字，需要查證全文取得詳細數據；且該文已被 ICML 2026 接受，代表已通過同行審查。
  * 是否公正：摘要中「持續優於 SOTA」的說法需要查證其他論文（例如 DeepThinkVLA）在相同基準上的具體數據是否有可比性，兩者可能使用不同基準或任務設定,需要進一步比對。



### Limitation

  * 論文本身摘要未明確列出限制，但從方法設計推論：將推理「潛在化」雖然降低延遲，但可能犧牲一定的可解釋性（無法像顯式 CoT 一樣直接讀懂模型的推理過程），這點在摘要中未被提及，需要查證全文是否有討論可解釋性/除錯難度的取捨。
  * 課程式訓練需要多階段、逐步從顯式過渡到潛在的訓練流程，訓練複雜度與所需資料/計算資源可能較高，摘要未提供具體訓練成本資訊。



### Related work

  * 摘要中提及會與「當前最先進的 VLA 方法」比較，但未列出具體論文名稱，可能包含如 DeepThinkVLA 之類的顯式 CoT-VLA 方法。
  * 暫無發現更新的相關研究（本文本身即為 2026 年 2 月提交、5 月修訂、並被 ICML 2026 接受的較新工作）。
  * Related work 值得 survey 的程度：高，此文與 DeepThinkVLA 在「CoT 對 VLA 是否有效」議題上分別給出「顯式 CoT + RL 因果對齊」與「潛在 CoT」兩種不同解法，兩篇合併閱讀能較全面理解該領域目前的技術路線分歧，值得深入比較。



### Conclusion

  * 本文針對 VLA 推理延遲這一實務痛點提出具體解法（潛在推理），且已被 ICML 2026 接受，具有一定學術認可度，值得參考，尤其對關注真實機器人部署延遲/即時性的讀者。
  * 與其他重要文章的關係：本文與 DeepThinkVLA（清單論文1）形成有趣對照——DeepThinkVLA 主張顯式 CoT + 因果對齊（RL）才能讓推理真正有效，LaRA-VLA 則主張把推理「內化」為潛在表示以兼顧效果與效率，兩者可視為「顯式 vs. 隱式」推理路線之爭，值得對照研讀以判斷哪種取捨更適合特定應用場景。
  * 對 ROCm/AMD 的關聯：本文聚焦於降低推理延遲以支援即時控制,這類主題与 VLA-Perf、EcoVLA（本清單論文5、6）等討論推理效能/部署的論文有潛在關聯，但摘要未提及具體硬體平台或框架，看不出與 ROCm/AMD 的直接技術關聯，需要查證全文的實驗硬體環境（是否使用 NVIDIA GPU 為主）。