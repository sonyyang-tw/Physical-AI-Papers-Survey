---
layout: paper
title: "Do World Action Models Generalize Better than VLAs? A Robustness Study"
section: vla
page_id: "1945392664"
permalink: /zh/vla/do-world-action-models-generalize-better-than-vlas-a-robustness-study-1945392664/
---

**Paper** : [Do World Action Models Generalize Better than VLAs? A Robustness Study](https://arxiv.org/abs/2603.22078)  
**Source** : arXiv (cs.RO)  
**arXiv ID** : 2603.22078

### Abstract

本論文對「World Action Models (WAMs) 是否比傳統 VLA 具有更好泛化能力」這個被廣泛假設的說法進行了實證檢驗。作者指出，機器人動作規劃需要不僅理解環境當前狀態，還要預測環境如何回應動作而演化；VLA 透過大規模視覺語言模型加上動作專家（action expert）取得了不錯的成功，但其表現受限於訓練資料的範圍，對未見過場景的泛化能力有限，且對各種情境擾動較脆弱。近期 world model 被重新提出作為替代方案——即所謂 WAM，這類模型建立在以大量影片資料訓練、預測未來狀態的 world model 之上，經過少量調整即可將其潛在表示解碼為機器人動作；有人主張其顯式的動態預測能力，結合從網路規模影片預訓練獲得的時空先驗，使 WAM 能比 VLA 泛化得更好。本文在 LIBERO-Plus 與 RoboTwin 2.0-Plus 兩個 benchmark 上，於各種視覺與語言擾動下，對比多個代表性的 SOTA VLA 策略與近期發布的 WAM。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392664_wamvla_robust_fig1.png) 

_Figure 1: RoboTwin 2.0-Plus 任務上的擾動範例。（各種噪聲 N、光照 L 等擾動代號定義詳見論文附錄 A）_

![Figure]({{ site.baseurl }}/assets/images/1945392664_wamvla_robust_fig3.png) 

_Figure 3: Cosmos-policy 所預測的未來影像示例。展示 LIBERO-Plus 中三種擾動類型（噪聲、光照、背景變化）下的真實影像（GT）與 Cosmos-policy 預測影像（Pred.）對比，說明其世界模型的動態預測能力。_

  * **要解決的問題** ：驗證一個業界流行但尚未被嚴謹實證檢驗的假說——WAM 是否真的比 VLA 更能泛化、更能抵抗視覺/語言擾動。
  * **主要方法** ：這是一篇實證比較研究（robustness study），而非新模型論文：
    * 選取多個代表性的 SOTA VLA 策略（如 π_0.5）與近期發布的 WAM（如 LingBot-VA、Cosmos-Policy）。
    * 在 LIBERO-Plus 與 RoboTwin 2.0-Plus 兩個 benchmark 上進行評測，這兩者是對原始 LIBERO / RoboTwin 2.0 benchmark 加入「各種視覺與語言擾動」的擴充版本，用以測試模型在分布外（OOD）情境下的穩健性。
    * 系統性比較不同模型族在擾動下的成功率變化，藉此檢驗 WAM 相對於 VLA 的泛化優勢是否成立。
  * **與以往方式的差異** ：以往關於 WAM 優於 VLA 的說法多是理論推測（基於 WAM 具有顯式動態預測與網路影片先驗），本文首次以系統性的擾動 benchmark 實證檢驗此假說，而非僅比較標準（無擾動）任務成功率。



### Result

  * WAM 展現出較強的穩健性：LingBot-VA 在 RoboTwin 2.0-Plus 上達到 74.2% 成功率，Cosmos-Policy 在 LIBERO-Plus 上達到 82.2% 成功率。
  * VLA（如 π_0.5）在部分任務上也能達到相近的穩健性，但通常需要更大量、更多樣的機器人資料集與多樣化的學習目標才能做到。
  * 是否公正：此為獨立第三方比較研究（非模型提出者自行宣稱），相對於單一模型論文的自我報告更具客觀性，是目前清單中少數專門處理「其他論文結果是否相符」問題的文章。但仍需注意：作者選取哪些 VLA/WAM 作為比較對象、benchmark 設計本身是否對某一類方法有利，可能影響結論的普適性；建議查證全文中具體的擾動類型清單與各模型在每類擾動下的細分數據，以及是否有評測程式碼公開（作者提及 RoboTwin2.0-Plus 評測程式碼已公開）供他人覆現。



### Limitation

  * 論文自陳的限制：摘要強調「VLA 若要達到相近穩健性，通常需要大量且多樣的機器人訓練資料與多樣化學習目標」，暗示這是 VLA 陣營的限制，而非 WAM 本身直接優越；但這也可能反映 WAM 在低資料場景下的相對優勢僅是條件性的（即取決於 VLA 是否有足夠資料）。
  * 從結果來看：即使是表現最好的 WAM（Cosmos-Policy 82.2%、LingBot-VA 74.2%），成功率仍非接近 100%，顯示即使 WAM 相對穩健，在強擾動下仍有顯著失敗率；具體是哪些擾動類型（視覺 vs. 語言）造成較大跌幅，需要查證全文。



### Related work

  * 此論文與清單中「World Action Models: The Next Frontier in Embodied AI」（2605.12090）主題高度互補：前者是分類/命名綜述，後者是實證檢驗；建議搭配閱讀。
  * 暫無發現此篇之後更新的直接後續研究（在本次搜尋範圍內）；但其開放評測程式碼（RoboTwin2.0-Plus）可能會被後續論文引用作為標準比較基準，值得持續追蹤。
  * 值得 survey 的程度：高。作為少數對「WAM 優於 VLA」這一流行假說進行實證檢驗的論文，對於想要客觀評估 WAM 範式價值的研究者而言參考價值很高。



### Conclusion

  * 綜合評價：非常值得參考。這是一篇提供實證證據、而非僅是理論宣稱的比較研究，有助於避免對 WAM 範式的過度樂觀解讀，是評估「是否該投入 WAM 方向」的重要參考依據。
  * 與其他論文關係：此文直接檢驗了「World Action Models: The Next Frontier in Embodied AI」（2605.12090）等綜述文章中提及的核心假說（WAM 具動態預測與影片先驗優勢），並比較了具體模型如 π_0.5（VLA）、LingBot-VA、Cosmos-Policy（WAM），可視為對該領域樂觀敘事的一種平衡性驗證。
  * ROCm/AMD 關聯：從摘要內容看不出與 ROCm/AMD 有明確關聯，論文未提及訓練/推論所用硬體平台；但由於文中提及的模型（尤其 Cosmos-Policy，可能與 NVIDIA Cosmos 平台相關）多半在 NVIDIA 生態系下開發與評測，這也間接指出目前 WAM 領域的評測與部署工具鏈以 NVIDIA 為主流，AMD/ROCm 若要切入此領域，可能需要補強對應的影片擴散模型與機器人策略評測工具鏈的相容性支援（此為推論觀察，非論文明確結論）。