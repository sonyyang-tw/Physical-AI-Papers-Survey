---
layout: paper
title: "Ctrl-World: A Controllable Generative World Model for Robot Manipulation"
section: wm
page_id: "1945391989"
permalink: /wm/ctrl-world-a-controllable-generative-world-model-for-robot-manipulation-1945391989/
---

**Paper** : [Ctrl-World: A Controllable Generative World Model for Robot Manipulation](https://arxiv.org/abs/2510.10125)  
**Source** : arXiv / ICLR 2026(已被接受)  
**arXiv ID** : 2510.10125

### Abstract

Generalist機器人政策(generalist robot policy)已能執行大量操作技能,但要評估與改進它們面對「未見過的物件與指令」時的表現仍然困難:嚴謹的評估需要大量真實世界的rollout,系統性改進則需要額外的、帶有專家標註的修正資料,兩者都緩慢、昂貴且難以擴展。World model提供了一個可擴展的替代方案,讓政策可以在「想像空間」中rollout。本文提出Ctrl-World,一個可控的多視角(multi-view)world model,可用來評估並改進generalist機器人政策的指令遵循能力。模型透過pose-conditioned記憶檢索機制維持長時序一致性,並透過frame-level的動作條件化達成精確的動作控制。使用DROID資料集(95k條軌跡、564個場景)訓練後,該模型可在新場景與新相機視角下生成20秒以上、時空一致的軌跡。作者證明該方法可在不需真實機器人rollout的情況下準確地為政策表現排序,並藉由在想像中合成成功軌跡並用其做監督式微調,將政策成功率提升44.7%。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391989_ctrlworld_fig1.png) 

_Figure 1: Ctrl-World overview — policy-in-the-loop rollouts with generalist robot policies for evaluation and improvement._

![Figure]({{ site.baseurl }}/assets/images/1945391989_ctrlworld_fig2.png) 

_Figure 2: Ctrl-World architecture — multi-view joint prediction, pose-conditioned memory retrieval, and frame-level action conditioning._

  * 要解決的問題:現有generalist機器人政策評估與改進的成本高(需要大量真實rollout及專家標註修正資料),而既有的world model無法同時支援多視角預測、細粒度動作控制、以及長時序一致的多步互動,因此不足以模擬現代generalist政策的部署場景。
  * Main method:Ctrl-World是一個以Stable Video Diffusion(SVD)為預訓練骨幹並微調而成的可控多視角world model,核心設計包含:(1) pose-conditioned記憶檢索機制,用於維持長時序(20秒以上)的時空一致性,即使相機視角改變或場景是全新的;(2) frame-level動作條件化,讓每一幀影像生成都能精準對應到機器人動作,達成細粒度的動作控制。
  * 和以往方式的差異:相較於過去只能做單視角預測、動作控制粗糙、或長時序容易漂移(drift)的world model(例如作為主要baseline的IRASim,代表僅支援單視角的先前動作條件化模擬方法),Ctrl-World支援多視角、細粒度動作控制、且能維持長時序一致性,使其能與現代generalist政策(如VLA policy)相容並互動。
  * 重要方法設計描述:整體流程可理解為——世界模型以SVD的影像擴散骨幹為基礎,輸入為多視角觀測與逐幀動作序列;記憶檢索模組會依據當前相機姿態(pose)去檢索歷史上相關的視覺記憶片段,作為生成新影格時的長程參考,避免長horizon rollout時的場景漂移或物件消失;動作條件化則是在每一幀的生成過程中注入該幀對應的機器人動作向量,讓模型能對細微的動作變化(如夾爪開合、微小位移)做出對應的視覺反應。



### Result

  * 在DROID資料集上訓練後,模型能在新場景與新相機擺放位置下生成超過20秒、時空一致的軌跡。
  * 該world model能不需真實機器人rollout就準確地為不同政策的表現排序(policy evaluation)。
  * 透過在想像空間中合成成功的軌跡,並用來對政策做監督式微調(supervised fine-tuning),可將政策成功率提升44.7%。
  * 摘要與可取得的資訊未提供與其他論文(如WEAVER、τ0-WM等同類world model)直接的量化比較數據;需要查證其他論文的比較數據以確認Ctrl-World在各項指標(如政策排序相關性、長時序一致性)上的相對優劣。



### Limitation

  * 論文摘要與可取得資訊中未明確自陳limitation的段落;需要查證全文(Limitation/Discussion章節)以確認作者自陳的限制。
  * 從結果推論的潛在弱項:模型訓練資料為DROID(95k條軌跡、564個場景),仍是特定機器人平台/場景分佈下的資料,對於完全不同的機器人形態(morphology)或全新任務類型的泛化能力尚不明朗;此外,20秒的長時序一致性雖優於過去方法,但對於更長時間尺度(分鐘級)的任務規劃可能仍有限制。



### Related work

  * 由作者群(Yanjiang Guo、Chelsea Finn等)延伸的後續工作VLAW(arXiv:2602.12063)直接引用並建立在Ctrl-World之上,聚焦於用真實世界rollout資料迭代改進world model保真度,再用改進後的world model反向提升VLA政策,可視為Ctrl-World概念的自然延伸。
  * 同期/後續的WEAVER(arXiv:2606.13672)也是針對機器人操作的world model,強調同時滿足fidelity、consistency、efficiency三個目標,可作為對比研究對象。
  * 值得survey的程度:高。這是這個子領域(robot manipulation world model)內經常被後續論文引用的重要baseline之一。



### Conclusion

  * 整體評價:值得參考。Ctrl-World針對「generalist機器人政策評估與改進成本過高」這個實務痛點,提出了一個具體可行且已在真實硬體上驗證的解法(44.7%成功率提升是相當顯著的數字),且開源了程式碼與模型(Hugging Face、GitHub),對於想要建立評估/改進pipeline的團隊有直接參考價值。
  * 與其他重要文章的關係:它是VLAW(同作者群後續工作)的直接基礎,也是WEAVER、τ0-WM等同時期robot manipulation world model論文比較與挑戰的對象之一,可視為此波「用world model評估/改進VLA政策」研究浪潮的代表作之一。
  * ROCm/AMD相關性:論文本身聚焦於世界模型的架構設計與機器人資料,並未提及訓練/推論所使用的硬體平台或ROCm相關議題。從摘要與可得資訊看不出與ROCm/AMD有明確關聯;若要評估在AMD GPU上部署此類SVD-based大型影片擴散模型的可行性,需要另外查證其計算資源需求(模型大小、推論延遲)等細節(全文未明確提及)。