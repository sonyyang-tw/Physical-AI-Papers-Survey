---
layout: paper
title: "IMLE-VLA: Fast Single-Step Action Generation for Vision-Language-Action Policies"
section: vla
page_id: "1960020599"
permalink: /zh/vla/imle-vla-fast-single-step-action-generation-for-vision-language-action-policies-1960020599/
---

### Abstract

IMLE-VLA 提出一種以 conditional Implicit Maximum Likelihood Estimation (cIMLE) 訓練的單步動作生成頭，用以取代 VLA 模型中常見的 diffusion / flow-matching 動作頭。現行主流設計（如 π0.5）依賴多步迭代取樣（例如 10 個 Euler 步），造成推論延遲、機器人動作出現「走走停停」的不連續運動，且降低任務完成速度。cIMLE 目標函數能保留動作的多模態覆蓋（避免單純回歸頭常見的 mode collapse），同時完全消除多步取樣。將 IMLE-VLA 套用於 π0.5 後，推論頻率提升 3.67 倍（55Hz vs. 15Hz），動作吞吐量最高提升 11 倍。在 40 項任務的 LIBERO benchmark 上，IMLE-VLA 取得所有 baseline 中最高的平均成功率（98.0%），同時保有最高推論頻率；在 LIBERO-plus 的測試時擾動下，IMLE-VLA 維持 π0.5 原有的穩健度，而其他快速 baseline 則明顯劣化。真實世界 Franka Emika Panda 機械臂四項任務實驗顯示動作更平滑（jerk 降低 2.2–3.0 倍），任務完成更快，且在每一項任務上都優於 π0.5，平均每回合 VLA 推論時間降低 3.9–6.6 倍。論文已被 IEEE/RSJ IROS 2026 接受。

### Method

**要解決的問題** ：VLA policy 常見設計是將預訓練 VLM backbone 搭配獨立的連續動作頭，並以 diffusion 或 flow matching 訓練。這類動作頭依賴多步迭代去噪取樣（π0.5 使用 10 個 Euler 步），造成明顯的推論瓶頸：機器人呈現走走停停的運動模式，任務完成速度下降，且高頻閉環控制難以實現。

**Main method** ：作者提出以 conditional Implicit Maximum Likelihood Estimation (cIMLE) 訓練一個單步條件生成器，直接取代原有的迭代式動作頭。cIMLE 的核心想法是：對每個條件（觀測+語言指令），從潛在雜訊中取樣 m 個候選動作，僅對其中「最接近」真實示範動作的樣本做梯度更新（nearest-neighbor 式的 loss），如此在保留單步生成（無需迭代去噪）的同時，仍能捕捉動作分布的多模態性，避免了單純 L2 回歸頭常見的模式崩塌（mode collapse）問題。

**和以往方式的差異** ：與 diffusion/flow-matching 動作頭（需要多步迭代求解 ODE/SDE）不同，cIMLE 動作頭在推論時只需一次前向傳遞即可生成完整動作，架構上是「即插即用」地替換掉 π0.5 原有的 flow-matching 動作頭，其餘 VLM backbone 與訓練資料維持不變，因此改動集中在動作生成機制本身，而非整體系統重新設計。

**關鍵方法圖示** ：Fig. 1（已嵌入下方）展示 IMLE-VLA 作為「即插即用」單步動作頭取代原本迭代式模組的整體架構；Fig. 5（已嵌入下方）展示三類真實世界實驗（單步操作、多步序列推理、動態反應性任務）的定性比較，顯示 IMLE-VLA 動作更快、更平滑、成功率更高。

![Figure]({{ site.baseurl }}/assets/images/1960020599_imle_overview.png) 

_Fig. 1: IMLE-VLA 整體架構 — 以單步 cIMLE 動作頭取代迭代式 diffusion/flow-matching 動作頭_

![Figure]({{ site.baseurl }}/assets/images/1960020599_imle_experiments.png) 

_Fig. 5: 真實世界三類任務實驗（單步操作、多步序列推理、動態反應性）定性比較_

### Result

**主要增強** ：(1) 推論頻率從 π0.5 的 15Hz 提升至 55Hz（3.67倍），H=10 執行 horizon 下動作吞吐量最高提升 11 倍；(2) LIBERO 40 任務 benchmark 平均成功率 98.0%，為所有 baseline 中最高，同時仍保有最快推論頻率；(3) LIBERO-plus 分布位移測試下，其他快速 baseline 成功率隨擾動程度嚴重下滑，IMLE-VLA 則維持接近 π0.5 原有的穩健度；(4) 真實世界 Franka Panda 四項任務中，IMLE-VLA 在每一項任務都勝過 π0.5，動作 jerk 降低 2.2–3.0 倍，每回合 VLA 推論耗時降低 3.9–6.6 倍。

**結果是否公正** ：論文的比較基準（π0.5、其他單步/少步 baseline）皆為近期公開強基線，且同時報告了模擬與真實機器人兩類實驗，並附上不同執行 horizon 與 cIMLE 樣本因子 m 的消融實驗（Fig. 3、Fig. 4），顯示作者對結果穩健度有充分交代。真實世界實驗樣本量為每任務 20 回合，規模中等但屬合理範圍；未發現與其他論文（如 π0.5 原始論文）報告數字存在明顯矛盾，98.0% 的 LIBERO 成功率與近期文獻中高效能 VLA 的成功率區間（95–99%）大致相符。

### Limitation

**已知限制** ：cIMLE 依賴取樣因子 m（訓練時每個條件抽取的候選動作數）進行多模態覆蓋，m=1 時退化為標準回歸（喪失多模態能力），顯示方法對超參數選擇較敏感；論文並未討論此方法在更複雜、長 horizon、需要顯式多階段推理的任務上（如本頁其他 hierarchy/reasoning 類別論文）的表現是否同樣具優勢。

**從 result 推論的弱項** ：真實世界實驗僅涵蓋四項任務、單一機械手臂（Franka Panda）與單一 GPU（A6000），跨具身（如人形、雙臂）的可遷移性尚未驗證；此外，最佳執行 horizon H=10 是針對 LIBERO 選定的，是否對所有下游任務都是最佳設定仍待更多驗證。

### Related work

本頁已收錄多篇聚焦「效率/單步生成」的相近論文，如 SnapFlow（progressive self-distillation 壓縮 flow-matching 至一步）與 Let It Be Simple（挑戰「單步生成很難」的假設），IMLE-VLA 與此二者在同一子主題方向上互為對照，可合併閱讀比較不同單步生成策略（self-distillation vs. cIMLE）之間的優劣與適用場景差異。值得後續追蹤 arXiv 上是否有更多以 cIMLE / 隱式最大似然估計應用於機器人動作生成的後續工作。

### Conclusion

IMLE-VLA 是一篇方法論簡潔且驗證扎實的論文：明確指出「單步生成 vs. 多模態覆蓋」這一效率/表現力權衡的核心痛點，並以 cIMLE 提供一個相對優雅的解法，同時附有模擬與真實機器人的完整驗證，並已被 IROS 2026 接受，值得參考。與本頁「Architecture Paradigms」子主題下的 SnapFlow、Let It Be Simple 構成三角對照關係，共同描繪 VLA 動作頭正朝「單步高頻推論」方向演進的趨勢；與 π0.5（基礎模型）則是直接的「效率增強插件」關係。對 ROCm/AMD 而言，此類論文凸顯的缺口在於：目前主流 VLA 推論效能評測與最佳化（如本文的 L40S GPU 基準）幾乎清一色基於 NVIDIA 生態，AMD 尚缺乏公開的 VLA 推論延遲/吞吐量基準測試與對應的 ROCm 優化案例，值得作為後續補強方向。