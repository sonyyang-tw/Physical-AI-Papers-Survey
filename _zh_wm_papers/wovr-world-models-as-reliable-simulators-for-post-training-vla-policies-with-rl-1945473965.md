---
layout: paper
title: "WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL"
section: wm
page_id: "1945473965"
permalink: /zh/wm/wovr-world-models-as-reliable-simulators-for-post-training-vla-policies-with-rl-1945473965/
---

**Paper** : [WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL](https://arxiv.org/abs/2602.13977)  
**Source** : arXiv (cs.RO, cs.AI)，CoRL Preprint  
**arXiv ID** : 2602.13977

### Abstract

強化學習 (RL) 有望為視覺-語言-動作 (VLA) 模型解鎖超越模仿學習的能力，但 RL 需要大量真實世界互動，這使其難以直接部署在實體機器人上。近期研究嘗試用學習到的世界模型作為策略優化的模擬器，然而閉迴路的想像式 rollout (imagined rollout) 難免遭遇幻覺 (hallucination) 與長時間範圍的誤差累積，這些誤差不僅降低視覺保真度，也會誤導策略優化，提供不可靠的學習訊號。本文提出 WoVR，一個可靠的世界模型式 RL 框架，用於 VLA 策略的後訓練 (post-training)。WoVR 不假設世界模型完全忠實，而是明確地規範 RL 如何與不完美的想像動態互動：透過可控的動作條件影片世界模型提升 rollout 穩定性、透過 Keyframe-Initialized Rollouts (KIR) 重塑想像互動以降低有效誤差深度、並透過「世界模型-策略共同演化 (World Model-Policy Co-evolution)」維持策略與模擬器的對齊。實驗顯示 WoVR 能實現穩定的長時間想像 rollout 與有效的策略優化，在 LIBERO 上取得優異表現，並在多個機器人平台上取得一致的真實世界效能提升。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473965_wovr_fig1.png) 

_Figure 2 (原文編號): WoVR 總覽，透過強化世界模型作為可控模擬器、Keyframe-Initialized Rollouts (KIR) 減少誤差深度、以及 PACE 維持策略與模型對齊，建立可靠的強化學習框架。_

![Figure]({{ site.baseurl }}/assets/images/1945473965_wovr_fig2.png) 

_Figure 3 (原文編號): 動作條件世界模型架構，基於影片擴散骨幹並透過雙通道動作注入設計實現逐幀可控性與穩定的分塊自回歸生成。_

  * **要解決的問題** ：世界模型做為 RL 模擬器時，閉迴路想像 rollout 會因幻覺與長時間誤差累積而失真，導致策略優化收到不可靠的學習訊號，難以直接把「不完美的世界模型」當作真實環境使用。
  * **Main method** ：WoVR 包含三個核心組件：
    * 可控的動作條件影片世界模型 (controllable action-conditioned video world model)，提升 rollout 的穩定性與視覺保真度。
    * **Keyframe-Initialized Rollouts (KIR)** ：透過從關鍵影格重新初始化想像互動，縮短「有效誤差深度」(effective error depth)，減少長時間誤差累積對策略學習的傷害。
    * **World Model –Policy Co-evolution**：讓策略的 rollout 資料回饋更新世界模型，世界模型改進後又產生更好的想像資料訓練策略，形成策略與模擬器彼此對齊、共同演化的迴圈。
  * **與以往方式的差異** ：以往方法多半假設世界模型「夠準確」可直接當模擬器使用；WoVR 反其道而行，明確承認世界模型不完美，並設計機制（KIR、co-evolution）主動規範/緩解幻覺與誤差累積對 RL 訓練訊號的污染，而非單純追求提升世界模型本身的準確度。
  * **重要設計描述** ：整體流程為：teleoperated / 真實資料 → 訓練可控動作條件影片世界模型 → VLA 策略在世界模型中進行想像 rollout（透過 KIR 從關鍵影格重啟以限制誤差深度）→ RL 用這些想像 rollout 更新策略 → 策略產生的新行為資料又回饋更新世界模型（co-evolution）→ 反覆迭代，逐步在真實機器人平台上部署驗證。



### Result

  * 在 LIBERO 基準上，WoVR 將平均成功率從 39.95% 提升到 69.2%（+29.3 個百分點），真實機器人任務成功率從 61.7% 提升到 91.7%（+30.0 個百分點）。
  * 在更強的基準設定下（base policy 經過完整軌跡 SFT，已達 88.1%），GRPO 達 89.7%、WMPO 達 92.4%，而 WoVR 仍取得最高平均成功率 95.9%。
  * 在兩個真實機器人平台上部署：Franka 平台提升 +28.9 個百分點，AgileX Piper 平台提升 +13.4 個百分點，均優於對照方法。
  * 世界模型本身達成 SOTA 品質，維持高效率 rollout（23 FPS）。
  * 是否公正：這些數據（69.2%、91.7%、95.9% 等）來自論文自身報告，屬於自我比較性質的結果；根據其他論文（Sword, arXiv:2605.07288）的評論，WoVR 在分布外 (OOD) 條件下的風格穩健性有明顯不足，從約第 15 幀開始生成風格便偏離真實情況，顯示其真實世界改善幅度可能因場景/風格分布而異，這點需要對照原始論文與 Sword 論文的比較設定差異。



### Limitation

  * 論文本身強調「不假設世界模型完全忠實」，這代表其設計出發點就承認世界模型存在幻覺與誤差累積問題，但透過 KIR 和 co-evolution 緩解而非徹底解決。
  * 根據其他論文（Sword）的獨立評論，WoVR 對分布外/風格偏移的穩健性較弱（OOD 情況下約第15幀開始風格偏離 ground truth），這代表其方法可能對訓練分布外場景的泛化能力有限，需要查證原論文是否有討論此限制。
  * 摘要與可得資訊未提供世界模型訓練與 rollout 所需的運算資源規模，也未討論是否有安全性/失敗模式的系統性分析，需要查證全文。



### Related work

  * 相關的同期/後續研究包括：Sword (arXiv:2605.07288，Style-Robust World Models)，該論文將 WoVR 列為比較基準之一，並指出其在風格穩健性上的弱點；World-VLA-Loop (arXiv:2602.06508)；以及一篇 2026 年 5 月的世界模型機器人學習綜合survey (arXiv:2605.00080)，將 WoVR 歸類為「世界模型-策略顯式共同演化」的代表性方法之一。另外還有 "From World Models to World Action Models" 教學型文獻 (arXiv:2607.00836)。
  * 值得 survey 的程度：高。WoVR 提出的 co-evolution 概念已被視為該領域的重要範式之一，並被多篇後續論文引用/比較，建議連同 Sword、World-VLA-Loop 一起追蹤閱讀，以獲得更全面的比較視角。



### Conclusion

  * 整體評價：這是一篇對「世界模型作為 RL 模擬器」這個方向具有代表性意義的論文，其 KIR 與 co-evolution 設計針對性地解決了長期以來世界模型模擬器不可靠的核心痛點，數據增益幅度顯著（LIBERO +29~30個百分點），值得深入參考。但需注意其風格穩健性受到後續論文（Sword）質疑，不宜全盤視為已解決世界模型幻覺問題。
  * 與其他重要文章的關係：WoVR 挑戰了「假設世界模型忠實可直接當模擬器」的先前做法（如更早期的 world-model-based RL 工作），並被 Sword 進一步挑戰其風格穩健性；同時與 World-VLA-Loop 同屬「策略-世界模型閉迴路協同」這一脈絡的代表工作。
  * ROCm/AMD 待補強部分：論文聚焦於演算法/框架設計，未提及具體訓練硬體平台（很可能使用 NVIDIA GPU 生態），沒有討論 ROCm 相容性；若 AMD 想在 MI300 系列上重現此類 world-model RL post-training pipeline，需自行驗證 diffusion/影片生成模型與 RL rollout 管線在 ROCm 上的效能與穩定性，此為明確的待補強空缺。