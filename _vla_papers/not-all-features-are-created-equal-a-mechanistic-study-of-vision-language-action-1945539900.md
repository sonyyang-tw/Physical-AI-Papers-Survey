---
layout: paper
title: "Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models"
section: vla
page_id: "1945539900"
permalink: /vla/not-all-features-are-created-equal-a-mechanistic-study-of-vision-language-action-1945539900/
---

**Paper** : [Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models](https://arxiv.org/abs/2603.19233)  
**Source** : arXiv / 已被 ICLR Multimodal Intelligence Workshop 接受  
**arXiv ID** : 2603.19233

### Abstract

VLA 模型結合感知、語言與運動控制於單一架構,但其如何將多模態輸入轉化為動作仍不清楚。本文對六個參數量從 80M 到 7B 的模型,在四個基準上總計超過 394,000 個 rollout 情節上,套用激活注入(activation injection)、稀疏自編碼器(SAE)與線性探針(linear probe)進行分析。結果顯示視覺路徑在所有架構中都主導動作生成:將基準激活注入無提示情節即可恢復近乎相同的行為,而跨任務注入則會使機器人趨向來源任務的位置(X-VLA 中 99.8% 的情節與來源軌跡對齊),顯示出與場景座標綁定、而非抽象任務表徵的空間性動作程式。語言的敏感度取決於任務結構而非模型設計:當視覺情境已能唯一決定任務時,語言會被忽略;當多個目標共享同一場景時,語言變得關鍵(X-VLA 的 libero_goal 任務:錯誤提示下成功率從 94% 降至 10%;而 libero_object 任務則不受提示正確與否影響,維持在 60-100%)。在三個多路徑架構(π0.5、SmolVLA、GR00T)中,專家(expert)路徑編碼動作程式,VLM 路徑編碼目標語意(專家注入造成的行為位移是 VLM 注入的兩倍),子空間注入實驗證實兩者佔據可分離的激活子空間。逐 token 的 SAE 處理對大多數架構的動作保真度至關重要,但均值池化(mean-pooling)在 X-VLA 上反而提升保真度。對比式識別法(contrastive identification)找出 82 個以上的操作概念,因果消融實驗顯示零效應比率介於 28%-92% 之間,與表徵寬度無關。作者釋出 Action Atlas 互動平台供探索六個模型的表徵。

### Method

![Figure](/assets/images/1945539900_notallfeatures_fig1.png) 

_Figure 1: Three core findings on pi0.5 — activation injection recovers baseline behavior, cross-task override, and feature attribution_

![Figure](/assets/images/1945539900_notallfeatures_fig2.png) 

_Figure 2: Methodology overview — activation recording from VLA backbone/action expert and counterfactual replay_

  * 要解決的問題:VLA 模型的視覺、語言、動作三種模態訊號在內部如何分工、如何被編碼,以及這種分工是否具有跨架構的普遍性。
  * 主要方法:結合三種機制可解釋性工具——(1) 激活注入(把一個情節的激活替換到另一情節中觀察行為變化,驗證因果性);(2) 稀疏自編碼器(SAE),用於分解並辨識可解釋的操作概念特徵;(3) 線性探針,用於檢驗特定語意/任務資訊是否可從激活線性讀出。三者互相佐證,並在六個橫跨 80M 到 7B 參數量的 VLA 模型、四個基準、近 40 萬個 rollout 上進行大規模驗證。
  * 與以往方式的差異:過去對 VLA 內部機制的研究通常侷限於單一模型或單一分析工具,樣本規模也遠小於本文(六模型 x 四基準 x 近 40 萬 rollout),使得本文結論具有較強的跨架構普遍性。此外,作者特別區分「視覺路徑主導」與「語言路徑依任務結構而定」兩種不同機制,這種細緻的條件式分析是先前研究較少涉及的。
  * 重要方法設計描述:核心流程包括:(1) 對「無提示(null-prompt)」情節注入其他情節的基準激活,觀察行為是否被視覺訊號主導而恢復;(2) 跨任務注入實驗,把源任務的激活注入到目標任務情節,測量機器人軌跡是否偏向源任務位置(以此驗證「空間綁定的動作程式」假說);(3) 對多路徑架構(如 π0.5、SmolVLA、GR00T)分別注入其 VLM 路徑與專家(expert)路徑的激活,比較兩者造成的行為位移大小,並用子空間注入(subspace injection)確認兩者是否佔據不同、可分離的激活子空間;(4) 用逐 token 與均值池化兩種 SAE 前處理方式比較對動作保真度的影響;(5) 用對比式方法在 SAE 特徵中識別操作概念,並以因果消融測試每個特徵的重要性(零效應比率)。



### Result

  * 主要發現/增強:視覺路徑在所有架構中對動作生成佔主導地位;語言敏感度是任務結構(場景是否存在歧義)決定,而非模型設計決定;三個多路徑架構中專家路徑與 VLM 路徑功能分離且佔據可分離子空間;SAE 逐 token 處理通常優於均值池化(X-VLA 例外);識別出 82+ 個操作概念,因果消融顯示不同特徵的敏感度差異極大(28%-92% 零效應率),且與表徵維度寬度無關。
  * 是否公正:本文樣本規模(六模型、四基準、近 40 萬 rollout)相對前述兩篇 VLA 可解釋性論文更大,結論的普遍性理論上更強;但這是一篇 workshop 論文(ICLR Multimodal Intelligence Workshop),並非正式會議主會場論文,審查嚴謹度可能不及 ICML 正式論文(如 Embodied Interpretability)。此外,本文與 SAE for VLA(2603.19183)同日提交,兩者在方法與結論上部分重疊(皆用 SAE 分析 VLA),但具體數據是否互相印證,需要查證其他論文的比較數據。



### Limitation

  * 論文摘要未明確列出限制章節,但可推測的弱項:(1) X-VLA 出現與其他架構不同的例外(均值池化優於逐 token),顯示結論可能不完全跨架構通用,需要針對每個新架構重新驗證;(2) 因果消融的零效應率範圍極廣(28%-92%),顯示特徵重要性高度不均勻,如何系統性篩選出「關鍵特徵」仍待解決;(3) 84 萬 rollout 規模龐大,重現該實驗需要相當的計算資源,可能限制其他團隊的獨立驗證能力。



### Related work

  * 與同期論文《Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models》(2603.19183)高度相關,兩者都使用 SAE 分析 VLA,值得對照兩篇的具體發現是否一致。
  * 暫無發現更明確的更新後續研究。
  * 值得 survey 的程度高:本文提供了目前規模最大的跨架構 VLA 機制分析,是理解「VLA 內部視覺/語言/動作分工」的重要參考基準。



### Conclusion

  * 綜合評價:本文以大規模、跨架構的方式系統性地分析 VLA 內部機制,對於理解「VLA 到底依賴視覺還是語言」這類實務問題(例如評估模型的分布外穩健性)極具參考價值,值得深入閱讀。
  * 與其他重要文章的關係:本文延伸並與 SAE-for-VLA(2603.19183)、Embodied Interpretability(2605.00321)構成 2026 年 VLA 機制可解釋性研究的核心三角,同時涉及 π0.5、SmolVLA、GR00T、X-VLA 等多個目前主流 VLA 架構,對於評估「哪個 VLA 架構的內部機制更透明、更適合在特定硬體上部署與除錯」有參考意義。就 ROCm/AMD 而言,論文本身未提及使用的訓練/推論框架與硬體,因此看不出明確的直接關聯;但若 AMD 未來要支援大規模 VLA 可解釋性研究(如同時對六個模型、四個基準做近 40 萬次 rollout 的激活收集與注入實驗),這類工作負載對推論吞吐與批次激活擷取的效能要求值得留意,惟論文未觸及此點,需另行評估。