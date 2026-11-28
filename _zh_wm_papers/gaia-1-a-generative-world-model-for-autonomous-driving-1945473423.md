---
layout: paper
title: "GAIA-1: A Generative World Model for Autonomous Driving"
section: wm
page_id: "1945473423"
permalink: /zh/wm/gaia-1-a-generative-world-model-for-autonomous-driving-1945473423/
---

**Paper** : [GAIA-1: A Generative World Model for Autonomous Driving](https://arxiv.org/abs/2309.17080)  
**Source** : arXiv (Technical Report, Wayve)  
**arXiv ID** : 2309.17080

### Abstract

GAIA-1（Generative AI for Autonomy）是 Wayve 提出的生成式世界模型，用於自動駕駛場景生成。模型以影片、文字、動作三種模態作為輸入，將世界建模問題轉化為無監督的序列建模問題：先將輸入映射為離散 token，再以自回歸方式預測下一個 token。模型展現出學習高階場景結構與動態、情境感知、泛化能力、以及對幾何關係的理解等湧現特性。作者認為這種能捕捉未來事件期望的表徵，結合生成逼真樣本的能力，能加速並強化自動駕駛技術的訓練。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473423_gaia1_fig1.png) 

_Figure 1: GAIA-1 multimodal video generation - future rollouts conditioned on actions._

![Figure]({{ site.baseurl }}/assets/images/1945473423_gaia1_fig2.png) 

_Figure 2: Architecture of GAIA-1 - encoding video/text/action into tokens, autoregressive world model, video decoder._

  * 要解決的問題：自動駕駛系統需要有效預測車輛動作後世界可能演化出的各種潛在結果，但現實世界場景複雜且非結構化，難以窮舉建模。
  * Main method：將世界建模視為無監督序列建模問題，把影片、文字、動作輸入映射到離散 token 空間，再訓練一個自回歸的下一個 token 預測模型（類似語言模型的做法，但套用在多模態的駕駛資料上）。
  * 與以往方式的差異：相較於傳統以顯式規則或監督式感知/預測管線（perception-prediction-planning pipeline）處理自動駕駛，GAIA-1 採用生成式、資料驅動的方式，直接從大規模影片資料中學習場景動態，並支援以文字與動作條件細粒度控制生成的駕駛情境（例如指定天氣、其他車輛行為等）。
  * 重要方法設計：架構上分為將原始感測輸入（影片幀、文字、動作）編碼為離散 token 的 tokenizer/encoder 部分，以及一個類似 Transformer 的自回歸世界模型，在 token 序列上進行下一 token 預測；生成階段再將預測出的 token 解碼還原為影片畫面，以此達成對未來場景的模擬與想像（imagination）。



### Result

  * 摘要中強調的成果偏質性描述：模型能展現對場景高階結構與動態的理解、情境感知能力、對新場景的泛化、以及幾何關係的理解，並可依文字/動作輸入生成具有細粒度控制的逼真駕駛影片。
  * 摘要本身並未提供具體的定量指標（如 FID、視覺品質分數等），需要查閱全文/技術報告以取得詳細數據。
  * 是否公正、是否有其他論文結果不符：需要查證其他論文（例如 GAIA-2 或後續自動駕駛世界模型論文）中對 GAIA-1 的比較數據，摘要未提供可供交叉驗證的量化指標。



### Limitation

  * 論文摘要未明確自陳限制（limitation）。
  * 從摘要與後續 GAIA-2 論文的動機描述可推測，GAIA-1 在多視角一致性（multi-camera consistency）、細粒度控制、多代理人互動建模等方面可能存在不足，這也是 GAIA-2 特別強調要解決的問題，說明 GAIA-1 在這些面向的能力有限。
  * 需要進一步查證全文以了解計算成本、生成解析度、時間長度限制等具體弱項。



### Related work

  * GAIA-2（arXiv:2503.20523）是 GAIA-1 的直接後繼工作，針對多視角一致性、細粒度控制與多代理人互動進行改進，值得一併閱讀作為對照。
  * 暫無發現其他更新的、直接挑戰或取代 GAIA-1 的研究；但整體世界模型/影片生成模型（如 NVIDIA Cosmos 系列、Genie 系列）在同一時期快速發展，值得後續 survey。
  * 判斷 related work 值得 survey 的程度：中高，GAIA 系列是自動駕駛專用世界模型的代表性工作，適合與通用世界模型（Genie、Cosmos）做架構與應用場景的對比。



### Conclusion

  * 綜合評價：GAIA-1 是自動駕駛領域生成式世界模型的早期代表作，將 LLM 式的離散 token 自回歸建模成功遷移到多模態駕駛資料上，具有指標性意義，值得作為了解「世界模型在自動駕駛應用」脈絡的入門讀物。
  * 與其他文章的關係：GAIA-1 開創了 Wayve 的 GAIA 系列世界模型，後續被 GAIA-2（latent diffusion 架構）取代／擴展；在方法論上與 DreamerV3（RL 導向的世界模型）、V-JEPA 2（自監督表徵式世界模型）屬於不同路線（GAIA-1 走生成式 token 自回歸路線），可作為世界模型方法論分類的一個重要案例。
  * ROCm/AMD 關聯：摘要中未提及任何特定硬體平台或訓練基礎設施細節，看不出與 ROCm/AMD 有明確關聯；若要補強，AMD 可關注的方向可能是大規模多模態序列模型（類 GPT 架構）在 ROCm 上的訓練效率與生態支援，但這僅為推測，論文本身未觸及此議題。