---
layout: paper
title: "VLAW: Iterative Co-Improvement of Vision-Language-Action Policy and World Model"
section: wm
page_id: "1945474219"
permalink: /zh/wm/vlaw-iterative-co-improvement-of-vision-language-action-policy-and-world-model-1945474219/
---

**Paper** : [VLAW: Iterative Co-Improvement of Vision-Language-Action Policy and World Model](https://arxiv.org/abs/2602.12063)  
**Source** : arXiv  
**arXiv ID** : 2602.12063

### Abstract

本文旨在透過迭代式線上互動來改進vision-language-action(VLA)模型的表現與可靠性。由於在真實世界收集政策rollout成本高昂,作者探討是否能用一個學習出來的模擬器——具體來說是動作條件化的視頻生成模型(action-conditioned video generation model)——來產生額外的rollout資料。然而,現有的world model缺乏政策改進所需的物理保真度:它們大多以缺乏多樣物理互動(尤其是失敗案例)覆蓋的示範資料集訓練,且難以準確建模接觸豐富(contact-rich)物件操作中細微但關鍵的物理細節。作者提出一個簡單的迭代改進演算法,利用真實世界的rollout資料來提升world model的保真度,再用改進後的world model反過來生成補充性的合成資料以改進VLA模型。在真實機器人的實驗中,作者用此方法在多個下游任務上改進了一個state-of-the-art VLA模型的表現,相較基礎政策(base policy)絕對成功率提升39.2%,並透過用生成的合成rollout訓練再額外提升11.6%。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474219_vlaw_fig1.png) 

_Figure 1: VLAW overview - learning an action-conditioned world model from limited real-world rollouts to generate large-scale synthetic data in imagination._

![Figure]({{ site.baseurl }}/assets/images/1945474219_vlaw_fig2.png) 

_Figure 3: Detailed VLAW pipeline - rollout, ground world model, generate synthetic trajectories via closed-loop policy-world model interaction, then optimize the VLA policy with a vision-language reward model._

  * 要解決的問題:現有world model因訓練資料缺乏「失敗案例」與細緻的接觸物理覆蓋,保真度不足以支撐政策改進(即用world model生成的合成資料訓練政策,可能因模型模擬失真而產生反效果或無效改進)。
  * Main method:提出一個簡單的迭代式共同改進(iterative co-improvement)演算法:(1) 用真實世界的政策rollout資料(包含成功與失敗案例)來提升world model(動作條件化視頻生成模型)的保真度;(2) 用保真度提升後的world model生成補充性合成rollout資料;(3) 用這些合成資料訓練/微調VLA政策。此過程反覆迭代,讓world model與VLA政策彼此共同改進。
  * 和以往方式的差異:與單純「訓練一次world model後就拿來生成資料改進政策」的方法不同,VLAW強調「迭代」——World model本身也需要持續被真實世界資料修正,尤其著重補足失敗案例與接觸豐富場景的物理細節覆蓋,而非只靠一次性訓練的示範資料。這解決了「World model本身保真度不足,導致用它生成的合成資料無法有效提升政策」的核心問題。
  * 重要方法設計描述:整體流程可理解為一個閉環系統——真實機器人先用當前的VLA政策執行rollout(蒐集包含成功與失敗的真實互動資料);這些真實資料(尤其是失敗案例)被用來重新訓練/微調world model,讓其更準確地模擬接觸物理與失敗模式;接著用更新後的world model,以動作條件化的方式生成大量合成rollout(包含在想像空間中呈現政策執行不同動作後的視覺後果);最後將這些合成資料用於監督式微調VLA政策,提升其成功率。整個循環可重複多輪,World model與VLA政策的品質理論上會逐輪提升。



### Result

  * 在真實機器人的多個下游任務上,相較於基礎政策(base policy),VLAW方法帶來39.2%的絕對成功率提升。
  * 其中,單獨透過「用生成的合成rollout訓練」這一步驟,額外貢獻了11.6%的成功率提升(其餘部分推測來自迭代改進world model本身及其他流程步驟,但摘要未細分各步驟的具體貢獻佔比,需要查證全文以釐清)。
  * 摘要未提供與Ctrl-World(同作者群Yanjiang Guo、Chelsea Finn的前作)在相同任務/基準下的直接數字比較,雖然VLAW明顯是Ctrl-World概念的延伸,但兩篇論文的實驗設定(任務、政策基礎模型)是否完全一致需要查證其他論文的比較數據以確認。



### Limitation

  * 論文摘要中明確指出限制的來源:現有(改進前的)world model「訓練資料缺乏多樣物理互動特別是失敗案例的覆蓋」,以及「難以準確建模接觸豐富物件操作中細微但關鍵的物理細節」——這是作者自陳、並且是VLAW方法試圖解決的核心問題本身,也隱含地說明了此類方法論的根本挑戰所在。
  * 從結果推論的潛在弱項:39.2%的提升雖然顯著,但迭代式共同改進演算法通常需要多輪「真實rollout收集→world model更新→合成資料生成→政策微調」的循環,這意味著仍然需要一定量的真實世界資料收集(雖然比純粹靠人工標註修正資料的方式更有效率),其總體資料收集與計算成本、以及迭代輪數與效益的邊際遞減關係,摘要中並未詳述,需要查證全文。



### Related work

  * 本論文與Ctrl-World(arXiv:2510.10125)高度相關且共享部分作者(Yanjiang Guo、Lucy Xiaoyang Shi、Jianyu Chen、Chelsea Finn),可視為Ctrl-World工作的直接延伸——Ctrl-World建立了可控多視角world model的基礎架構,VLAW則進一步聚焦於「world model本身保真度不足」的問題,並提出迭代式的解法。
  * 與WEAVER、τ0-WM同屬「world model輔助VLA政策改進」的研究方向,適合一併比較不同的資料策略(WEAVER/τ0-WM著重架構統一與效率,VLAW著重迭代式資料保真度提升)。
  * 值得survey的程度:高,尤其對於想要理解「world model保真度不足如何影響下游政策改進效果」這個實務問題的讀者非常有參考價值。



### Conclusion

  * 整體評價:值得參考。VLAW提出了一個直觀但重要的洞察——即使有了像Ctrl-World這樣的可控world model,若其保真度(尤其是失敗案例與接觸物理細節)不足,直接拿來生成合成資料訓練政策的效果會受限;透過迭代式的真實資料回饋來持續修正world model,是務實且有效的解法(39.2%的提升是相當有說服力的證據)。
  * 與其他重要文章的關係:VLAW是Ctrl-World的直接後續延伸(同作者群),並隱含地挑戰了「一次性訓練好的world model就足以支撐政策改進」這個假設,強調迭代與真實資料回饋的必要性。與WEAVER、τ0-WM相比,VLAW更聚焦於資料層面(而非模型架構層面)的保真度問題,三者可視為互補而非直接競爭的研究方向。
  * ROCm/AMD相關性:論文聚焦於迭代演算法設計與真實機器人驗證,未提及訓練/推論所用的硬體平台。從現有資訊看不出與ROCm/AMD有明確關聯;若要評估此類迭代式訓練(需反覆訓練world model與VLA政策)在AMD硬體上的計算資源需求與效率,需要查證全文以確認是否有相關討論(目前未提及)。