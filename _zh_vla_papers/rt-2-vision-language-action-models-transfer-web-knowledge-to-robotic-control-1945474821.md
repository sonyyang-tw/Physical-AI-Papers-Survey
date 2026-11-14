---
layout: paper
title: "RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control"
section: vla
page_id: "1945474821"
permalink: /zh/vla/rt-2-vision-language-action-models-transfer-web-knowledge-to-robotic-control-1945474821/
---

**Paper** : [RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control](https://arxiv.org/abs/2307.15818)  
**Source** : arXiv / Google DeepMind  
**arXiv ID** : 2307.15818

### Abstract

本文研究如何將在網路規模資料上訓練的視覺-語言模型(VLM)直接整合進端到端的機器人控制中,以提升泛化能力並激發新興的語意推理能力。作者提出將 VLM 同時在機器人軌跡資料與網路規模的視覺-語言任務(如視覺問答)上共同微調(co-fine-tune),並將機器人動作表示為文字 token,以與自然語言 token 相同的方式納入訓練資料。此類模型被稱為視覺-語言-動作(VLA)模型。本文提出的 RT-2 建構於先前的 RT-1 模型之上,使用兩個基礎 VLM(PaLI-X 與 PaLM-E)。經過六千次評估試驗的廣泛評測,RT-2 展現出優異的機器人策略表現,並從網路規模訓練中獲得一系列新興能力,包括對新物件的顯著提升泛化能力、理解訓練資料中未出現的指令的能力,以及對使用者指令的初步推理能力(例如判斷該用哪個物件充當臨時鐵鎚,或該給疲憊的人哪種飲料)。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474821_rt2_fig1.png) 

_Figure 1: RT-2 overview — robot actions represented as text tokens, co-trained with Internet-scale vision-language data_

![Figure]({{ site.baseurl }}/assets/images/1945474821_rt2_fig2.png) 

_Figure 2: RT-2 generalizes to real-world situations requiring reasoning, symbol understanding, and human recognition_

  * 要解決的問題:如何讓機器人策略同時具備「端到端學習觀測到動作的映射」以及「享受網路規模語言/視覺-語言預訓練帶來的泛化與推理能力」這兩個優點,而非兩者擇一。
  * 主要方法:共同微調(co-fine-tuning)——把預訓練好的 VLM(PaLI-X、PaLM-E)同時在機器人示範軌跡資料與原本的網路規模視覺-語言任務(如 VQA)上進行微調,而不是只用機器人資料微調(這樣會遺忘原有的網路知識)。動作被離散化並表示為文字 token,與自然語言 token 並列輸出,讓模型能用生成文字的方式「說出」動作。
  * 與以往方式的差異:先前的機器人學習方法(包括作者自己的 RT-1)主要僅在機器人示範資料上訓練,無法利用網路規模的語意知識;RT-2 是首次將 VLM 直接轉化為端到端機器人控制策略、且透過共同微調保留網路知識的方法,並因此獲得先前方法所沒有的「新興能力」(如對未見物件的推理)。
  * 重要方法設計描述:架構上,RT-2 以 PaLI-X(5B / 55B 參數)或 PaLM-E(12B 參數)作為基礎 VLM;動作(六自由度末端執行器位移、旋轉、夾爪開合等)被離散化為有限個 bin,每個 bin 對應一個文字 token;模型輸入影像與語言指令,輸出的文字 token 序列中一部分即代表動作;訓練資料混合了 RT-1 收集的機器人示範資料(13 台機器人、17 個月、辦公室廚房環境)與原始網路規模視覺-語言資料;模型也可結合思維鏈(chain-of-thought)推理,先產生中間推理步驟再輸出動作。



### Result

  * 主要增強:RT-2 保留了在原始訓練任務上的表現,並顯著提升了在「未見過場景」上的表現,從 RT-1 的 32% 大幅提升至 62%,證明大規模預訓練帶來的顯著益處。RT-2 也展現出思維鏈推理、對新物件泛化、理解未見指令等新興能力。
  * 是否公正:評測規模達 6000 次試驗,屬於較嚴謹的機器人評測規模;但作為 Google DeepMind 自家發表的論文,其比較基準(RT-1)也是同團隊先前工作,是否有第三方獨立復現的評測結果需要查證其他論文的比較數據。OpenVLA(2406.09246)論文中提及 RT-2-X(55B)作為比較基準,顯示後續研究確實採用 RT-2 系列作為公認基準,一定程度佐證其結果的參考價值。



### Limitation

  * 論文自陳/可推測的限制:(1) 使用超大規模 VLM(55B 參數的 PaLI-X)作為基礎,對推論延遲與部署成本有較高要求,不利於即時控制場景;(2) 動作離散化為文字 token 的表示方式,可能在需要高精度連續控制的任務上有表達力限制;(3) 訓練資料的機器人示範仍侷限於特定環境(辦公室廚房),對其他更複雜、更精細操作任務的泛化能力需要查證全文。



### Related work

  * 後續 OpenVLA(arXiv:2406.09246,2024)直接以 RT-2-X(55B)作為比較基準,並宣稱以 7B 參數(7 倍更小)在 29 個任務上超越 RT-2-X 達 16.5% 絕對成功率,顯示 RT-2 系列已成為 VLA 領域公認的重要基準線。
  * π0(2410.24164)、GR00T N1(2503.14734)等後續 VLA 模型也延續了「VLM + 機器人動作輸出」的核心思路,但改用 flow matching / diffusion 而非文字 token 離散化來輸出動作,顯示這是 RT-2 之後的技術演進方向。
  * 值得 survey 的程度極高:RT-2 是 VLA 這個研究方向的奠基性(seminal)論文之一,幾乎所有後續 VLA 論文都會將其列為背景介紹或比較對象。



### Conclusion

  * 綜合評價:RT-2 是 VLA 領域的開創性工作,首次證明將網路規模 VLM 直接轉化為機器人控制策略是可行且能帶來顯著泛化增益的方法,對整個領域影響深遠,是必讀的基礎論文。
  * 與其他重要文章的關係:RT-2 被後續 OpenVLA、π0、GR00T N1 等重要工作視為關鍵背景與比較基準,後續研究普遍朝「用連續動作生成方法(diffusion/flow matching)取代文字 token 離散化」的方向演進,顯示 RT-2 的文字 token 動作表示法雖具開創性但已被更精細的連續控制方法超越。對 ROCm/AMD 而言,RT-2 使用的 55B 參數超大型 VLM 對推論硬體的記憶體與算力有相當要求,若 AMD 欲支援此類大型 VLA 模型的推論或微調(尤其是共同微調需同時處理機器人資料與網路規模資料的混合訓練),值得關注大模型分散式訓練/推論在 ROCm 上的成熟度,但論文本身並未提及所使用的具體訓練硬體,此為推論而非論文明文提及。