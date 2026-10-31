---
layout: paper
title: "SuperMimic: Scaling Humanoid Whole-Body Control with One Differentiable World Model"
section: wm
page_id: "2610284800"
permalink: /zh/wm/supermimic-scaling-humanoid-whole-body-control-with-one-differentiable-world-mod-2610284800/
---

### Abstract

追蹤大規模人類動作資料集已成為實現通用、富表現力人形全身控制的主流途徑，但跨大量動作進行規模化訓練成本高昂——既有管線多採用 model-free 強化學習，要嘛透過有損蒸餾合併各動作專家策略，要嘛以叢集級算力暴力訓練單一策略。本論文提出 SuperMimic，以單一可微分 world model 學習所有動作共享的動態特性，並以此分攤（amortize）跨動作的學習成本；該 world model 從標準剛體模擬器（MuJoCo Warp）的紀錄軌跡中擬合而成。World model 與追蹤 policy 在同一個訓練迴圈中共同訓練，透過對短想像 rollout 進行時間反向傳播（backpropagation-through-time, BPTT），policy 獲得解析梯度（analytic gradient）。快速的想像 rollout 與解析梯度使 policy 學習效率大幅提升：在單一 GPU 上訓練 3 小時，SuperMimic 即超越在 128 顆 GPU 上訓練 7 天的 SOTA 動作追蹤基線（SONIC）之回報，GPU 工時降低超過 1000 倍，在 129,514 個 benchmark 動作中僅失敗 25 個（基線失敗 179 個）；以兩顆 GPU 訓練 9.8 小時後，SuperMimic 達到零失敗。從 1 小時到 264 小時的動作資料規模下，world model 的預測誤差維持穩定，達到目標回報所需的 GPU 工時成長緩慢。訓練出的 policy 可零樣本遷移至真實 Unitree G1 人形機器人，執行多樣化甚至高難度特技動作。論文已獲 CoRL 2026 接受為 Oral，作者團隊來自 UC Berkeley（含 Pieter Abbeel、Koushil Sreenath 等知名研究者）。

### Method

- **要解決的問題**：人形全身控制若要泛化至大規模、多樣化的人類動作資料集，既有 model-free RL 管線面臨規模化瓶頸：要嘛為每個動作訓練專家策略再透過蒸餾合併（蒸餾過程有損，合併後效能打折扣），要嘛直接以單一策略暴力學習所有動作（需要叢集級算力，如 SONIC 基線使用 128 顆 L40 GPU 訓練 7 天，約 21,000 GPU 工時）。算力成本成為衡量「動作追蹤規模化定律（scaling law）」的實際障礙，使研究者難以系統性探索資料規模與效能之間的關係。

- **Main method**：SuperMimic 的核心思路是以一個可微分 world model 分攤所有動作共享的動態特性學習，取代為每個動作單獨學習或暴力擴大規模。具體而言，先以標準剛體模擬器 MuJoCo Warp 蒐集紀錄軌跡（log transitions），擬合出一個學習得到的、可微分的 world model；接著 world model 與追蹤 policy 在同一訓練迴圈中共同訓練——world model 在每次迭代都更新（並非先訓練後凍結），而策略更新時 world model 被暫時固定。訓練時 policy 在 world model 內進行短想像 rollout（32 步），透過 BPTT 取得解析策略梯度，而非依賴 model-free RL 的高變異梯度估計；一個 critic 負責 bootstrap 超出想像 horizon 之外的回報（實驗顯示若無 critic，16 步以下的想像 horizon 會訓練失敗，有 critic 則 16 步即可匹配無 critic 32 步的效果）。由於從未對模擬器本身取微分，此方法可相容於具有非平滑接觸（non-smooth contact）的標準剛體模擬器，不需要特製的可微分物理引擎。

- **和以往方式的差異**：既有 model-free RL 方法（如 SONIC）必須透過與模擬器大量互動取得高變異的策略梯度估計，難以規模化；SuperMimic 則是先用一個「可微分代理模型」取代模擬器本身的梯度角色，讓策略能透過解析梯度高效學習，大幅降低了達到目標回報所需的想像步數（相較 PPO-WM 基線減少約 64 倍）與總體 GPU 工時（超過 1000 倍）。此外，世界模型驅動的想像 rollout 在批次運算規模下比 MuJoCo Warp 本身快超過 10 倍（在實際使用的 2k–16k 平行環境範圍內，分別快 11 倍與 26 倍），使得大規模平行想像訓練在算力上可行。

- **關鍵方法圖**：見下方嵌入圖片——第一張圖為論文項目首頁展示圖，呈現模擬 Unitree G1 機器人完成側滾翻、空翻等高難度動作，標語「算力不再是瓶頸」；第二張圖呈現 SuperMimic 與基線 SONIC 的算力對比示意，128 顆 GPU 的訓練牆收斂為單一 GPU 卡片，直觀呈現超過 1000 倍的 GPU 工時降低幅度。

![Figure]({{ site.baseurl }}/assets/images/2610.28480_supermimic_teaser.jpg)

_Figure 1: SuperMimic 項目首頁展示圖——模擬 Unitree G1 人形機器人執行空翻、側滾翻、迪斯可舞步等高難度全身動作，標語「算力不再是瓶頸」_

![Figure]({{ site.baseurl }}/assets/images/2610.28480_supermimic_compute.jpg)

_Figure 2: SuperMimic 與 SONIC 算力對比示意——128 顆 GPU 組成的訓練牆（背景模糊）收斂為單一 GPU 卡片（前景清晰），直觀呈現 GPU 工時降低超過 1000 倍的規模化優勢_

### Result

- **主要增強部分**：在單一 H100 GPU 上訓練 3 小時，SuperMimic 即超越 SONIC released checkpoint（128 顆 L40 GPU 訓練 7 天，約 21,000 GPU 工時）的正規化回報（0.90）；以此換算，SuperMimic 在總體 GPU 工時上降低超過 1000 倍，牆鐘時間降低超過 50 倍。在涵蓋 129,514 個 benchmark 動作的失敗率評測中，SONIC released checkpoint 失敗 179 個動作（含全部 44 個空翻與全部 22 個側滾翻），SuperMimic 在單 GPU 訓練 3 小時後僅失敗 25 個，以雙 GPU 訓練 9.8 小時後達到零失敗。World model 預測誤差從 1 小時到 264 小時的動作資料規模下維持在 0.007–0.011 區間，顯示其能穩定吸收規模持續成長的訓練資料；訓練出的策略並可直接零樣本遷移至真實 Unitree G1 機器人，完成側滾翻、180 度空翻等高難度特技動作且無需逐動作微調。

- **結果是否公正**：論文在 FAQ 章節中主動揭露並檢視了與基線比較的潛在不公平因素——SuperMimic 僅使用 SONIC 全部 611 小時資料中的公開子集 BONES-SEED（264.56 小時，少 2.3 倍），且兩者硬體不同（H100 相較 L40 的 fp32 算力為 0.74 倍、tensor-core 峰值為 5.5 倍），論文明確指出「2.3 倍資料量差異與至多 5.5 倍峰值算力差異，不足以解釋 1000 倍的 GPU 工時落差」，以此論證核心結論的穩健性而非迴避比較公平性問題，顯示作者對結果有審慎且透明的交代。

### Limitation

- **已知 limitation**：論文 FAQ 中明確說明 benchmark 動作同時是兩種方法的訓練動作，因此失敗率數字衡量的是「覆蓋率（coverage）」而非「泛化能力（generalization）」，也就是說目前結果並未直接驗證 policy 對訓練集以外全新動作的泛化表現。此外，真實機器人驗證雖已完成多樣動作的零樣本遷移，但論文未提供在更大範圍環境擾動（如不同地形、外部干擾）下的系統性穩健性數據。

- **從 result 來看的弱項**：由於 World model 需要與 policy 同步每次迭代更新（而非一次性擬合後凍結），此設計雖提升了樣本效率，但也意味著 world model 本身的擬合品質與穩定性成為整體訓練流程的潛在瓶頸，若動態特性過於複雜或多樣（超越人形全身動作追蹤的範疇），單一共享 world model 能否持續有效分攤學習成本仍待更廣泛任務類型的驗證。

### Related work

- SuperMimic 與本頁「Model-Based RL / Latent Dynamics for Control」主題下的 DreamerV3、Dream-MPC 等論文同屬「以學習到的動態模型取代直接與真實/模擬環境互動以提升樣本效率」這一經典 model-based RL 脈絡，但 SuperMimic 的獨特之處在於其應用場景聚焦於人形全身動作追蹤這一高維、高動態的具體問題，並且明確展示了可微分 world model 搭配 BPTT 解析梯度在算力規模化上帶來的巨大（超過三個數量級）效率提升，將 model-based RL 的理論優勢轉化為可驗證的規模化定律測量工具。
- 判斷值得 survey 的程度：高。SuperMimic 已獲 CoRL 2026 接受為 Oral，出自 UC Berkeley 知名研究團隊（含 Pieter Abbeel、Koushil Sreenath），在同一 benchmark 上直接對比 SOTA 基線並提供了透明的算力公平性討論，且已完成真實人形機器人驗證，是近期將 world model 應用於人形控制規模化訓練的代表性工作。

### Conclusion

- **綜合評價**：SuperMimic 以單一可微分 world model 搭配 policy 共同訓練與 BPTT 解析梯度，成功將人形全身動作追蹤的訓練算力需求從叢集級（128 顆 GPU、7 天）降低至單一 GPU、數小時量級，GPU 工時降低超過 1000 倍，同時在失敗率與回報兩項核心指標上超越 SOTA model-free RL 基線，並完成真實機器人零樣本遷移驗證。其價值不僅在於效率提升本身，更在於讓「動作追蹤規模化定律」的系統性測量從算力不可行變為算力可行，為後續人形全身控制的規模化研究打開了新的實驗空間。

- **與其他重要文章的關係**：SuperMimic 可與本頁「Robot-Specific Action-Conditioned World Models」主題下聚焦機器人操作任務的 world model（如 Ctrl-World、DreamDojo）互補對照——後者關注操作任務的視覺/動作預測，SuperMimic 則示範了 world model 在人形全身運動控制這一不同任務類型上，透過可微分性直接服務於策略梯度計算（而非僅作為規劃或資料生成工具）的另一種應用範式。ROCm/AMD 在此領域尚待補強之處：SuperMimic 的核心訓練迴圈高度依賴 world model 與 policy 的高頻共同迭代、BPTT 反向傳播以及大規模平行想像 rollout（2k–16k 平行環境），這對底層深度學習框架在可微分模擬、長序列反向傳播記憶體效率與平行 rollout 吞吐量上提出了具體要求；若 AMD 欲在人形機器人規模化訓練基礎設施市場站穩腳步，驗證 ROCm 軟體棧對這類「可微分 world model + BPTT policy gradient」訓練範式的框架相容性與效能表現，將是值得關注的生態系拓展方向。
