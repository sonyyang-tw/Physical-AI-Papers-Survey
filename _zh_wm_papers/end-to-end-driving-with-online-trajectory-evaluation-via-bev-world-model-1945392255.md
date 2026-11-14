---
layout: paper
title: "End-to-End Driving with Online Trajectory Evaluation via BEV World Model"
section: wm
page_id: "1945392255"
permalink: /zh/wm/end-to-end-driving-with-online-trajectory-evaluation-via-bev-world-model-1945392255/
---

**Paper** : [End-to-End Driving with Online Trajectory Evaluation via BEV World Model](https://arxiv.org/abs/2504.01941)  
**Source** : arXiv / ICCV 2025(已被接受)  
**arXiv ID** : 2504.01941

### Abstract

End-to-end自動駕駛透過將感知、預測、規劃整合進一個完全可微分(differentiable)的框架,已取得顯著進展。然而,要充分發揮其潛力,有效的線上軌跡評估(online trajectory evaluation)對確保安全性是不可或缺的。透過預測給定軌跡的未來結果,軌跡評估會變得更有效,而這可以透過使用world model來捕捉環境動態並預測未來狀態來達成。因此,作者提出一個end-to-end駕駛框架WoTE,利用BEV(bird's-eye-view,鳥瞰視角)世界模型來預測未來的BEV狀態以進行軌跡評估。所提出的BEV world model相較於影像級(image-level)world model有更佳的延遲效率,且可以無縫地用現成的BEV空間交通模擬器來監督訓練。作者在NAVSIM基準以及基於CARLA模擬器的閉環(closed-loop)Bench2Drive基準上驗證此框架,取得state-of-the-art的表現。程式碼已在GitHub釋出。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392255_wote_fig1.png) 

_Figure 1: WoTE概念圖 - 以往end-to-end駕駛方法著重學習高品質軌跡(a);WoTE則進一步用BEV world model對候選軌跡進行線上評估(b)。_

![Figure]({{ site.baseurl }}/assets/images/1945392255_wote_fig2.png) 

_Figure 2: WoTE整體架構 - 分為Trajectory Prediction(BEV encoder編碼多視角影像產生軌跡候選)與Trajectory Evaluation(BEV world model預測未來狀態並評分)兩大部分。_

  * 要解決的問題:End-to-end自動駕駛系統雖已能整合感知、預測、規劃,但缺乏有效的線上軌跡評估機制來確保安全性。作者指出兩個關鍵技術挑戰:第一,需要良好的未來場景表徵——許多既有的自駕world model用擴散模型預測未來的影像級場景,運算耗時,不適合即時駕駛;第二,缺乏對未來狀態的監督訊號——world model需要針對多個候選軌跡分別想像出多個未來狀態,但真實世界資料集通常只包含一個實際發生的未來狀態,無法直接提供多重未來的監督。
  * Main method:提出WoTE框架,核心是一個BEV空間的world model,用來預測未來的BEV狀態以評估候選軌跡的優劣。此BEV world model相較於影像級world model有更高的延遲效率(不需生成完整的像素級影像),同時可以直接用現成的、BEV空間的交通模擬器(traffic simulator)作為監督訊號來源,解決了「多重未來缺乏監督」的問題。軌跡評估則是透過BEV特徵與軌跡嵌入(trajectory embedding)進行比較,使整個評估過程可微分,因此能與感知、規劃模組共同進行end-to-end最佳化。
  * 和以往方式的差異:相較於過去許多model-based軌跡評估方法依賴顯式軌跡表示與不可微分的度量指標(這限制了它們的end-to-end最佳化能力),以及影像級world model因擴散生成而運算耗時,WoTE選擇在BEV空間(而非像素空間)建模未來,兼顧了效率(不需生成完整影像)與可微分性(可直接嵌入end-to-end訓練)。相較於Hydra-MDP等model-free軌跡評估方法,WoTE透過引入BEV world model,展現了model-based方法的優勢。
  * 重要方法設計描述:整體流程可理解為——感知模組先將感測器輸入編碼成BEV特徵表示(鳥瞰視角下的場景語義/幾何資訊);規劃模組提出多個候選未來軌跡;BEV world model針對每個候選軌跡,在BEV空間中「想像」執行該軌跡後場景會如何演變(例如其他車輛、行人的位置變化),產生對應的未來BEV狀態預測,而非生成完整的像素級影片畫面;接著將這些預測出的未來BEV狀態與軌跡本身編碼成特徵向量,透過一個可微分的評分機制對每條候選軌跡進行評估與排序,選出最安全/最優的軌跡執行。訓練時,BEV world model的預測結果可直接用現成的BEV空間交通模擬器所產生的多重未來狀態作為監督訊號,解決真實資料集只有單一真實未來的限制。



### Result

  * 在NAVSIM基準以及基於CARLA模擬器的閉環Bench2Drive基準上,WoTE均取得state-of-the-art的表現。
  * 論文特別提到WoTE優於Hydra-MDP,原因在於Hydra-MDP採用model-free的軌跡評估方式,而WoTE採用model-based(BEV world model)的方式,凸顯了model-based方法的優勢。
  * WoTE的程式碼已在GitHub公開(liyingyanUCAS/WoTE),並已被後續工作(如WPT、MindDrive)引用作為強力baseline,顯示其結果具有一定的可信度與影響力。
  * 摘要與可得資訊未提供WoTE與同期其他BEV/世界模型方法(除Hydra-MDP外)的完整量化對比表,需要查證全文或原始論文的實驗表格以取得完整的比較數據。



### Limitation

  * 論文摘要中未包含明確的Limitation自陳段落,需要查證全文以確認作者自陳的限制。
  * 從方法設計推論的潛在弱項:BEV world model雖然比影像級world model更有效率,但BEV表示本身是一種降維後的抽象表徵,可能會遺失某些像素級細節(例如精細的紋理、光照變化)所隱含的資訊,這類資訊在某些邊緣案例(如判斷路面濕滑、光照造成的視覺遮蔽)中可能對安全評估有影響,但摘要未討論此權衡。此外,依賴「現成的BEV空間交通模擬器」作為監督來源,意味著模型的評估品質某種程度上受限於該模擬器本身的真實度與覆蓋範圍。



### Related work

  * WPT(World-to-Policy Transfer,arXiv:2511.20095)與MindDrive(arXiv:2512.04441)是引用WoTE作為強力baseline的後續工作,顯示WoTE在end-to-end自駕world model領域具有持續的影響力,值得追蹤這些後續研究如何進一步改進或挑戰WoTE的設計。
  * 與DriVerse(arXiv:2504.18576)同屬自駕world model領域但技術路線不同,適合比較「BEV空間軌跡評估」與「像素級軌跡條件生成」兩種不同應用取向的優劣。
  * 值得survey的程度:高。WoTE已被證實在此子領域具有指標性地位(已有多篇後續論文引用比較),適合作為理解「world model如何整合進end-to-end自駕決策框架」的重要參考點。



### Conclusion

  * 整體評價:值得參考。WoTE針對「如何在end-to-end自駕框架中做到高效且可微分的線上軌跡評估」這個具體工程問題,提出了一個平衡效率與有效性的解法(BEV空間而非像素空間建模),並在兩個不同性質的基準(NAVSIM開環、Bench2Drive閉環)上都取得SOTA表現,證明了方法的穩健性。已被ICCV 2025接受,並已成為後續工作的重要baseline,具有較高的參考價值。
  * 與其他重要文章的關係:WoTE與DriVerse同屬自駕world model領域,但分別代表「決策評估導向」與「場景生成導向」兩種不同的技術路線;WoTE也直接與Hydra-MDP(model-free方法)進行比較,證明了model-based(world model)方法在此任務上的優勢,並被WPT、MindDrive等後續研究延伸引用。
  * ROCm/AMD相關性:論文聚焦於BEV world model的架構設計與自駕基準測試,未提及使用的計算硬體平台或ROCm相關內容。從現有資訊看不出與ROCm/AMD有明確關聯;若考量BEV world model相對於影像級模型的「延遲效率優勢」,這類效率導向的架構設計理論上更容易在資源受限或非NVIDIA的硬體平台(如AMD GPU)上部署,但論文本身並未討論此點,需要另行查證或實測。