---
layout: paper
title: "Decoding Task Progress from VLA Representations"
section: vla
page_id: "1945539940"
permalink: /Physical-AI-Papers-Survey/vla/decoding-task-progress-from-vla-representations-1945539940/
---

**Paper** : [Decoding Task Progress from VLA Representations](https://arxiv.org/abs/2608.13474)  
**Source** : arXiv  
**arXiv ID** : 2608.13474

### Abstract

VLA 模型正快速朝向作為通用操作策略部署,但目前缺乏理解其內部表徵、或在執行期監控其狀態的基本工具。本文借鑑機制可解釋性的概念,探測 π0.5 模型的殘差流(residual stream),發現「任務進度」(即軌跡中剩餘時間的正規化值)可從激活中線性讀出。作者發現這個訊號在 PaliGemma 骨幹網路尚未經過任何機器人專屬資料訓練前就已存在。單一線性探針能泛化到未見過的任務,並在以多提示資料訓練時能隨語言反事實(counterfactual)而變化,但並不能有效操控(steer)策略行為。這些特性使得該訊號可直接用於監控已部署的 VLA。作者將此探針作為一種無需標籤(label-free)的分布外(OOD)偵測器,能偵測任務進度停滯的情況,並發現其表現可與最先進方法相媲美。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539940_taskprogress_fig1.png) 

_Figure 1: Task progress is linearly readable from pi0.5 internal activations via a linear probe on residual-stream activations_

![Figure](/Physical-AI-Papers-Survey/assets/images/1945539940_taskprogress_fig2.png) 

_Figure 2: Decodability of the progress feature across layers (SigLIP, PaliGemma Gemma backbone, action expert) and probe performance vs. capacity_

  * 要解決的問題:已部署的 VLA 缺乏對其內部狀態的監控工具,例如無法得知模型是否「卡住」、任務是否正在正常推進,這對安全部署是一大缺口。
  * 主要方法:借用機制可解釋性中的線性探針(linear probe)方法,在 π0.5 模型的殘差流激活上訓練一個簡單的線性分類器/回歸器,用以預測「任務進度」(軌跡中剩餘時間的正規化比例)。
  * 與以往方式的差異:先前對 VLA 執行期監控的方法多依賴額外的標籤資料或專門訓練的異常偵測模型;本文則證明「任務進度」這種語意量早已隱含在模型的既有激活中(甚至在 PaliGemma 預訓練骨幹、尚未看過任何機器人資料時就存在),只需一個簡單線性探針即可讀出,無需額外標籤或重新訓練整個模型。
  * 重要方法設計描述:流程包括:(1) 對 π0.5 模型在執行不同操作任務時收集殘差流激活;(2) 以「正規化剩餘時間」作為回歸目標,訓練線性探針;(3) 驗證此探針在 PaliGemma 預訓練骨幹(未經機器人資料微調)上是否已存在該訊號;(4) 測試探針在多提示(multi-prompt)資料下,對語言反事實的敏感度;(5) 嘗試用探針方向去操控(steer)策略行為,驗證其是否具因果操控力;(6) 將探針包裝為一個無需標籤的 OOD/停滯偵測器,並與現有最先進(SOTA)偵測方法比較。



### Result

  * 主要發現:任務進度訊號可線性讀出,且泛化到未見任務;此訊號在預訓練骨幹階段就已存在,顯示這類語意量並非機器人資料微調才產生的;探針對語言反事實敏感(代表確實反映任務語意),但**無法** 用於有效操控策略行為(steering 失敗),顯示「可讀出的訊號」不等於「可操控的訊號」,兩者是分離的性質。作為 OOD 偵測器,此線性探針的表現可與最先進方法相媲美。
  * 是否公正:論文本身將自己的簡易線性探針方法與「最先進的 OOD 偵測方法」比較並宣稱具競爭力,但摘要未列出具體數值或所比較的基準方法名稱,是否公正、是否有其他論文提出不同結論,需要查證其他論文的比較數據以確認。



### Limitation

  * 論文自陳的限制:探針雖然可以讀出任務進度且可用於偵測,但**不能用於操控策略行為**(steering 無效),這代表此訊號雖然「可讀」但並非策略決策的因果驅動因子,應用範圍侷限在監控/偵測,而非主動干預。
  * 從結果看的弱項:方法僅在 π0.5 一個模型架構上驗證,是否能推廣到其他 VLA 架構(如 OpenVLA、GR00T、SmolVLA)未知,需要查證全文或後續研究。此外,「任務進度停滯偵測」作為 OOD 偵測手段,對於非「停滯」型態的失敗模式(如任務執行方向錯誤但仍在推進)可能無法偵測,論文未討論此類失效模式的涵蓋範圍。



### Related work

  * 這篇論文與 Tri-Info(arXiv:2606.19998,同樣關注 VLA 失敗偵測)方向高度相關,兩者都嘗試從模型內部訊號(而非額外訓練的偵測器)偵測執行期異常,值得對照比較兩者在偵測準確度與泛化能力上的差異。
  * 暫無發現更新的直接後續研究。
  * 值得 survey 的程度高:此文提供了一個輕量、可解釋、且不需額外標籤的 VLA 監控方法,對於希望在生產環境中部署 VLA 的工程團隊(包含考慮在 AMD 硬體上部署推論的團隊)有直接的實務參考價值。



### Conclusion

  * 綜合評價:本文提出簡單但具洞察力的發現——任務進度訊號早已隱含在預訓練 VLM 骨幹中,並展示其在安全監控上的實用價值,是一篇小巧但有實務意義的工作,值得參考,尤其對關注部署可靠性、runtime monitoring 的工程師有直接幫助。
  * 與其他重要文章的關係:本文與 Tri-Info(2606.19998)同屬「VLA 執行期失敗偵測/監控」的子領域,兩者互補(線性探針 vs 資訊理論訊號);也與 π0/π0.5(Physical Intelligence 的旗艦模型)直接相關,因為本文分析對象即為 π0.5。對 ROCm/AMD 而言,若 AMD 團隊正在探索在自家硬體上部署 VLA 推論服務,這類「輕量線性探針監控」方法因計算成本極低(只需額外一個線性層的前向計算),是相對容易在任何推論框架(包含 ROCm 上的 PyTorch/vLLM 等)上實作的監控機制,可視為低成本、高投報的 runtime 可觀測性補強方向;但論文本身未討論任何硬體或框架層面的議題,此推論屬於延伸判斷而非論文明確結論。