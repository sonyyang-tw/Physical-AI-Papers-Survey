---
layout: paper
title: "HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL"
section: vla
page_id: "1945364999"
permalink: /Physical-AI-Papers-Survey/vla/haf-adapting-generalist-vlas-to-humanoid-whole-body-loco-manipulation-via-hierar-1945364999/
---

**Paper** : [HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL](https://arxiv.org/abs/2608.16837)  
**Source** : arXiv (cs.RO, cs.AI)  
**arXiv ID** : 2608.16837

### Abstract

人形機器人被視為在以人為中心環境中的通用智能體，深具潛力，但通用型（generalist）VLA 基礎模型並不能直接套用於人形機器人的 whole-body loco-manipulation。人形機器人動作的高維度與各部位間的相互依賴，使傳統單階段 VLA 架構難以有效協調移動、腰部姿態與雙臂操作。此外，透過離線行為克隆（behavior cloning）訓練出的策略，在真實世界部署時仍可能表現不佳；雖然線上強化學習可透過真實世界互動來精煉策略，但直接微調大型 VLA 骨幹網路需要極高運算成本，且在真實機器人探索過程中可能引入安全風險。為解決這些瓶頸，作者提出 HAF（Humanoid Adaptation Framework），一個由 HAF-VLA 與 HAF-Steer 兩部分組成的框架，將現成的通用型 VLA 基礎模型轉移到人形機器人的 whole-body loco-manipulation。HAF-VLA 是建立在預訓練 flow-matching VLA 之上的階層式動作流生成器，將全身動作去噪過程拆分成三個依序階段，並搭配階段嵌入（stage embeddings）與跨階段 KV cache 來保留運動學上的相依性，避免一次性生成導致的全身動作不連貫。在凍結的 HAF-VLA 之上，HAF-Steer 是一個潛在空間的離線轉線上（offline-to-online）強化學習管線，利用 flow-matching 的可逆性與基於 DCT 的降維技術，將 RL 優化限制在一個精簡的噪聲子空間中，訓練一個正則化的 SAC 策略。此設計避免了更新龐大的 VLA 骨幹網路，同時能高效地在真實世界中精煉策略。在七項真實世界人形機器人 loco-manipulation 任務上的評估中，HAF 超越了單階段 VLA baseline，並提升了全身協調性與任務表現。專案網站: <https://grange007.github.io/HAF>

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945364999_haf_fig1.png) 

_Figure 1: HAF overview._

![Figure](/Physical-AI-Papers-Survey/assets/images/1945364999_haf_fig2.png) 

_Figure 2: HAF VLA pipeline._

  * 要解決的問題：通用型 VLA 基礎模型雖然強大，但無法直接套用到人形機器人的 whole-body loco-manipulation，原因有二：(1) 人形動作維度高且各部位（移動、腰部姿態、雙臂）高度相依，單階段 VLA 架構難以協調；(2) 離線行為克隆訓練出的策略在真實部署時可能次優，而直接對大型 VLA 骨幹做線上 RL 微調成本過高且有安全風險。
  * Main method：HAF 框架包含兩個核心元件——(1) HAF-VLA：建立在預訓練 flow-matching VLA 之上的「階層式動作流」生成器，將全身動作的去噪（denoising）過程拆成三個依序階段（推測為下肢移動、軀幹姿態、雙臂操作等分層，摘要未明確列出三階段具體對應內容，需查證全文），並用階段嵌入與跨階段 KV cache 保留各階段間的運動學相依性；(2) HAF-Steer：在凍結的 HAF-VLA 上疊加一個潛在空間的 offline-to-online RL 管線，利用 flow-matching 的可逆性以及基於離散餘弦轉換（DCT）的降維，把 RL 優化限制在一個精簡的「噪聲子空間」內，並訓練一個正則化的 SAC（Soft Actor-Critic）策略。
  * 和以往方式的差異：與傳統「單階段 VLA 一次性生成全身動作」的方式不同，HAF-VLA 採用分階段、有先後依賴關係的動作生成流程，避免一次性生成造成的全身動作不連貫；與傳統「直接微調 VLA 骨幹做線上 RL」不同，HAF-Steer 凍結大型 VLA 骨幹，只在一個經過降維的精簡潛在噪聲子空間內做 RL 優化，大幅降低微調所需運算成本與探索風險。
  * 重要方法設計描述：可以把整個系統想像成「生成 + 微調」兩層架構：底層 HAF-VLA 像一條分階段的裝配線,動作生成依序流過三個處理站,每一站都用「階段嵌入」標記自己的角色,並透過跨階段的 KV cache（類似把前一站的處理結果的關鍵資訊帶到下一站)確保下游動作與上游決策保持運動學一致性,不會出現手腳不同步的怪異動作；上層 HAF-Steer 則像一個安裝在裝配線末端的「校正模組」,它不改動裝配線本身（凍結 HAF-VLA），而是先用 flow-matching 的可逆性把生成過程「倒推」回一個噪聲空間，再用 DCT 把這個噪聲空間壓縮成低維度子空間，最後在這個小空間裡訓練 SAC 策略做即時修正，這樣既能利用真實世界回饋做線上調整，又不需要承擔重新訓練整個大模型的成本與風險。



### Result

  * 在七項真實世界人形機器人 loco-manipulation 任務上的評估顯示,HAF 超越了「vanilla 單階段 VLA baseline」,並提升了全身協調性（whole-body coordination）與任務表現（task performance）。摘要未提供具體的量化數字（如成功率百分比、提升幅度），需要查證全文的實驗表格以了解具體增強程度。
  * 是否公正：需要查證其他論文的比較數據；摘要中的比較對象僅限於「vanilla single-stage VLA baselines」，並未與同批次的 WholeBodyVLA（同樣針對人形 whole-body loco-manipulation）做直接比較，兩者發表時間相近（HAF 更晚），但摘要互不引用，是否有本質性的效能差異需要查證全文或後續文獻。



### Limitation

  * 摘要中沒有明確自陳的 limitation 段落，需要查證全文以了解該框架在何種任務類型或動作複雜度下表現受限，以及三階段動作流的分割方式是否對所有人形任務都適用。
  * 從方法設計推測的潛在弱項：HAF-Steer 將 RL 優化限制在精簡的噪聲子空間內，雖然降低了運算成本與安全風險，但也可能限制了策略能夠探索與修正的自由度上限，對於需要大幅偏離預訓練分布的任務可能改善有限；此外，僅在七項真實世界任務上驗證，任務數量相對有限，其泛化能力的廣度需要進一步查證。



### Related work

  * 與同批次清單中的 WholeBodyVLA（arXiv:2512.11047）高度相關，兩者是同一問題領域（適配通用 VLA 至人形 whole-body loco-manipulation）在相近時間的兩種不同解法，值得對照比較：WholeBodyVLA 著重「從人類影片學習移動操作知識 + 專門 RL 控制器」，HAF 則著重「凍結預訓練 flow-matching VLA + 分階段動作流 + 潛在空間 offline-to-online RL」。
  * 暫無發現比 HAF 更新的直接後續研究（本文於 2026年8月提交，是本清單中發表時間較新的論文之一）。
  * Related work 值得 survey 的程度高：人形機器人 whole-body loco-manipulation 的 VLA 適配是快速發展的熱門子領域，建議將 HAF 與 WholeBodyVLA 一併閱讀比較，以掌握該問題目前的兩大主流技術路線。



### Conclusion

  * 綜合評價：HAF 提出了一套技術上頗具巧思的兩段式解法（分階段動作流生成 + 精簡潛在空間 RL 微調），針對「大型 VLA 骨幹難以安全高效地做線上微調」這個實務痛點提供了具體方案，值得參考，尤其對於想在真實機器人上做線上策略精煉、又想避免重新訓練整個大模型的團隊有參考價值。
  * 與其他重要文章的關係：與 WholeBodyVLA（arXiv:2512.11047）構成同一問題領域的兩種對照解法；HAF-Steer 使用的 flow-matching 可逆性與 DCT 降維技術，延伸自 flow-matching 生成模型與傳統訊號處理（DCT）的結合，是否有進一步挑戰或延伸自其他 latent RL 論文，需要查證全文的相關工作章節。
  * 對 ROCm/AMD：看不出與 ROCm/AMD 有明確的直接關聯,論文聚焦於機器人動作生成架構與強化學習演算法設計,未提及具體的訓練/推論硬體平台選型；不過，HAF-Steer 強調「避免更新大型 VLA 骨幹、只在精簡子空間內做 RL」的設計理念，若要在 AMD/ROCm 平台上部署，理論上可降低對大規模分散式訓練基礎設施的依賴，但這只是推測，摘要本身並未提供支持此判斷的具體細節。