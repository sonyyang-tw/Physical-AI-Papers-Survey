---
layout: paper
title: "Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination"
section: wm
page_id: "1945365146"
permalink: /Physical-AI-Papers-Survey/wm/dream-mpc-gradient-based-model-predictive-control-with-latent-imagination-1945365146/
---

**Paper** : [Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination](https://arxiv.org/abs/2605.04568)  
**Source** : arXiv (cs.LG / cs.AI / cs.RO)，已被 ICML 2026 接受  
**arXiv ID** : 2605.04568

### Abstract

Dream-MPC 提出一種以梯度為基礎（gradient-based）的模型預測控制（MPC）方法，結合學習到的世界模型與策略先驗（policy prior）進行「潛在想像」（latent imagination）式規劃。作者指出，現行最先進的模型式強化學習（model-based RL）方法要嘛用無梯度、族群式（population-based）方法做規劃（如 MPPI/CEM），要嘛用學習到的策略網路，或兩者混合；混合方法（MPC + 學習模型 + 策略先驗）雖已展現不錯效果，但通常仍依賴無梯度優化，對高維控制任務計算成本高。雖然梯度式方法理論上更有效率，但先前研究顯示其實務表現常不如無梯度方法。Dream-MPC 從策略 rollout 出少量候選軌跡，並以學習到的世界模型透過梯度上升逐一優化這些軌跡，搭配不確定性正則化（uncertainty regularization）與跨時間步的優化迭代攤銷（amortization，重複利用先前已優化的動作）。在 24 個連續控制任務上的實驗顯示，Dream-MPC 能顯著提升底層策略表現，並可超越無梯度 MPC 與其他 SOTA baseline。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945365146_dreammpc_fig2.png) 

_Figure 2: Overview of the proposed approach - Dream-MPC以gradient-based MPC在latent space z中優化從policy網路rollout出的動作序列,N條候選軌跡經取樣後平行優化。(註:論文中的Figure 1為結果彙總圖表,非概念圖,故此處僅嵌入方法架構圖Figure 2。)_

  * 要解決的問題：梯度式 MPC 理論上比無梯度方法（MPPI 等）更有效率（模型評估次數更少），但過去實務上表現常常較差；作者要解決「如何讓梯度式 MPC 真正在高維連續控制任務上超越無梯度方法」的問題。
  * Main method：Dream-MPC 從策略網路 π 產生的 rollout 中取出少量候選軌跡（在潛在空間 z 中），對每條候選軌跡以梯度上升法優化其動作序列，目標是最大化某個價值目標 J；同時加入不確定性正則化以避免過度自信地利用世界模型的預測誤差；並透過「跨時間步攤銷」重複利用前一時間步已優化好的動作序列，減少每步都要重新優化的運算量。
  * 與以往方式的差異：相較 MPPI 等無梯度方法需要大量取樣與模型評估（例如 N×I×H = 512×6×3 = 9216 次模型評估），Dream-MPC 只需極少量的候選數與迭代次數（例如 5×1×3 = 15 次模型評估），大幅降低計算成本；同時透過策略先驗生成候選軌跡的起點，讓少量候選也能有效優化，克服了以往「梯度式方法缺乏好的初始提案時表現不佳」的問題。
  * 重要方法設計描述：整體規劃流程為——在每個時間步，策略網路 π 產生 N 條候選動作序列（rollout），這些序列在世界模型的潛在空間中展開為想像軌跡；接著對每條候選軌跡進行 I 次梯度上升迭代，利用世界模型可微分的特性直接對動作序列求梯度以提升目標值 J；不確定性正則化項用來懲罰世界模型預測不確定性高的軌跡分支，避免規劃器鑽入模型誤差的死角；優化完成後，選擇 J 值最高的候選軌跡的第一個動作施加到環境中，並將此軌跡的優化結果保留、攤銷到下一時間步繼續微調（而非從頭優化），藉此把整體優化的時間成本分攤到多個時間步。方法可與 Dreamer、TD-MPC2、DINO-WM、BMPC 等不同的世界模型/策略框架整合（替換其中的規劃器）。



### Result

  * 主要成果：在 DeepMind Control Suite、Meta-World、HumanoidBench 共 24 個連續控制環境上，將 Dream-MPC 整合進 TD-MPC2 與 BMPC，均能顯著提升底層策略表現，並可超越梯度自由的 MPPI 規劃器與其他 SOTA baseline；同時也在圖像觀測（image-based observation）任務上展現優於 MPPI 的效果。
  * 增強部分：主要增強「規劃效率」（大幅減少模型評估次數，如上述 15 次 vs 9216 次）與「策略最終表現」；同時也驗證了方法可跨多種模型式 RL 框架（TD-MPC2、BMPC、Dreamer）遷移使用。
  * 是否公正：作者也誠實指出一個重要限制——在 TD-MPC2 上，Dream-MPC 雖能改善策略表現，但無法穩定超越 MPPI 的表現，顯示梯度式 MPC 對「高品質初始策略先驗」的依賴仍是問題；這代表其優勢並非在所有設定下都一致，屬於較為公正、有自我批判的呈現方式。是否有其他論文（如 ELVIS: Ensemble-Calibrated Latent Imagination for Long-Horizon Visual MPC，同期出現的相關工作）提出不同的比較結果，需要進一步查證。



### Limitation

  * 論文中自陳的限制：作者明確提到（1）固定的優化參數（如迭代次數、學習率等）可能需要依任務動態調整以進一步提升表現；（2）梯度式 MPC 需要高品質的策略先驗（policy prior）才能有效規劃，但這樣的先驗並非總是可得；（3）在 TD-MPC2 上無法穩定匹配 MPPI 的表現。
  * 從結果來看的弱項：方法的效率優勢建立在「少量候選＋少量迭代」的假設上，若策略先驗品質不佳，少量候選可能無法覆蓋足夠的探索空間，導致規劃品質下降；此外方法對超參數（候選數 N、迭代數 I）的敏感度以及跨任務的穩健性，仍待更廣泛驗證。



### Related work

  * 有發現同期（2026 年 5 月）出現的相關工作 ELVIS（Ensemble-Calibrated Latent Imagination for Long-Horizon Visual MPC，arXiv:2605.04709），主題與 Dream-MPC 高度相關（同樣關注 latent imagination 式的 MPC，但著重長時域視覺任務與集成校準的不確定性估計），值得對照比較。
  * Related work 值得 survey 的程度：中高。梯度式規劃與世界模型結合的方向持續活躍（ICML 2026 同時收錄本文），建議後續針對 Dream-MPC、ELVIS 及其各自在 TD-MPC2/Dreamer/BMPC 上的表現做交叉比較。



### Conclusion

  * 綜合評價：這是一篇聚焦「用梯度資訊提升 MPC 規劃效率」的紮實工程型論文，透過候選軌跡＋梯度上升＋攤銷迭代的組合，把模型評估次數壓到極低，同時維持甚至提升策略表現，對關心即時控制/低延遲推論的工程師（如機器人或具身智能系統）有直接參考價值；其自陳限制（依賴策略先驗品質）也讓評價更可信。
  * 與其他重要文章的關係：延伸自 Dreamer 系列（latent imagination 概念的源頭，"Dream to Control: Learning Behaviors by Latent Imagination"）與 TD-MPC2/BMPC 等模型式 RL 框架，挑戰的是傳統無梯度 MPC（MPPI/CEM）在高維任務上的效率瓶頸；與同期 ELVIS 論文構成互補的研究方向。
  * ROCm/AMD 待補強部分：論文未提及具體訓練硬體平台，摘要中也無 ROCm/AMD 相關資訊，看不出明確關聯。若要在 AMD 硬體上部署此類「世界模型可微分規劃」pipeline，需自行驗證其對可微分模擬與世界模型反向傳播在 ROCm 生態下的支援程度，本文並未提供相關資訊。