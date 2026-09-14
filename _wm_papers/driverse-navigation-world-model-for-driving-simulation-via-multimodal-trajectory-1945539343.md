---
layout: paper
title: "DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment"
section: wm
page_id: "1945539343"
permalink: /Physical-AI-Papers-Survey/wm/driverse-navigation-world-model-for-driving-simulation-via-multimodal-trajectory-1945539343/
---

**Paper** : [DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment](https://arxiv.org/abs/2504.18576)  
**Source** : arXiv / ACM Multimedia(ACM MM) 2025(已被接受)  
**arXiv ID** : 2504.18576

### Abstract

本文提出DriVerse,一個能從單張圖片與一段未來軌跡出發,模擬「導航驅動」駕駛場景的生成式模型。過去的自駕world model要不是直接把軌跡或離散控制訊號餵入生成流程(導致控制輸入與2D生成模型隱含特徵之間對齊不佳、輸出畫質低),就是使用粗略的文字指令或離散車輛控制訊號(精度不足以引導細粒度、軌跡特定的影片生成,不適合用來評估實際的自駕演算法)。DriVerse以兩種互補形式引入明確的軌跡引導:一是將軌跡token化為文字提示(使用預先定義的趨勢詞彙表,無縫整合進語言條件中);二是將3D軌跡轉換成2D空間運動先驗,以強化對駕駛場景中靜態內容的控制。為了處理動態物件,作者進一步引入一個輕量的運動對齊模組(motion alignment module),聚焦於動態像素的幀間一致性,顯著增強長序列中移動元素的時間連貫性。在幾乎不需額外訓練、也不需額外資料的情況下,DriVerse在nuScenes與Waymo兩個資料集上的未來影片生成任務中,表現優於專門化模型。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539343_driverse_fig1.png) 

_Figure 1: DriVerse navigation world model overview - 從單張圖片與導航軌跡生成高品質、與真實駕駛場景對齊的影片。_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539343_driverse_fig2.png) 

_Figure 2: DriVerse framework overview - 靜態對齊(Multimodal Trajectory Prompting)與動態對齊(Motion Alignment)兩大模組架構。_

  * 要解決的問題:過去的自駕導航world model在「控制訊號」與「生成畫面」之間的對齊做得不好——直接餵入原始軌跡/離散控制訊號會導致低保真度輸出,而用粗略文字指令或離散控制訊號又缺乏精確度,無法支撐細粒度的、軌跡特定的影片生成,因此不適合用來評估實際的自駕演算法表現。
  * Main method:提出「多模態軌跡提示」(Multimodal Trajectory Prompting, MTP)策略,同時利用語義與空間線索來引導影片生成:(1) 定義一套「趨勢詞彙表」(trend vocabulary),將軌跡的運動模式轉換成一系列離散token,加進傳統文字提示中做語義條件化;(2) 將3D軌跡轉換為2D空間運動先驗,強化對場景中靜態內容的控制。此外引入一個輕量的運動對齊模組,專注於動態像素的幀間一致性。為處理長序列生成中因車輛轉向角度變化帶來的偽影(artifact),還設計了動態視窗生成(Dynamic Window Generation, DWG)策略,在自迴歸(autoregressive)延伸生成過程中,依據朝向角變化自適應地在適當的中間幀更新條件參考幀。
  * 和以往方式的差異:相較於直接把軌跡數值或離散控制訊號硬塞進生成模型的方法,DriVerse透過「文字化的趨勢詞彙 + 2D空間運動先驗」這種雙重顯式軌跡引導,更貼合2D生成模型(如擴散模型)本身習慣的語言/空間條件輸入形式,因此對齊效果更好;同時運動對齊模組與動態視窗生成策略,專門處理其他方法容易忽略的「動態物件時間一致性」與「長序列自迴歸生成的轉向偽影」問題。
  * 重要方法設計描述:整體流程可想像為——輸入一張起始畫面與一段未來3D軌跡;軌跡先被轉換成兩種表徵形式同時輸入生成模型:一種是「趨勢詞彙」文字token(例如描述加速、轉彎等趨勢的離散詞),與原始文字提示拼接;另一種是把3D軌跡投影成2D影像空間中的運動先驗(例如未來路徑在畫面中的預期位置),用來約束靜態場景內容(道路、建築等)如何隨相機移動而變化。生成過程中,運動對齊模組專注在畫面中「會動的東西」(如其他車輛、行人)上,確保它們在連續幀之間的外觀與位置變化是連貫的,而不是像素級隨機跳動。當自迴歸生成延伸到較長的影片時,動態視窗生成策略會偵測車輛朝向角度的變化幅度,適時更新用來條件化下一段生成的參考幀,避免因長時間累積誤差導致畫面失真。



### Result

  * 在幾乎不需額外訓練、不需額外資料的情況下,DriVerse在nuScenes與Waymo兩個資料集的未來影片生成任務上,表現優於專門化(specialized)模型。
  * 摘要與可得資訊未提供具體的量化指標數字(如FID、FVD等影片生成品質指標的具體數值),需要查證全文以取得精確的比較數據。
  * 摘要未提及與其他自駕world model(如GeoDrive、WoTE等)的直接比較數據,需要查證其他論文的比較數據以確認DriVerse在該子領域中的相對排名。



### Limitation

  * 論文摘要中未包含明確的Limitation自陳段落,需要查證全文以確認作者自陳的限制。
  * 從方法設計推論的潛在弱項:DriVerse依賴「趨勢詞彙表」這種預先定義的離散化軌跡表示法,對於超出詞彙表覆蓋範圍的極端或罕見駕駛行為(如緊急避障的複雜軌跡)的表達能力可能有限;此外,該方法主要驗證於影片生成品質(視覺保真度與時間連貫性),而非直接驗證其作為下游自駕規劃/決策評估工具的有效性,是否能像WoTE一樣直接用於軌跡評估仍待查證。



### Related work

  * GeoDrive(arXiv:2505.22421,3D幾何資訊驅動的自駕world model,具精確動作控制)是同時期相關的自駕world model論文,適合與DriVerse比較幾何/軌跡條件化方式的異同。
  * 同類綜述資源(如GitHub上的Awesome-World-Model、World-Models-Autonomous-Driving-Survey)持續在收錄此類論文,顯示該子領域仍在快速演進中。
  * 值得survey的程度:中高。DriVerse代表了自駕world model中「顯式軌跡條件化」這一設計流派的代表作,值得與WoTE(BEV空間軌跡評估)、GeoDrive(3D幾何條件化)等不同技術路線的論文一併比較,以理解該領域目前的技術分歧與收斂點。



### Conclusion

  * 整體評價:值得參考,尤其對於關注「如何讓生成式world model精確回應軌跡/控制輸入」這個問題的讀者。其「文字化趨勢詞彙+2D空間運動先驗」的雙重顯式軌跡引導設計思路具有一定的工程創新性,且已被ACM MM 2025正式接受,具有一定的同行評審把關。
  * 與其他重要文章的關係:DriVerse與WoTE(arXiv:2504.01941)同屬自駕world model領域,但技術路線不同——DriVerse著重於「生成高保真的未來駕駛場景影片」以供訓練/評估使用,而WoTE著重於「用BEV空間world model直接做線上軌跡評估」以支撐end-to-end駕駛決策,兩者可視為「生成式模擬」與「決策評估」兩種不同應用取向的代表。與GeoDrive等同期論文則可比較不同的軌跡/幾何條件化技術細節。
  * ROCm/AMD相關性:論文聚焦於生成模型的軌跡條件化設計與影片生成品質評測,未提及使用的計算硬體平台或ROCm相關內容。從現有資訊看不出與ROCm/AMD有明確關聯。