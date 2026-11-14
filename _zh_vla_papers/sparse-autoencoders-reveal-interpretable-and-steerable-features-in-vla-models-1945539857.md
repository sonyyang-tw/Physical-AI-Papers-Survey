---
layout: paper
title: "Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models"
section: vla
page_id: "1945539857"
permalink: /zh/vla/sparse-autoencoders-reveal-interpretable-and-steerable-features-in-vla-models-1945539857/
---

**Paper** : [Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models](https://arxiv.org/abs/2603.19183)  
**Source** : arXiv (24 頁, 11 張圖)  
**arXiv ID** : 2603.19183

### Abstract

VLA 模型雖已成為通用機械手臂操作的主流方法,但少有研究以機制可解釋性(mechanistic interpretability)的角度探討其在物件、場景、指令變化下為何能泛化。本文在 VLA 的隱藏層激活上訓練稀疏自編碼器(Sparse Autoencoder, SAE),學習出激活的稀疏字典,揭露出許多對應到模型表徵空間中可解釋方向的特徵。作者辨識出對應動作基元(motion primitives)與語意概念的 SAE 特徵,其中部分特徵具跨情節的通用性且可被因果式操控(steerable)。作者提出一個指標用以將特徵分類為「通用可遷移的基元」或「情節專屬的記憶」,為理解 VLA 泛化能力提供線索。作者在 LIBERO 模擬基準與真實世界 DROID 硬體上進行操控(steering)實驗驗證這些發現。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539857_saevla_fig1.png) 

_Figure 1: SAE 訓練與特徵解析流程總覽_

![Figure]({{ site.baseurl }}/assets/images/1945539857_saevla_fig2.png) 

_Figure 2: 特徵操控(steering)實驗架構_

  * 要解決的問題:VLA 模型內部到底學到了什麼可重複使用的表徵,使其能夠將感知、語言與動作跨任務、跨場景連結起來?目前缺乏機制層面的理解。
  * 主要方法:在 VLA 的隱藏層激活上訓練 Sparse Autoencoder,將高維度、疊加(superposed)的激活分解為稀疏、可能對應單一語意/動作概念的特徵字典項(dictionary features)。
  * 與以往方式的差異:先前對 VLA 的理解多停留在端到端的行為評估(成功率等黑盒指標),缺乏對內部表徵的細粒度分解;本文借用近年在 LLM 可解釋性領域流行的 SAE 技術,將其應用到機器人 VLA 領域,並额外提出通用性 vs 情節記憶的分類指標,以及透過「操控(steering)」實驗(放大/消融特定特徵)來驗證因果性,而非僅做相關性分析。
  * 重要方法設計描述:流程包括:(1) 收集 VLA 模型在大量 rollout episode 上的隱藏層激活;(2) 訓練 SAE 學習稀疏字典,將激活分解為多個可解釋的特徵方向;(3) 對每個特徵進行語意標註,辨識其是否對應動作基元(如「抓取」、「移動到左側」)或語意概念(如物件類別);(4) 提出通用性指標,量化特徵是否在多個不同 episode 中穩定出現(通用可遷移基元)或僅出現在特定情節(情節專屬記憶);(5) 進行操控實驗:放大(amplify)通用/語意特徵,觀察是否誘發符合其語意的行為;消融(ablate)特徵,觀察是否破壞模型表現;(6) 在 LIBERO 模擬與 DROID 真實機器人硬體上重複驗證。



### Result

  * 主要增強/發現:放大通用且具語意的特徵能誘發與其語意一致的行為,消融這些特徵則會破壞模型表現,證明這些 SAE 特徵具有因果作用而非僅是相關性產物。作者也展示可利用 steering 來控制模型執行原本無法直接以語言提示(unpromptable)的行為方向。這些結果為「VLA 學到可重複使用的內部特徵、連結感知/語言/動作」提供了機制層面的證據。
  * 是否公正:實驗同時涵蓋模擬(LIBERO)與真實硬體(DROID),具一定的外部效度;但摘要未提供與其他同類 SAE-for-VLA 研究(如 arXiv:2603.19233)之間的直接量化比較,兩篇論文可能有部分重疊或互補的發現,需要查證其他論文的比較數據以確認結論一致性。



### Limitation

  * 論文摘要未明確列出限制章節內容,但可推測的弱項包括:(1) 並非所有 SAE 特徵都能被清楚語意標註,可能存在大量無法解釋的「死特徵」或多義特徵;(2) 操控實驗的效果可能因任務、模型架構而異,通用性有待更廣泛驗證;(3) SAE 訓練本身需要額外計算資源與超參數調整(如稀疏度、字典大小),其穩定性與可重現性需要查證全文。



### Related work

  * 同一時期(2026年3月19日)有另一篇密切相關的論文《Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models》(arXiv:2603.19233),同樣使用 SAE 等機制可解釋性工具分析 VLA,兩者可能出自不同團隊但方向高度重疊,值得對照閱讀。
  * 值得 survey 的程度高:此文代表了 VLA 可解釋性領域将 LLM 可解釋性技術(SAE)遷移應用的重要嘗試,是理解 VLA 內部表徵的基礎性工作之一。



### Conclusion

  * 綜合評價:本文首次系統性地將 SAE 應用於 VLA 模型並透過真實硬體驗證因果操控效果,方法紮實、驗證充分,值得參考,尤其對想深入理解 VLA「黑盒」內部運作的研究者有高度價值。
  * 與其他重要文章的關係:本文與《Not All Features Are Created Equal》(2603.19233)、《Embodied Interpretability》(2605.00321)同屬 2026 年興起的 VLA 機制可解釋性研究群,彼此互補(SAE 特徵分解 vs 因果介入歸因)。對 ROCm/AMD 而言,SAE 訓練與大規模激活收集屬於計算密集型的離線分析工作,論文未提及使用何種硬體/框架,因此看不出與 ROCm 生態系統有明確直接關聯;若 AMD 欲切入此類可解釋性工具鏈,值得關注的空白是「SAE 訓練與大批次介入實驗在 ROCm/PyTorch 上的效能與生態系支援」,但這點論文本身並未觸及。