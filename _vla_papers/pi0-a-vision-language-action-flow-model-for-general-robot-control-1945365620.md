---
layout: paper
title: "Pi0: A Vision-Language-Action Flow Model for General Robot Control"
section: vla
page_id: "1945365620"
permalink: /vla/pi0-a-vision-language-action-flow-model-for-general-robot-control-1945365620/
---

**Paper** : [π0: A Vision-Language-Action Flow Model for General Robot Control](https://arxiv.org/abs/2410.24164)  
**Source** : arXiv / Physical Intelligence,發表於 RSS 2025  
**arXiv ID** : 2410.24164

### Abstract

機器人學習有望釋放靈活、通用、靈巧機器人系統的全部潛力,並解答人工智慧領域最深層的一些問題。然而,要將機器人學習提升到實際系統所需的通用性水準,在資料、泛化與穩健性上都面臨重大障礙。本文討論通才機器人策略(即機器人基礎模型)如何應對這些挑戰,以及如何為複雜且高度靈巧的任務設計有效的通才機器人策略。作者提出一種新穎的 flow matching 架構,建構於預訓練的視覺-語言模型(VLM)之上,以繼承網路規模的語意知識。接著討論如何在來自多種靈巧機器人平台(包含單臂機器人、雙臂機器人與移動操作機器人)的大規模多樣化資料集上訓練此模型。作者從三個面向評估此模型:預訓練後零樣本執行任務的能力、遵循人類與高層 VLM 策略的語言指令的能力,以及透過微調習得新技能的能力。評估涵蓋多樣任務,如疊衣服、清理桌面、組裝箱子。

### Method

![Figure](/assets/images/1945365620_pi0_fig1.png) 

_Figure 1: pi0 overview — VLM backbone plus action expert producing continuous actions via flow matching_

![Figure](/assets/images/1945365620_pi0_fig3.png) 

_Figure 3: Overview of the framework — pre-training mixture, flow matching VLA model with VLM backbone and action expert_

  * 要解決的問題:如何設計一個能處理複雜、高度靈巧任務(如疊衣服這種需要精細連續控制的任務)的通才機器人策略,同時兼顧資料效率、泛化能力與穩健性。
  * 主要方法:提出一種新穎的 flow matching(擴散模型的一種變體)架構,建構於預訓練 VLM 之上,透過 flow matching 直接生成連續的高頻動作序列,而非像 RT-2/OpenVLA 那樣將動作離散化為文字 token。
  * 與以往方式的差異:先前的自回歸式(autoregressive)VLA(如 RT-2、OpenVLA)將動作表示為離散文字 token,逐一生成,對於需要高頻(最高可達 50Hz)且高度靈巧的連續控制任務構成主要挑戰;π0 首次將 flow matching 應用於 VLA 架構,使模型能生成連續、高頻的動作序列,更適合複雜靈巧操作。
  * 重要方法設計描述:架構上包含一個預訓練 VLM 骨幹(繼承網路規模語意知識)與一個較小的「動作專家(action expert)」模組(約 3 億參數),後者根據本體感覺(proprioceptive)輸入與 flow matching 技術生成動作序列;模型在 7 種不同機器人本體配置、68 種任務的多樣資料上進行預訓練;之後可直接零樣本提示執行任務,或針對複雜下游任務(如疊衣服)進行微調。



### Result

  * 主要增強:π0 在零樣本執行、遵循人類/高層 VLM 策略的語言指令、以及透過微調習得新技能三個面向都展現良好表現,尤其在需要高頻、高精度連續控制的複雜靈巧任務(疊衣服、清理桌面、組裝箱子)上,相較於先前自回歸式離散動作表示的方法更具優勢。
  * 是否公正:摘要未提供與 RT-2/OpenVLA 等自回歸式方法的直接數值比較,具體效能對比數據需要查證全文;π0 是由 Physical Intelligence(該領域重要新創公司)發表,後續已被多篇論文(包含本次任務中的多篇可解釋性論文,如 Not All Features Are Created Equal 將 π0.5 列為分析對象)作為分析基準,顯示其結果具一定業界認可度。



### Limitation

  * 論文摘要未明確列出限制章節,但可推測的弱項:(1) flow matching/diffusion 式的動作生成通常需要多步迭代採樣,相較單步生成的自回歸 token 方法,推論時的計算開銷與延遲特性不同,需要查證全文以了解其實際推論速度;(2) 動作專家模組雖然較小(約 3 億參數),但仍需與大型 VLM 骨幹聯合運作,整體系統的部署與服務複雜度可能高於單一模型的方案;(3) 訓練資料雖橫跨 7 種機器人本體,但單臂、雙臂、移動操作機器人之間的資料分布差異可能影響模型在特定本體上的最優表現,需要查證全文。



### Related work

  * 後續 Physical Intelligence 釋出 π0.5(arXiv:2504.16054,2025年4月),針對移動操作進行後訓練特化,進一步強化開放世界泛化能力;更後續據稱已有 π*0.6「從經驗中學習的 VLA」等延伸工作。
  * π0.5 已被多篇 2026 年的 VLA 機制可解釋性論文(如 Not All Features Are Created Equal, 2603.19233;Decoding Task Progress, 2608.13474)選為主要分析對象,顯示 π0 系列已成為學術界研究 VLA 內部機制的重要平台。
  * 值得 survey 的程度極高:π0 是首個將 flow matching 引入 VLA 架構的重要工作,代表了 VLA 動作生成機制從「離散 token」轉向「連續流」的關鍵轉折點,是理解當前 VLA 技術演進的必讀論文。



### Conclusion

  * 綜合評價:π0 透過引入 flow matching 架構,解決了先前自回歸式 VLA 在高頻、高精度連續控制任務上的表達力瓶頸,是 VLA 技術演進的重要里程碑,強烈建議參考。
  * 與其他重要文章的關係:π0 與其後續版本 π0.5 已成為 2026 年多篇 VLA 機制可解釋性研究(SAE、激活注入、任務進度探測等)的核心分析對象,顯示其架構设计(VLM + 動作專家的雙路徑設計)具有代表性,並與 GR00T N1 的「雙系統」架構理念相呼應。對 ROCm/AMD 而言,flow matching/diffusion 式的多步迭代採樣對推論硬體的吞吐與延遲特性要求,與自回歸式生成不同,若 AMD 欲評估 VLA 推論在 ROCm 上的優化空間,π0 這類 flow matching 架構的採樣迴圈效能(例如迭代步數對延遲的影響)會是值得深入研究的面向,但論文本身未觸及 ROCm 或特定硬體的討論,此為延伸判斷。