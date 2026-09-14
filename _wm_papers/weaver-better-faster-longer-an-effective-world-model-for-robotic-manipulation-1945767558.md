---
layout: paper
title: "WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation"
section: wm
page_id: "1945767558"
permalink: /wm/weaver-better-faster-longer-an-effective-world-model-for-robotic-manipulation-1945767558/
---

**Paper** : [WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation](https://arxiv.org/abs/2606.13672)  
**Source** : arXiv  
**arXiv ID** : 2606.13672

### Abstract

World model(WM,即學習出來的模擬器)對機器人領域的潛在影響非常深遠——政策評估、政策改進、測試時規劃——且都能在有限的真實世界互動下達成。但要解鎖這些下游能力,WM需要同時滿足三個要件:(1) 保真度(fidelity,產生與現實相關的模擬軌跡)、(2) 一致性(consistency,產生長時序內連貫一致的模擬軌跡)、(3) 效率(efficiency,快速產生模擬軌跡)。本文提出WEAVER(World Estimation Across Views for Embodied Reasoning),一個同時達成上述三項要件的WM架構,在機器人操作任務上取得state-of-the-art結果。WEAVER是一個多視角(multi-view)WM,透過flow-matching損失訓練來預測未來潛變量與獎勵值。作者提煉出模型架構、記憶機制、預測目標等關鍵設計決策,以解鎖過去world model方法難以處理的長時序動態操作任務。作者在真實機器人硬體上應用WEAVER,證明其在政策評估(與真實世界成功率相關係數ρ=0.870)、政策改進(在π0.5機器人基礎模型上提升38%真實世界成功率)、測試時規劃(提升14%真實世界成功率,同時比之前的world model快5-10倍)上均有效。WEAVER在分佈外(out-of-distribution)場景評測中也優於先前的world model。

### Method

![Figure](/assets/images/1945767558_weaver_fig1.png) 

_Figure 1: WEAVER — a world model satisfying high fidelity, long-horizon consistency, and efficient generation, enabling policy evaluation, policy improvement, and test-time planning._

![Figure](/assets/images/1945767558_weaver_fig2.png) 

_Figure 2: WEAVER architecture — world model encodes memory/history/action for latent rollouts, with a latent verifier (reward + critic heads) steering the policy distribution._

  * 要解決的問題:過去的world model難以同時滿足fidelity、consistency、efficiency三個要件——例如高保真的方法往往速度慢(如需要多步擴散去噪),速度快的方法又難以維持長時序一致性,導致無法真正支撐長時序、動態的機器人操作任務所需的政策評估、改進與測試時規劃。
  * Main method:WEAVER是一個多視角world model,以flow-matching損失訓練,同時預測未來的(視覺)潛變量與獎勵值(reward value)。作者系統性地梳理並提煉出橫跨模型架構、記憶機制(memory)、預測目標(prediction objective)三個維度的關鍵設計決策,用以解鎖此前world model方法難以處理的長時序、動態操作任務。
  * 和以往方式的差異:相較於過去(包含Ctrl-World等)偏重單一目標(例如只重視長時序一致性或只重視動作可控性)的world model,WEAVER的核心貢獻在於「同時」達成三個要件,尤其在效率上有5-10倍的加速,同時保持甚至提升保真度與一致性,並額外預測獎勵值以支援測試時規劃(而不只是被動地生成畫面)。
  * 重要方法設計描述:整體流程可理解為——模型以多視角觀測作為輸入,透過flow-matching(一種比傳統擴散模型步驟更少、生成更快的生成建模技術)來預測未來的潛在表示與對應的獎勵/進度分數;記憶機制的設計讓模型能在長horizon下保留關鍵的場景與物件資訊,避免像素級細節的擴散生成帶來的高延遲;預測目標同時包含視覺潛變量與獎勵訊號,使得同一個模型既可以「想像」未來畫面,也能直接輸出量化的評分,供政策評估或測試時的候選動作篩選使用。



### Result

  * 政策評估(policy evaluation):與真實世界成功率的相關係數達到ρ=0.870,顯示world model的評分能相當準確地反映真實表現。
  * 政策改進(policy improvement):在π0.5機器人基礎模型基礎上,真實世界成功率提升38%。
  * 測試時規劃(test-time planning):真實世界成功率提升14%,同時比先前的world model快5-10倍。
  * 在分佈外(out-of-distribution)場景下,WEAVER的表現也優於先前的world model。
  * 摘要未提供與Ctrl-World、τ0-WM等同類論文的直接數字對比(例如同一基準下的成功率百分比差異),需要查證其他論文的比較數據以確認相對優劣,尤其WEAVER與Ctrl-World都使用π系列或類似的機器人基礎模型做為改進對象,值得交叉比對。



### Limitation

  * 摘要中未包含明確的Limitation自陳段落,需要查證全文(Limitation/Discussion章節)以確認作者自陳的限制。
  * 從結果推論的潛在弱項:雖然14%的測試時規劃提升與5-10倍加速看起來顯著,但相對於政策改進的38%提升,測試時規劃的效益相對有限,顯示現階段測試時規劃在效益/成本權衡上可能還有改進空間;此外,論文聚焦於機器人操作(manipulation)任務,對於導航或更複雜的多物件互動場景的泛化能力未在摘要中提及。



### Related work

  * 與Ctrl-World(arXiv:2510.10125)、τ0-WM(arXiv:2606.01027)同屬「機器人操作world model」的研究方向,三者都聚焦於政策評估與改進,是彼此重要的比較對象,尤其Ctrl-World也使用類似的π系列機器人基礎模型作為改進對象,適合進行交叉比較。
  * 暫無發現更新的、直接建立在WEAVER之上的後續研究(截至可查證的資訊)。
  * 值得survey的程度:高。此論文明確提出並系統性驗證了fidelity/consistency/efficiency三要件的框架,對於評估同類world model論文的方法論具有參考價值。



### Conclusion

  * 整體評價:值得參考。WEAVER提出的「fidelity、consistency、efficiency三要件缺一不可」框架具有清晰的問題定義價值,且在真實機器人硬體上的驗證數據(ρ=0.870相關係數、38%成功率提升、5-10倍加速)相當具體,對於想要理解「什麼樣的world model設計才能真正支撐政策評估與改進」的讀者很有參考意義。
  * 與其他重要文章的關係:WEAVER與Ctrl-World、τ0-WM共同構成了2026年機器人操作world model研究的重要三角,分別代表不同的架構取捨(WEAVER強調效率與獎勵預測、Ctrl-World強調pose-conditioned長時序一致性、τ0-WM強調統一策略與模擬的單一backbone)。三者之間的比較(尤其在相同的π系列基礎模型上的改進幅度)值得進一步查證與追蹤。
  * ROCm/AMD相關性:論文聚焦於world model的架構設計與真實機器人驗證,未提及使用的硬體平台或ROCm相關內容。從現有資訊看不出與ROCm/AMD有明確關聯;若考慮flow-matching訓練與推論在AMD GPU上的效率(尤其其強調的5-10倍加速是否與特定硬體優化相關),需要查證全文以確認是否有討論訓練/推論基礎設施細節。