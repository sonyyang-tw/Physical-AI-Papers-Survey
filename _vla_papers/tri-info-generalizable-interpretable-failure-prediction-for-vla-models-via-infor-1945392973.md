---
layout: paper
title: "Tri-Info: Generalizable, Interpretable Failure Prediction for VLA Models via Information Theory"
section: vla
page_id: "1945392973"
permalink: /Physical-AI-Papers-Survey/vla/tri-info-generalizable-interpretable-failure-prediction-for-vla-models-via-infor-1945392973/
---

**Paper** : [Tri-Info: Generalizable, Interpretable Failure Prediction for VLA Models via Information Theory](https://arxiv.org/abs/2606.19998)  
**Source** : arXiv  
**arXiv ID** : 2606.19998

### Abstract

VLA 模型已被部署在多樣化任務中,但它們仍是黑盒,其與物理世界的互動一旦出錯可能造成不可逆的傷害,因此具普遍性且可解釋的失敗偵測至關重要。作者觀察到成功與失敗的 rollout 具有系統性不同的資訊理論特徵。基於此,本文將 VLA 控制形式化為一個閉環資訊管線(closed-loop information pipeline),並推導出三重資訊理論(Triple Information-theoretic, Tri-Info)訊號,分別捕捉動作是否保持多樣性、時間上是否一致、以及是否與狀態轉移耦合。在六個 VLA 模型與三個基準環境上,Tri-Info 在同分布(in-domain)情境下的表現與最強基線相當。此外,Tri-Info 能在不重新訓練的情況下跨架構、跨環境、跨越模擬到真實(sim-to-real)的落差進行遷移,在真實世界任務上達到 83% 準確率,而先前的偵測器在此情境下表現退化至接近隨機猜測的水準。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945392973_triinfo_fig1.png) 

_Figure 1: Information-theoretic metrics shift at failure onset — representative failure trajectories under three failure modes_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945392973_triinfo_fig3.png) 

_Figure 3: VLA control as a closed-loop information processing pipeline, the scaffold for the eight derived metrics_

  * 要解決的問題:如何建立一個不需針對特定模型/環境重新訓練、且結果可解釋的 VLA 失敗偵測機制,尤其是要能跨越模擬到真實世界的落差(sim-to-real gap)。
  * 主要方法:將 VLA 的控制過程形式化為一個閉環資訊管線,從資訊理論角度推導出三個訊號(Tri-Info):(1) 動作多樣性(actions 是否保持應有的變化性,而非退化為單調重複);(2) 時間一致性(動作序列在時間上是否連貫、不出現異常跳動);(3) 動作與狀態轉移的耦合程度(動作是否確實影響環境狀態,而非「空轉」)。
  * 與以往方式的差異:先前的失敗偵測方法多依賴針對特定模型/環境訓練的分類器,泛化能力有限,在 sim-to-real 遷移時容易失效(如摘要所述「先前偵測器崩潰至隨機猜測水準」)。Tri-Info 因為建立在資訊理論的通用統計量上,不依賴模型特定的訓練資料,因此具備跨架構、跨環境的遷移能力。
  * 重要方法設計描述:流程大致為:(1) 將 VLA 的控制迴路建模為資訊管線,定義動作序列、狀態序列之間的資訊流;(2) 分別計算三個資訊理論指標(多樣性、時間一致性、狀態耦合)作為 rollout 的特徵;(3) 用這三個訊號(而非模型內部的隱藏表徵)來判斷該 rollout 是成功還是失敗;(4) 在六個不同 VLA 模型、三個基準環境上驗證同分布偵測準確度;(5) 測試在不重新訓練的情況下,直接將這些訊號應用到新架構、新環境、以及真實機器人資料上,驗證其遷移能力。



### Result

  * 主要增強:在同分布情境下,Tri-Info 與最強基線的偵測表現相當(未必超越,但持平);其最大優勢在於跨域遷移能力——在不重新訓練的情況下跨架構、跨環境、跨 sim-to-real 落差時,Tri-Info 在真實世界任務上達到 83% 準確率,而先前方法則「崩潰至隨機猜測」,顯示出顯著優勢。
  * 是否公正:論文使用六個 VLA 模型、三個基準環境進行驗證,規模尚可,但「先前偵測器崩潰至隨機猜測」的具體對比方法名稱與數據需要查證全文以確認是否公正引用了正確的基線設置;是否有其他論文對相同基線提出不同(較不極端)的結論,需要查證其他論文的比較數據。



### Limitation

  * 論文摘要未明確列出限制章節,但可推測的弱項:(1) 「同分布下與最強基線持平」意味著 Tri-Info 的價值主要體現在跨域遷移,若應用場景本身就是同分布(不需要遷移),則其優勢不明顯;(2) 三個資訊理論訊號的計算是否需要對動作/狀態序列有足夠長度才能穩定估計(資訊理論量通常對樣本量敏感),論文未討論其在短序列或高頻控制下的穩定性,需要查證全文;(3) 83% 的真實世界準確率雖然優於崩潰的基線,但絕對數值仍有相當的錯誤率,對於安全關鍵應用是否足夠仍待評估。



### Related work

  * 與《Decoding Task Progress from VLA Representations》(arXiv:2608.13474)方向高度相關,兩者都關注 VLA 執行期失敗/異常偵測,但方法路徑不同(資訊理論訊號 vs 線性探針讀取任務進度),值得對照比較。
  * 暫無發現更新的直接後續研究。
  * 值得 survey 的程度高:失敗偵測與安全監控是 VLA 邁向實際部署的關鍵一環,此文提供了一個具跨域遷移能力的通用方法,值得深入了解其資訊理論訊號的具體計算方式。



### Conclusion

  * 綜合評價:本文針對 VLA 部署中「安全監控」這個實務痛點,提出一個具跨架構、跨環境、跨 sim-to-real 遷移能力的失敗偵測框架,尤其在真實世界表現大幅優於既有方法,是一篇具高度實務價值的工作,值得參考。
  * 與其他重要文章的關係:本文與 Decoding Task Progress(2608.13474)同屬 VLA 執行期監控/失敗偵測子領域,兩者互補;也隱含與六個受測 VLA 模型(可能包含 OpenVLA、π0、GR00T 等主流架構)的橫向比較意義。對 ROCm/AMD 而言,這類基於資訊理論訊號的偵測方法計算成本低廉(僅需對動作/狀態序列做統計量計算),若 AMD 考慮在自家硬體上為客戶提供 VLA 部署的安全監控功能,此類輕量、無需重新訓練的方法具有較高的落地可行性;但論文本身未提及任何硬體/框架議題,此為延伸判斷而非論文明確結論。