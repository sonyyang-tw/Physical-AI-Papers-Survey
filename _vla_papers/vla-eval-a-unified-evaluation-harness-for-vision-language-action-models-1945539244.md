---
layout: paper
title: "vla-eval: A Unified Evaluation Harness for Vision-Language-Action Models"
section: vla
page_id: "1945539244"
permalink: /vla/vla-eval-a-unified-evaluation-harness-for-vision-language-action-models-1945539244/
---

**Paper** : [DreamerAD: Efficient Reinforcement Learning via Latent World Model for Autonomous Driving](https://arxiv.org/abs/2603.24587)  
**Source** : arXiv (cs.LG / cs.RO)  
**arXiv ID** : 2603.24587

### Abstract

DreamerAD 是第一個針對自動駕駛設計的「潛在空間世界模型」強化學習框架，主打將擴散模型（diffusion）取樣步驟從 100 步壓縮到 1 步，達到 80 倍加速，同時維持視覺可解釋性。作者指出，真實道路上訓練 RL policy 成本高且不安全；既有的 pixel-level 擴散世界模型雖可支援想像式（imagination-based）安全訓練，但多步擴散推論延遲高（每幀約 2 秒），無法支撐高頻率的 RL 互動。DreamerAD 利用影片生成模型中已去噪的潛在特徵，搭配三項機制加速並穩定訓練，最終在 NavSim v2 上以 87.7 EPDMS 達到 SOTA，證明潛在空間 RL 可用於自動駕駛。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539244_vlaeval_fig1.png) 

_Figure 1: vla-eval overview teaser figure._

  * 要解決的問題：既有 pixel-level diffusion world model 用於自動駕駛 RL 訓練時，多步擴散取樣延遲太高（約 2 秒/幀），無法支援高頻率 RL 互動；同時真實路測資料成本高、風險大。
  * Main method：DreamerAD 提出三個關鍵機制：
    * Shortcut forcing：透過遞迴式的多解析度步數壓縮，降低取樣複雜度，把擴散取樣從 100 步壓到 1 步。
    * 自迴歸密集獎勵模型（autoregressive dense reward model）：直接在潛在表示上運作，做細粒度的 credit assignment（獎勵分配）。
    * 針對 GRPO 的高斯詞彙取樣（Gaussian vocabulary sampling）：限制探索空間，使產生的軌跡符合物理可行性。
  * 與以往方式的差異：以往的世界模型多在 pixel 空間做多步擴散去噪，推論慢；DreamerAD 改在「已去噪的潛在特徵」空間上運作，並用 shortcut forcing 大幅減少取樣步數，兼顧速度與視覺可解釋性（因為仍是基於影片生成模型的潛在空間，而非完全黑箱的抽象狀態）。
  * 重要方法設計描述：整體流程可以想像為——輸入的駕駛影片先由影片生成模型（diffusion-based）編碼為潛在序列；shortcut forcing 機制以遞迴、多解析度方式壓縮去噪步驟，讓一次前向即可得到近似 100 步去噪的結果；在此潛在空間上疊加一個自迴歸的獎勵頭，逐幀輸出密集獎勵訊號；RL policy 則用 GRPO（group relative policy optimization 一類方法）在此潛在空間中被訓練，其動作/軌跡取樣使用高斯詞彙分佈加以約束，避免產生不符合物理規律（如瞬移、穿越障礙物）的軌跡。



### Result

  * 主要成果：DreamerAD 在 NavSim v2 上達到 87.7 EPDMS，號稱是目前的 SOTA；同時擴散取樣加速達 80 倍（100 步→1 步）。
  * 增強部分：主要在「訓練效率」（可支援高頻率 RL 互動）與「最終策略表現」（NavSim v2 分數）兩方面同時提升，且保留了視覺可解釋性（相較於全抽象潛在狀態的世界模型，仍可從潛在空間解碼回可視化影片供除錯）。
  * 是否公正：摘要中僅提供作者自己在 NavSim v2 上的分數，未見與其他方法逐項比較的具體數字（如 baseline 的 EPDMS）。需要查證其他論文（例如同期的 NavSim v2 leaderboard 或其他 world-model-based RL 方法）的比較數據，才能確認 87.7 EPDMS 相對其他方法的優勢幅度。



### Limitation

  * 論文中自陳的限制：摘要本身未明確列出 limitation 段落內容（僅有簡短 abstract，未讀取全文 PDF/HTML 內文）。
  * 從結果推測的弱項：
    * 該方法高度依賴預訓練好的影片生成模型作為潛在特徵來源，其上限（世界模型本身的模擬品質）可能限制下游 RL policy 的天花板。
    * Shortcut forcing 將 100 步壓縮到 1 步，是否會在複雜/長尾駕駛場景（如密集互動、罕見事故場景）中犧牲精細度，摘要未說明，需查證全文的消融實驗（ablation）。
    * 此摘要未提及是否已在真實車輛上驗證（sim-to-real gap），僅在 NavSim v2（模擬/離線評測基準）上驗證。



### Related work

  * 暫無發現更新的相關研究（未執行進一步全文獻檢索，僅根據 arXiv abstract 頁面資訊）。若要嚴謹判斷，建議後續搜尋 NavSim v2 相關論文與其他 diffusion-based / latent-based 世界模型在自動駕駛 RL 上的最新工作進行比較。
  * Related work 值得 survey 的程度：中高。此方向（latent world model + RL for AD）與 embodied AI/world model 研究高度相關，建議後續針對 diffusion 加速技術（shortcut forcing 一類方法）與其他 driving world model（如 EOT-WM）做交叉比較。



### Conclusion

  * 綜合評價：這是一篇針對「世界模型 RL 訓練效率」提出具體工程解法的論文，方法論組合（latent 壓縮 + dense reward + 受限探索）具參考價值，尤其對關心訓練吞吐量/延遲的工程師而言，其加速技術（shortcut forcing）值得深入研讀。但由於只讀到摘要，實驗細節、消融分析、與其他方法的公平比較均待查證全文。
  * 與其他重要文章的關係：延伸自「diffusion-based driving world model」與「latent imagination RL（如 Dreamer 系列）」的脈絡；與 EOT-WM（同樣是driving world model，但著重軌跡可控性而非 RL 訓練效率）互補而非直接競爭。
  * ROCm/AMD 待補強部分：摘要未提及具體訓練硬體或框架資訊，看不出與 ROCm/AMD 的明確關聯。若要導入 AMD 硬體訓練此類「diffusion 取樣加速 + latent RL」pipeline，需要進一步查證其對 diffusion 推論優化（如 flash-attention 類算子、混合精度）在 ROCm 上的可移植性，此點論文並未提供資訊，不宜臆測。