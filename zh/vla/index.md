---
layout: default
title: "VLA Papers"
permalink: /zh/vla/
---

# VLA (Vision-Language-Action) Papers

本頁由自動化 Paper Survey Harness 維護，每日依照下方主題分類，挑選一篇當日新發布（arXiv）或近期重要的 top conference 論文，撰寫完整導讀並建立子頁面。

每篇論文標題皆為連結，點擊可進入該論文的完整 survey 子頁面（Abstract / Method / Result / Limitation / Related work / Conclusion）。

---

## 主題分類 (Topic Taxonomy)

### 1. Architecture Paradigms（架構典範：Autoregressive / Diffusion / Flow-matching / Hybrid）

Scope：VLA 的核心動作生成機制設計 — token/action 如何被解碼（離散自迴歸、連續 diffusion、flow matching、或統一/混合方案）。

代表論文：

- [Discrete Diffusion VLA: Bringing Discrete Diffusion to Action Decoding in Vision-Language-Action Policies]({{ site.baseurl }}/zh/vla/discrete-diffusion-vla-bringing-discrete-diffusion-to-action-decoding-in-vision--1945364352/) — arXiv:2508.20072 — 用離散 diffusion 統一 vision/language/action 解碼，優於同 backbone 的 AR baseline
- [DFM-VLA: Iterative Action Refinement for Robot Manipulation via Discrete Flow Matching]({{ site.baseurl }}/zh/vla/dfm-vla-iterative-action-refinement-for-robot-manipulation-via-discrete-flow-mat-1945538880/) — arXiv:2603.26320 — discrete flow matching，可迭代修正已生成的 action token
- [SnapFlow: One-Step Action Generation for Flow-Matching VLAs via Progressive Self-Distillation]({{ site.baseurl }}/zh/vla/snapflow-one-step-action-generation-for-flow-matching-vlas-via-progressive-self--1945767352/) — arXiv:2604.05656 — progressive self-distillation 將 flow-matching 去噪壓縮至 1 步
- [AsyncVLA: Asynchronous Flow Matching for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/asyncvla-asynchronous-flow-matching-for-vision-language-action-models-1945767374/) — arXiv:2511.14148 — 非均勻/異步 flow-matching schedule，長 horizon 下具信心度自我修正
- [Let It Be Simple: One-Step Action Generation for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/let-it-be-simple-one-step-action-generation-for-vision-language-action-models-1945767397/) — arXiv:2606.05737 — 挑戰「一步生成很難」的假設

### 2. Hierarchy: High-Level Planning/Reasoning vs Low-Level Control

Scope：VLM/reasoner 負責任務分解、低階 policy 負責執行的階層式系統；含 VLA 的 chain-of-thought / latent reasoning。

代表論文：

- [What Matters in Orchestrating Robot Policies: A Systematic Study of Hierarchical VLA Agents]({{ site.baseurl }}/zh/vla/what-matters-in-orchestrating-robot-policies-a-systematic-study-of-hierarchical--1945392011/) — arXiv:2606.10267 — 用 options 框架統一 Hi-VLA agent 的系統性研究
- [DualCoT-VLA: Visual-Linguistic Chain of Thought via Parallel Reasoning for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/dualcot-vla-visual-linguistic-chain-of-thought-via-parallel-reasoning-for-vision-1945767494/) — arXiv:2603.22280 — 平行視覺 + 語言 chain-of-thought
- [DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/deepthinkvla-enhancing-reasoning-capability-of-vision-language-action-models-1945473584/) — arXiv:2511.15669 — latent CoT 變數，檢驗推理是否真正驅動動作決策
- [LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks]({{ site.baseurl }}/zh/vla/lohovla-a-unified-vision-language-action-model-for-long-horizon-embodied-tasks-1945538792/) — arXiv:2506.00411 — 統一 backbone 同時做高階規劃與低階控制
- [Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/latent-reasoning-vla-latent-thinking-and-prediction-for-vision-language-action-m-1945391568/) — arXiv:2602.01166 — 將多模態 CoT 內化為連續 latent space
- [ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/) — arXiv:2601.11404（CVPR 2026, AgiBot）— 推理直接發生在動作空間，由 Explicit/Implicit Action Reasoner 雙模組構成，是與語言/視覺 CoT 明確區隔的第三種 CoT 路線

### 3. Efficiency（壓縮 / 快速推論 / 資料效率訓練）

Scope：讓 VLA 可實際部署 — distillation、量化、edge/on-device 推論、延遲特性分析、小型模型。

代表論文：

- [VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model]({{ site.baseurl }}/zh/vla/vla-adapter-an-effective-paradigm-for-tiny-scale-vision-language-action-model-1945538827/) — arXiv:2509.09372 (AAAI 2026) — 極小規模 VLA 範式，強調參數效率
- [EcoVLA: Energy-Efficient Device-Edge Co-Inference for VLA Models under Real-Time Constraints]({{ site.baseurl }}/zh/vla/ecovla-energy-efficient-device-edge-co-inference-for-vision-language-action-mode-1945364578/) — arXiv:2608.15502 — 能源最佳化 device-edge 協同推論
- [How Fast Can I Run My VLA? Demystifying VLA Inference Performance with VLA-Perf]({{ site.baseurl }}/zh/vla/how-fast-can-i-run-my-vla-demystifying-vla-inference-performance-with-vla-perf-1945391760/) — arXiv:2602.18397 — 跨 VLA + 推論系統組合的解析式效能/延遲模型
- [Offline Semantic Guidance for Efficient Vision-Language-Action Policy Distillation (VLA-AD)]({{ site.baseurl }}/zh/vla/offline-semantic-guidance-for-efficient-vision-language-action-policy-distillati-1945473850/) — arXiv:2605.16241 — 從 OpenVLA-7B teacher 蒸餾至 158M student
- [A Survey on Efficient Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/a-survey-on-efficient-vision-language-action-models-1945363892/) — arXiv:2510.24795 — 統一效率分類：模型設計 / 訓練 / 資料

### 4. Memory, History-Awareness & Long-Horizon Control

Scope：處理非 Markov 長 horizon 操作任務的記憶機制（顯式語言記憶、latent memory bank、關鍵幀/事件記憶、world-model imagination）。

代表論文：

- [MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation]({{ site.baseurl }}/zh/vla/memoryvla-perceptual-cognitive-memory-in-vision-language-action-models-for-robot-1945363954/) — arXiv:2508.19236 — Cognition-Memory-Action 框架
- [MemoryVLA++: Temporal Modeling via Memory and Imagination in Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/memoryvla-temporal-modeling-via-memory-and-imagination-in-vision-language-action-1945473250/) — arXiv:2606.09827 — 於去噪 latent space 加入 world-model imagination
- [Explicit Language Memory for Long-Horizon Planning in Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/explicit-language-memory-for-long-horizon-planning-in-vision-language-action-mod-1945364103/) — arXiv:2608.04765 — 每個決策步驟更新的自然語言記憶
- [EventVLA: Event-Driven Visual Evidence Memory for Long-Horizon Vision-Language-Action Policies]({{ site.baseurl }}/zh/vla/eventvla-event-driven-visual-evidence-memory-for-long-horizon-vision-language-ac-1945538699/) — arXiv:2606.20092 — 動態關鍵幀證據記憶
- [Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation (LaMem-VLA)]({{ site.baseurl }}/zh/vla/dual-latent-memory-in-vision-language-action-models-for-robotic-manipulation-1945391543/) — arXiv:2607.07608 — 雙重 latent 短/長期記憶

### 5. Data, Benchmarks & Simulation

Scope：訓練語料、模擬環境，以及 VLA policy 的評測套件/穩健性壓力測試。

代表論文：

- [LIBERO-Para: A Diagnostic Benchmark and Metrics for Paraphrase Robustness in VLA Models]({{ site.baseurl }}/zh/vla/libero-para-a-diagnostic-benchmark-and-metrics-for-paraphrase-robustness-in-vla--1945766990/) — arXiv:2603.28301 — 揭露原版 LIBERO 對指令改寫的脆弱性
- [vla-eval: A Unified Evaluation Harness for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/vla-eval-a-unified-evaluation-harness-for-vision-language-action-models-1945539244/) — arXiv:2603.13966 — 跨 18 個 benchmark、13 個 model server 的統一評測
- [VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks]({{ site.baseurl }}/zh/vla/vlabench-a-large-scale-benchmark-for-language-conditioned-robotics-manipulation--1945474246/) — arXiv:2412.18194 (ICCV 2025) — 長 horizon 語言條件操作 benchmark
- [VLA-REPLICA: A Low-Cost, Reproducible Benchmark for Real-World Evaluation of Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/vla-replica-a-low-cost-reproducible-benchmark-for-real-world-evaluation-of-visio-1945392290/) — arXiv:2605.20774 — 低成本可重現的真實世界評測 benchmark
- [Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines]({{ site.baseurl }}/zh/vla/vision-language-action-in-robotics-a-survey-of-datasets-benchmarks-and-data-engi-1945392329/) — arXiv:2604.23001 (TMLR)
- [Scaling Sim-to-Real VLA Reinforcement Learning with Generative 3D Worlds]({{ site.baseurl }}/zh/vla/scaling-sim-to-real-vla-reinforcement-learning-with-generative-3d-worlds-1985671234/) — arXiv:2603.18532 (CoRL 2026) — 3D 世界生成模型驅動場景多樣性規模化 sim-to-real RL

### 6. Embodiment Diversity（人形 / 雙臂 / 四足 / 自駕）

Scope：跨具身與特定具身的 VLA 適配 — 人形全身操作、四足操作、雙臂靈巧操作、自駕 VLA。

代表論文：

- [WholeBodyVLA: Towards Unified Latent VLA for Whole-Body Loco-Manipulation Control]({{ site.baseurl }}/zh/vla/wholebodyvla-towards-unified-latent-vla-for-whole-body-loco-manipulation-control-1945392363/) — arXiv:2512.11047 (ICLR 2026) — 統一 latent VLA 做全身移動+操作
- [HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL]({{ site.baseurl }}/zh/vla/haf-adapting-generalist-vlas-to-humanoid-whole-body-loco-manipulation-via-hierar-1945364999/) — arXiv:2608.16837
- [Human-as-Humanoid: Enabling Zero-Shot Humanoid Learning from Ego-Exo Human Videos with Human-Aligned Embodiments]({{ site.baseurl }}/zh/vla/human-as-humanoid-enabling-zero-shot-humanoid-learning-from-ego-exo-human-videos-1945539450/) — arXiv:2606.32009
- [LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction]({{ site.baseurl }}/zh/vla/leverb-humanoid-whole-body-control-with-latent-vision-language-instruction-1945539712/) — arXiv:2506.13751 — 透過 latent action vocabulary + RL controller 的人形全身控制
- [ChainFlow-VLA: Causal Flow Planning with Vision-Language Models]({{ site.baseurl }}/zh/vla/chainflow-vla-causal-flow-planning-with-vision-language-models-1945365318/) — arXiv:2605.23270 — 自駕專用 AR+diffusion 軌跡生成

### 7. World Models Integration（World Action Models）

Scope：結合預測式 world/video model 與動作生成，提升泛化性、穩健性與模擬/規劃能力。與 [World Model Papers]({{ site.baseurl }}/zh/wm/) 頁面有主題重疊，此處聚焦「動作生成優先」的整合研究。

代表論文：

- [World Action Models: The Next Frontier in Embodied AI]({{ site.baseurl }}/zh/vla/world-action-models-the-next-frontier-in-embodied-ai-1945392639/) — arXiv:2605.12090 — 定義 WAM 分類：Cascaded vs Joint WAM
- [Do World Action Models Generalize Better than VLAs? A Robustness Study]({{ site.baseurl }}/zh/vla/do-world-action-models-generalize-better-than-vlas-a-robustness-study-1945392664/) — arXiv:2603.22078
- [In-Context World Modeling for Robotic Control]({{ site.baseurl }}/zh/vla/in-context-world-modeling-for-robotic-control-1945474654/) — arXiv:2606.26025
- [World Model for Robot Learning: A Comprehensive Survey]({{ site.baseurl }}/zh/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/) — arXiv:2605.00080
- [Robots Need More than VLA and World Models]({{ site.baseurl }}/zh/vla/robots-need-more-than-vla-and-world-models-1945392804/) — arXiv:2606.06556 — 立場論文，指出資料/具身/world-model 介面缺口

### 8. Interpretability & Diagnostics（附加主題）

Scope：VLA 內部機制的因果分析、探測、失敗預測。

代表論文：

- [Embodied Interpretability: Linking Causal Understanding to Generalization in Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/embodied-interpretability-linking-causal-understanding-to-generalization-in-visi-1945539823/) — arXiv:2605.00321 (ICML 2026)
- [Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models]({{ site.baseurl }}/zh/vla/sparse-autoencoders-reveal-interpretable-and-steerable-features-in-vla-models-1945539857/) — arXiv:2603.19183
- [Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/not-all-features-are-created-equal-a-mechanistic-study-of-vision-language-action-1945539900/) — arXiv:2603.19233 — 視覺路徑主導語言
- [Decoding Task Progress from VLA Representations]({{ site.baseurl }}/zh/vla/decoding-task-progress-from-vla-representations-1945539940/) — arXiv:2608.13474
- [Tri-Info: Generalizable, Interpretable Failure Prediction for VLA Models via Information Theory]({{ site.baseurl }}/zh/vla/tri-info-generalizable-interpretable-failure-prediction-for-vla-models-via-infor-1945392973/) — arXiv:2606.19998
- [Artificial Foveated Perception for Mitigating Shortcut Learning in Robotic Foundation Models]({{ site.baseurl }}/zh/vla/artificial-foveated-perception-for-mitigating-shortcut-learning-in-robotic-found-1972778734/) — arXiv:2607.10655（CoRL 2026, Yale/UConn/PKU/Imperial）— policy-agnostic 遮罩預測器，微調期間監督 policy 注意力以緩解 shortcut learning，推論時零額外開銷

---

## 基礎/參考模型（不分主題，任何 survey 都應知道的里程碑）

1. [RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control]({{ site.baseurl }}/zh/vla/rt-2-vision-language-action-models-transfer-web-knowledge-to-robotic-control-1945474821/) — arXiv:2307.15818 (Google DeepMind) — 建立 VLA 典範
2. [OpenVLA: An Open-Source Vision-Language-Action Model]({{ site.baseurl }}/zh/vla/openvla-an-open-source-vision-language-action-model-1945393020/) — arXiv:2406.09246 — 開源 7B VLA
3. [π0: A Vision-Language-Action Flow Model for General Robot Control]({{ site.baseurl }}/zh/vla/pi0-a-vision-language-action-flow-model-for-general-robot-control-1945365620/) — arXiv:2410.24164 (Physical Intelligence, RSS 2025) — flow-matching 連續動作通用 policy
4. [GR00T N1: An Open Foundation Model for Generalist Humanoid Robots]({{ site.baseurl }}/zh/vla/gr00t-n1-an-open-foundation-model-for-generalist-humanoid-robots-1945393079/) — arXiv:2503.14734 (NVIDIA) — dual-system 人形基礎模型
5. [Helix: A Vision-Language-Action Model for Generalist Humanoid Control]({{ site.baseurl }}/zh/vla/helix-a-vision-language-action-model-for-generalist-humanoid-control-1945393112/) — Figure AI 官方部落格 — 首個支援人形上半身高頻全身控制的 VLA
6. [π*0.6: a VLA That Learns From Experience]({{ site.baseurl }}/zh/vla/pistar06-a-vla-that-learns-from-experience-1978234561/) — arXiv:2511.14759 (Physical Intelligence) — 首次系統性將 RL（Recap 方法）整合進 π 系列模型，讓 VLA 從真實世界自主經驗中持續自我改進

---

## 每日 Paper 推送記錄

> 以下由排程任務自動新增，每篇新論文皆標註推送日期、所屬主題分類、來源（arXiv 當日新作 / top conference）。

_(尚無記錄 — 排程啟動後將自動累積)_

### 推送日期: 2026-09-08

[τ0-VLA: a Hierarchical Robot Foundation Model with World-Model-Guided Test-Time Computation]({{ site.baseurl }}/zh/vla/τ0-vla-a-hierarchical-robot-foundation-model-with-world-model-guided-test-time-c-1946673513/) — Hierarchy: High-Level Planning/Reasoning vs Low-Level Control（主題分類2）／World Models Integration（主題分類7）交叉 — arXiv:2608.16885，2026年8月17日提交，尚未於本頁記錄

選中原因：出自 Agibot Finch（與 Shanghai Innovation Institute、香港中文大學合作）——符合「科技大廠/知名實驗室出品」準則；將 test-time compute scaling 引入階層式 VLA 的高階子任務生成，並以 world model 預測候選子任務的視覺結果作為評分依據，是與既有「world model 輔助動作生成」路線明確區隔的方法論創新，而非既有技巧的小幅組合；訓練資料規模達 40,115 小時真實世界資料，屬工業級投入。

τ0-VLA 解決長 horizon 機器人操作任務中「高階決策無法依難度動態分配運算資源」的問題：其高階策略結合 proposal model、world model、value model 與 reflective model，在不確定的決策點上以 world-model 引導的 beam search 對候選子任務進行視覺結果預測與評分，再由 reflective model 產生最終子任務，低階策略則以 flow matching 執行跨具身動作。在四項真實機器人長 horizon 任務中，階層式系統平均成功率達 45%（優於 GR00T N1.7 的 2.5% 與 π0.5 的 22.5%），且測試時運算 (TTC) 相較單次規劃 (Plan Once) 全面提升成功率與子任務預測準確率。主要限制：真實機器人評測樣本量偏小（每任務僅10次試驗），且 world model 預測誤差可能反向誤導高階決策，這類 world-model-guided 方法的普遍風險論文未見針對性分析。

### 推送日期: 2026-09-09

[π0.7: a Steerable Generalist Robotic Foundation Model with Emergent Capabilities]({{ site.baseurl }}/zh/vla/π07-a-steerable-generalist-robotic-foundation-model-with-emergent-capabilities-1951435101/) — 基礎/參考模型（π 系列旗艦，屬架構典範與階層規劃跨主題）— arXiv:2604.15483，2026年4月16日提交（4月24日修訂），top conference caliber 出品、尚未於本頁記錄過

選中原因：出自 Physical Intelligence（π0 / RSS 2025 原創團隊），符合「科技大廠/知名實驗室出品」準則；提出「多樣情境條件」（diverse context conditioning）訓練範式，用 episode metadata + 次目標圖片作為額外條件訊號，讓模型能吃下異質、次優甚至失敗軌跡的資料並實現可組合泛化，是明確的方法論創新而非既有技巧的小幅組合；air fryer 案例（訓練資料僅兩段零碎示範，靠半小時人類教練式提示將成功率從 5% 拉到 95%）展示了具代表性的泛化與可引導性突破。

π0.7 解決 VLA「可組合泛化」長期難以實現的問題：5B 參數模型（4B VLM backbone + MEM 影片歷史編碼器 + 860M action expert），推論時由同架構高階語意策略生成指令，並由 BAGEL-based 輕量 world model 產生次目標圖片。關鍵結果：在未見過的多階段廚房任務、跨具身摺衣、操作濃縮咖啡機等任務上開箱即用即逼近專門 RL 微調模型的水準，air fryer 案例成功率從 5% 提升到 95%。限制：作者坦承在大規模多樣資料集上很難嚴格界定任務是否真正「未見過」，且高成功率仰賴人類即時教練式提示介入，純零樣本能力可能被高估；此外評測多由 Physical Intelligence 自行執行，尚待第三方獨立復現。

### 推送日期: 2026-09-10

[EgoScale: Scaling Dexterous Manipulation with Diverse Egocentric Human Data]({{ site.baseurl }}/zh/vla/egoscale-scaling-dexterous-manipulation-with-diverse-egocentric-human-data-1955533518/) — Data, Benchmarks & Simulation（主題分類5，兼具 Embodiment Diversity 靈巧手操作元素）— arXiv:2602.16710，2026年2月18日提交，top conference caliber 出品（NVIDIA GEAR 主導）、尚未於本頁記錄過

選中原因：作者群為 NVIDIA GEAR 團隊（含 Linxi "Jim" Fan、Yuke Zhu、Danfei Xu）與 UC Berkeley（Trevor Darrell）、University of Maryland（Furong Huang）合作，符合「科技大廠/知名實驗室出品」準則；首次系統性驗證「大規模第一人稱人類影片資料規模」與驗證損失之間存在對數線性 scaling law，且此驗證損失可預測下游真實機器人表現，是資料規模化路線上具方法論意義的實證創新，而非既有技巧的小幅組合；訓練資料規模達 20,854 小時、動作標註第一人稱人類影片，超越先前研究 20 倍以上，屬工業級投入。

EgoScale 解決「機器人遙操作資料成本高、難以規模化」的問題：以兩階段流程（大規模人類資料預訓練 + 輕量人機對齊中訓練）訓練 VLA 模型，並以連續代理動作標籤從無標籤人類影片中提取可遷移的互動知識。關鍵結果：在 22 自由度靈巧機械手上，相較無預訓練基線平均成功率提升 54%，且能有效遷移至自由度較低的機械手，顯示大規模人類動作提供可重複使用、跨具身的運動先驗；同時發現的 scaling law 為業界資料採集投資規劃提供量化依據。主要限制：偽動作標籤（源自人類姿態估計）的雜訊如何影響下游策略精細動作精度未見充分敏感度分析，且全部評測基於單一機構內部任務與硬體平台，跨機構外部驗證仍待補足。

### 推送日期: 2026-09-11

[IMLE-VLA: Fast Single-Step Action Generation for Vision-Language-Action Policies]({{ site.baseurl }}/zh/vla/imle-vla-fast-single-step-action-generation-for-vision-language-action-policies-1960020599/) — Architecture Paradigms（主題分類1）— arXiv:2609.10915，2026年9月10日新作，arXiv 當日新作（前一日提交）

選中原因：已被 IEEE/RSJ IROS 2026 接受，符合「top conference caliber」準則；雖作者群（Simon Fraser University、University of Pennsylvania、Amii）非傳統科技大廠，但方法論直接建立於並大幅超越 Physical Intelligence 的旗艦模型 π0.5（本頁已收錄之基礎模型），故與本頁核心研究脈絡高度相關；以 conditional Implicit Maximum Likelihood Estimation (cIMLE) 訓練單步動作生成頭取代 diffusion/flow-matching 迭代動作頭，是真正的方法論創新（而非既有單步生成技巧的小幅組合），並同時通過模擬與真實機器人的完整驗證。

IMLE-VLA 解決 VLA 動作頭依賴多步迭代取樣（如 π0.5 的 10 步 Euler 積分）造成推論延遲、機器人動作走走停停的問題：以 cIMLE 目標函數訓練單步條件生成器，取樣多個候選動作僅對最接近示範的樣本做梯度更新，藉此保留動作多模態覆蓋同時消除迭代取樣。應用於 π0.5 後，推論頻率從 15Hz 提升至 55Hz（3.67倍），LIBERO 40 任務 benchmark 平均成功率達 98.0%（所有 baseline 中最高），LIBERO-plus 擾動測試下仍保有 π0.5 原有穩健度，真實 Franka Panda 機械臂四項任務全面勝過 π0.5，jerk 降低 2.2–3.0 倍。主要限制：cIMLE 對取樣因子 m 的超參數選擇較敏感（m=1 時退化為標準回歸），且真實世界驗證僅限單一機械手臂與四項任務，跨具身可遷移性尚未驗證。

### 推送日期: 2026-09-14

[HuRo: Robotizing Human Videos for Scalable VLA Pretraining]({{ site.baseurl }}/zh/vla/huro-robotizing-human-videos-for-scalable-vla-pretraining-1964050194/) — Data, Benchmarks & Simulation（主題分類5，兼具大規模人類資料規模化元素）— arXiv:2609.10706，2026年9月10日新作，已被 CoRL 2026 接受（top conference caliber）、尚未於本頁記錄過

選中原因：已被 CoRL 2026 正式接受，符合「top conference caliber」準則；作者群來自韓國延世大學（Seon Joo Kim 團隊），雖非傳統科技大廠出品，但本文與本頁已收錄的 NVIDIA GEAR「大規模人類資料規模化」路線（EgoScale、DreamDojo）方法論高度相關且互補；方法論上首次系統性驗證「端到端動作+視覺聯合機器人化」相較「純視覺遷移」的效果差異，並提出可規模化的機器人化管線本身（而非僅產出訓練資料或驗證 scaling law），是資料工程路線上具方法論意義的創新，而非既有技巧的小幅組合；資料集規模達 63 萬段機器人化 episode、1.42 億影格，屬工業級投入。

HuRo 解決「機器人示範資料採集成本過高、難以規模化」的問題：建立機器人化管線，將異質人類活動影片的觀測與動作訊號重定向並轉換為機器人對齊格式，補全跨標註層級缺失的中介訊號，再以此對 VLA 模型進行端到端預訓練。關鍵結果：在四項真實世界操作任務上，隨機器人化預訓練規模擴大，整體完成率由 51.5% 提升至 80.3%，分布外（OOD）完成率由 34.9% 提升至 72.2%；消融實驗證明視覺機器人化能提升 OOD 穩健性，且端到端動作+視覺聯合轉換優於純視覺遷移。主要限制：機器人化管線仰賴多層級標註與訊號推斷，其誤差對下游動作精度的影響未見充分敏感度分析，且評測僅限四項真實任務與五個人類影片來源，跨機構外部驗證仍待補足。

### 推送日期: 2026-09-15

[ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/) — Hierarchy: High-Level Planning/Reasoning vs Low-Level Control（主題分類2，CoT/推理相關子方向）— arXiv:2601.11404，2026年1月16日提交（3月30日修訂v2），已被 CVPR 2026 正式接受（top conference caliber）、尚未於本頁記錄過

選中原因：已被 CVPR 2026 接受，符合「top conference caliber」準則；作者群與程式碼倉庫（github.com/AgibotTech/ACoT-VLA）確認出自 AgiBot（本頁已收錄之 τ0-VLA 亦為同一團隊），符合「科技大廠/知名實驗室出品」準則；提出「Action Chain-of-Thought」——推理直接發生在動作空間（而非既有的語言子任務或目標影像合成等間接中介表示）——是與本頁既有 CoT 路線（DualCoT-VLA 的語言+視覺平行 CoT、DeepThinkVLA 與 Latent Reasoning VLA 的 latent CoT）明確區隔的第三種 CoT 空間，屬方法論創新而非既有技巧的小幅組合。

ACoT-VLA 解決傳統 VLA 直接映射多模態輸入到動作、或以語言子任務/目標影像作為中介推理時，這類間接表示難以承載精確動作執行所需細粒度資訊的問題：核心方法為 Explicit Action Reasoner (EAR) 提出粗粒度參考軌跡作為顯式動作層級推理步驟，並與 Implicit Action Reasoner (IAR) 從 VLM 內部表示萃取的隱式動作先驗共同構成 ACoT，條件化下游動作頭。真實世界與模擬環境的大量實驗顯示此方法優於既有 VLA baseline，並已通過 CVPR 2026 同行評審。主要限制：摘要層級描述未充分揭露 EAR 粗粒度軌跡在長 horizon 任務中累積誤差的風險，亦未討論 EAR/IAR 兩路徑推理不一致時的容錯機制；具體評測任務清單與跨具身泛化能力等細節需查閱全文進一步確認。

### 推送日期: 2026-09-16

[Artificial Foveated Perception for Mitigating Shortcut Learning in Robotic Foundation Models]({{ site.baseurl }}/zh/vla/artificial-foveated-perception-for-mitigating-shortcut-learning-in-robotic-found-1972778734/) — Interpretability & Diagnostics（主題分類8，兼具跨主題「微調穩健性」元素）— arXiv:2607.10655，2026年7月12日提交（9月7日修訂v2），已被 CoRL 2026 正式接受（top conference caliber）、尚未於本頁記錄過

選中原因：已被 CoRL 2026 正式接受，符合「top conference caliber」準則；作者群來自 Yale University、University of Connecticut、Peking University、Imperial College London 等學術機構聯合團隊，雖非傳統科技大廠出品，但真實機器人實驗直接以本頁已收錄之 Physical Intelligence π0.5（基礎/參考模型）作為驗證骨幹，方法論與本頁核心研究脈絡高度相關；提出將「fine-tuning 期間對齊 policy 視覺注意力」重新定義為獨立輔助監督問題，且刻意設計為推論時零額外開銷、不修改 policy 架構本身，是與既有僅在動作層級監督的微調範式明確區隔的方法論創新，而非既有技巧的小幅組合；在四種基礎模型（SmolVLA、OpenVLA、π0.5、Motus）、八項模擬任務與真實機器人五項任務上均完整驗證，並開源程式碼、標註工具與資料集。

本文提出 Artificial Foveated Perception (AFP)，解決機器人基礎模型微調後容易依賴 shortcut（背景紋理、光照、物件共現等與任務成功無因果關係的視覺相關性）、導致環境擾動下失效的問題：核心方法為一個policy-agnostic 的任務條件化遮罩預測器，以 MobileNetV3 特徵路徑與 deformable cross-attention 查詢路徑預測任務相關區域遮罩，微調期間作為輔助 grounding loss 對齊 policy 注意力，推論時完全不參與。關鍵結果：π0.5 的 in-distribution Soft-IoU 從 0.17 提升至 0.93，真實機器人五項任務（含 FurnitureBench）在分佈內外皆全面提升，且長 horizon 多階段任務微調速度明顯加快。主要限制：依賴人類標註的任務相關性遮罩，標註成本與潛在偏誤仍是規模化瓶頸，且真實世界驗證僅限單一機械手臂平台。


### 推送日期: 2026-09-17

[π*0.6: a VLA That Learns From Experience]({{ site.baseurl }}/zh/vla/pistar06-a-vla-that-learns-from-experience-1978234561/) — 基礎/參考模型（π 系列旗艦後繼版本，兼具 RL 訓練配方創新元素）— arXiv:2511.14759，2025年11月14日提交（11月19日修訂v2），top conference caliber 出品（Physical Intelligence 團隊超過 55 位作者）、尚未於本頁記錄過

選中原因：出自 Physical Intelligence（π0 / π0.5 / π0.7 原創團隊），符合「科技大廠/知名實驗室出品」準則；提出 Recap（RL with Experience and Corrections via Advantage-conditioned Policies），首次將示範、自主線上收集資料、專家遠端操作介入三種異質資料來源整合進單一以優勢條件化（advantage conditioning）為核心的 RL 訓練配方，讓 VLA 能在部署後持續透過真實世界經驗自我改進，是與既有純模仿學習或個別 RL 微調技巧明確區隔的方法論創新，而非既有技巧的小幅組合；在摺衣、紙箱組裝、義式咖啡製作三類高難度真實任務上進行長達 13 小時的連續無中斷驗證，屬工業級投入。

π*0.6 解決 VLA policy 以模仿學習訓練時受限於示範資料表現上限、且部署後易受複合誤差影響而無法從自身錯誤學習改進的問題：核心方法 Recap 先以離線 RL 在多任務多機器人資料上訓練價值函數並估計每個動作的優勢，再將 policy 條件化於優勢改善指標，取得改進後的 π*0.6，隨後針對下游任務以少量示範微調並透過自主資料收集與人類遠端操作介入持續以 RL 精進。關鍵結果：在部分最困難任務上將吞吐量提升逾兩倍、失敗率降低約一半，足以支撐連續 13 小時製作咖啡、在陌生家庭連續兩小時以上摺疊全新衣物、以及在真實工廠產線組裝 59 個包裝用紙箱等長時間無中斷運作。主要限制：系統並非完全自主，仍依賴大量人類標註、介入與場景重置，且採用迭代式離線更新而非全線上 RL 迴圈，探索策略也相對樸素，仰賴 policy 隨機性與人類介入。

### 推送日期: 2026-09-21

[XR-1: Towards Versatile Vision-Language-Action Models via Learning Unified Vision-Motion Representations]({{ site.baseurl }}/zh/vla/xr-1-towards-versatile-vision-language-action-models-via-learning-unified-1978567234/) — Architecture Paradigms（主題分類1，兼具 World Models Integration 跨模態表示元素）— arXiv:2511.02776，2025年11月4日提交（2026年7月12日修訂v3），已被 ICML 2026 接受並獲選 Oral（top conference caliber）、尚未於本頁記錄過

選中原因：已被 ICML 2026 接受並獲選 Oral（僅少數論文獲此殊榮），符合「top conference caliber」準則；作者群出自 Beijing Innovation Center of Humanoid Robotics（X-Humanoid，與本頁已收錄之 τ0-VLA、ACoT-VLA、GE-Act 2.0 同源機構），並與北京大學、北京航空航天大學合作，符合「科技大廠/知名實驗室出品」準則；提出 Unified Vision-Motion Codes (UVMC)——以雙分支 VQ-VAE 加共享 codebook 加 KL 對齊損失，首次同時且聯合地從視覺動態與機器人動作兩種模態萃取互補動態知識作為中介表示，是與既有僅從單一模態學習潛在變數引導 policy 學習的方法明確區隔的架構創新，而非既有技巧的小幅組合；在六種異質具身、逾 120 項任務、超過 14,000 次真實機器人 rollout 上完整驗證，屬工業級投入。

XR-1 解決 VLA 模型「難以從高維觀測生成精確低階動作」與「難以彌合跨異質資料來源領域落差」兩項根本挑戰：核心方法為 UVMC，透過雙分支 VQ-VAE（Vision Branch 編碼視覺動態、Motion Branch 編碼動作與本體感覺）共享同一組 codebook 並以對齊損失強迫兩者在共享潛在空間中對齊，再以三階段訓練範式（自監督 UVMC 學習、UVMC 引導跨具身預訓練、任務專屬後訓練）將其應用於下游 policy。關鍵結果：在預訓練階段完全未見過的 Tien Kung 2.0 人形機器人上（20 項任務嚴格具身遷移測試），XR-1 平均成功率達 72.0%，遠超 π0.5（41.0%）、π0（40.8%）、GR00T-N1.5（38.0%）等既有 SOTA baseline；消融實驗證實雙模態聯合編碼、跨資料源對齊（含 Ego4D 人類影片）與規模化預訓練三者缺一不可。主要限制：論文未設立獨立 Limitations 章節具體討論方法侷限，且消融顯示性能高度仰賴大規模預訓練資料規模，對資料稀缺場景的適用性仍待驗證。

### 推送日期: 2026-09-22

[FiberTune: Preserving Action-Fiber Visual Residuals in Vision-Language-Action Fine-Tuning]({{ site.baseurl }}/zh/vla/fibertune-preserving-action-fiber-visual-residuals-in-vision-language-action-fin-1982345671/) — Interpretability & Diagnostics（主題分類8，兼具微調穩健性元素）— arXiv:2606.08653，2026年6月7日提交（9月13日修訂v3），已被 CoRL 2026 正式接受（top conference caliber）、尚未於本頁記錄過

選中原因：已被 CoRL 2026 正式接受，符合「top conference caliber」準則；作者群來自中國科學院大學、紫東太初大模型研究中心、河北工業大學、北京信息科技大學等學術與研究機構聯合團隊，雖非傳統科技大廠出品，但方法論直接建立於本頁已收錄之 π0.5、OpenVLA-OFT（皆為知名基礎模型/框架）之上，並與本頁「Interpretability & Diagnostics」主題下既有的 Artificial Foveated Perception（AFP，同為 CoRL 2026）形成直接呼應；首次將「動作監督僅約束部分特徵方向、其餘動作等價方向的視覺結構完全不受監督」形式化為資訊論問題，並提出「線上動作探針濾除 + 教師殘餘對齊 + 有效秩正則化」的訓練時介入方案，是與既有僅監督完整隱藏狀態（如 BlindVLA）的做法明確區隔的方法論創新，而非既有技巧的小幅組合；在兩個 benchmark、兩種架構（π0.5、OpenVLA-OFT）的六種受控情境與真實世界 SO-101 機械手臂上完整驗證。

FiberTune 解決 VLA 微調時動作監督損失只約束「會改變預測動作」的特徵方向，導致「動作等價」狀態間應保持一致的視覺結構（背景、物件顏色、干擾物等）得不到梯度訊號、可能被壓縮坍縮的問題：核心方法是以線上訓練的線性動作探針估計動作可預測方向並將其從視覺 token 表示中濾除，再將濾除後的殘餘與凍結視覺教師模型做 cosine 對齊、並以批次協方差特徵值的正規化頻譜熵做有效秩正則化，鼓勵殘餘保持高秩不坍縮；教師、探針與對齊模組僅在訓練時使用，推論時零額外開銷。關鍵結果：在 CALVIN ABC→D（π0.5, adapted）上 SR(5) 從 61.4% 提升至 72.1%（+10.7 個百分點），真實世界 SO-101 pick-place 任務成功率從 72.7% 提升至 78.1%，分佈外未見顏色物件成功率提升 15.6 個百分點；消融實驗證實「先濾除動作方向再對齊殘餘」優於直接對齊完整狀態（後者反而傷害效能）。主要限制：探針濾除後的殘餘僅是一階、池化特徵的近似，真實機器人驗證僅限單一任務與單一機械手臂平台，分佈外測試樣本量偏小。

### 推送日期: 2026-09-24

[Scaling Sim-to-Real VLA Reinforcement Learning with Generative 3D Worlds]({{ site.baseurl }}/zh/vla/scaling-sim-to-real-vla-reinforcement-learning-with-generative-3d-worlds-1985671234/) — Data, Benchmarks & Simulation（主題分類5，兼具 Efficiency 推論加速元素）— arXiv:2603.18532，2026年3月19日提交（9月21日修訂v3），已被 CoRL 2026 正式接受（top conference caliber）、尚未於本頁記錄過

選中原因：已被 CoRL 2026 正式接受，符合「top conference caliber」準則；作者群出自 Horizon Robotics General AI 團隊（Andrew Choi、Wei Xu 等），符合「科技大廠/知名實驗室出品」準則；首次系統性驗證「3D 世界生成模型驅動的場景多樣性規模化」對 VLA RL 微調零樣本泛化具有直接因果關係，並以語言驅動場景設計器自動化場景設計流程，是與既有僅在人工設計少數固定場景中做 sim-to-real RL 微調的做法明確區隔的方法論創新，而非既有技巧的小幅組合；同時完整驗證模擬（100 個生成場景）與真實世界（12 場景、240 次試驗）雙軌效果。

本文解決 VLA 的 RL 微調長期面臨的兩難：真實世界 RL 雖規避 sim-to-real 落差，卻因場景多樣性規模化困難而使廣泛預訓練模型退化為過擬合的場景專屬 policy；傳統模擬訓練雖能提供多樣場景，但人工設計場景成本高昂。核心方法結合語言驅動場景設計器與 3D 世界生成模型（以 GPT-4o 驅動多階段 QA 迴圈確保生成品質）自動產出 100 個獨特互動場景，並以 PPOFlow（PPO 化的 ReinFlow 變體）將預訓練 flow-matching VLA policy 轉換為單步高斯 policy 進行高效 RL 微調。關鍵結果：模擬成功率從 9.7% 提升至 79.8%，真實世界成功率從 21.7% 提升至 75%，且消融實驗證實場景多樣性擴大能直接改善零樣本泛化（N=50 相較 N=1 提升 24.7 個百分點）。主要限制：實驗聚焦於取放任務，尚未證實規模化趨勢能否遷移至其他操作技能、VLA 骨幹或具身形態，且固定運算預算下較大場景數的訓練覆蓋度會下降，可能影響對飽和現象的解讀。
