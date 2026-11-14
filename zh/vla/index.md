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

- [IMLE-VLA: Fast Single-Step Action Generation for Vision-Language-Action Policies]({{ site.baseurl }}/zh/vla/imle-vla-fast-single-step-action-generation-for-vision-language-action-policies-1960020599/) — arXiv:2609.10915（IROS 2026）— 以 conditional IMLE 訓練單步動作生成頭取代迭代 diffusion/flow-matching 動作頭，應用於 π0.5 後推論頻率提升 3.67 倍
- [XR-1: Towards Versatile Vision-Language-Action Models via Learning Unified Vision-Motion Representations]({{ site.baseurl }}/zh/vla/xr-1-towards-versatile-vision-language-action-models-via-learning-unified-1978567234/) — arXiv:2511.02776（ICML 2026 Oral）— 雙分支 VQ-VAE 共享 codebook 聯合編碼視覺動態與機器人動作，提升跨具身遷移泛化
- [Holo-M: Humanoid Loco-Manipulation With Discrete VLA Model]({{ site.baseurl }}/zh/vla/holo-m-humanoid-loco-manipulation-with-discrete-vla-model-1791131204/) — arXiv:2609.35709（Horizon Robotics）— 依身體部位拆解的 tokenizer（FAST-RVQ 量化）搭配分組離散擴散解碼，支援人形全身 loco-manipulation

- [FocusVLA: Future-Intent Guided Dynamic View Routing for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/focusvla-future-intent-guided-dynamic-view-routing-for-vision-language-action-2610314230/) — arXiv:2610.31423（CoRL 2026，2026-10-22 新作）— 預測未來互動意圖以引導動作生成時的動態多視角路由，修正多視角 VLA 的「視角依賴慣性」，RoboTwin 2.0 平均成功率提升 10.10 pp、真實世界達 85.0%

- [APT: Action Expert Pretraining Improves Instruction Generalization of Vision-Language-Action Policies]({{ site.baseurl }}/zh/vla/apt-action-expert-pretraining-improves-instruction-generalization-2606123660/) — arXiv:2606.12366（CoRL 2026，浙江大學/RobbyAnt/浙江人形機器人創新中心）— 以貝氏分解將 policy 拆為語言無關的 Vision-Action 先驗與語言條件化概似函數，兩階段訓練 action expert，解決連續動作 VLA 的 OOD 語言泛化瓶頸

- [NestedVLA: Learning to Consolidate and Generate Skills for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/nestedvla-learning-to-consolidate-and-generate-skills-for-vision-language-ac-2610232710/) — arXiv:2610.23271（NeurIPS 2026，香港理工大學）— 以嵌入 VLA 的任務條件超網路「生成」action-expert 參數更新取代既有合併方法的「選擇」範式，解決多個獨立訓練 VLA policy 事後整合時的參數衝突問題

- [FlowVLA: Enabling World Dynamics Understanding through Pluggable 3D Flow Learning]({{ site.baseurl }}/zh/vla/flowvla-enabling-world-dynamics-understanding-through-pluggable-3d-flow-2610161600/) — arXiv:2610.16160（CoRL 2026，Ajou University / Samsung Electronics）— 以重建導出的 3D flow 作訓練期專屬監督，點層級+TCP層級雙重 flow 耦合場景動態與控制訊號，零推論期開銷下提升跨架構 VLA 操作表現與零樣本穩健性

- [FR-VLA: Implicit Force Reasoning VLA for Contact-Rich Manipulation]({{ site.baseurl }}/zh/vla/fr-vla-implicit-force-reasoning-vla-for-contact-rich-manipulation-2610259810/) — arXiv:2610.25981（CoRL 2026，NTU / A*STAR SIMTech）— 以可學習力查詢 token 推導力許可訊號，分離力相關性判斷與力表徵，解決力覺模態何時接地進入動作生成的問題

- [CoRE-VLA: Towards Scalable and Robust Vision-Language-Action Modeling via Conditional Routing of Experts]({{ site.baseurl }}/zh/vla/core-vla-towards-scalable-and-robust-vision-language-action-modeling-2607036930/) — arXiv:2607.03693（CoRL 2026，浙江大學 / 上海創新研究院 / 復旦大學）— 將動作生成 formalize 為情境條件化稀疏運算，感測器可用性與任務意圖雙重條件化路由至通用或模態特化專家，LIBERO 全部四子套件達最佳表現

### 2. Hierarchy: High-Level Planning/Reasoning vs Low-Level Control

Scope：VLM/reasoner 負責任務分解、低階 policy 負責執行的階層式系統；含 VLA 的 chain-of-thought / latent reasoning。

代表論文：

- [What Matters in Orchestrating Robot Policies: A Systematic Study of Hierarchical VLA Agents]({{ site.baseurl }}/zh/vla/what-matters-in-orchestrating-robot-policies-a-systematic-study-of-hierarchical--1945392011/) — arXiv:2606.10267 — 用 options 框架統一 Hi-VLA agent 的系統性研究
- [DualCoT-VLA: Visual-Linguistic Chain of Thought via Parallel Reasoning for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/dualcot-vla-visual-linguistic-chain-of-thought-via-parallel-reasoning-for-vision-1945767494/) — arXiv:2603.22280 — 平行視覺 + 語言 chain-of-thought
- [DeepThinkVLA: Enhancing Reasoning Capability of Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/deepthinkvla-enhancing-reasoning-capability-of-vision-language-action-models-1945473584/) — arXiv:2511.15669 — latent CoT 變數，檢驗推理是否真正驅動動作決策
- [LoHoVLA: A Unified Vision-Language-Action Model for Long-Horizon Embodied Tasks]({{ site.baseurl }}/zh/vla/lohovla-a-unified-vision-language-action-model-for-long-horizon-embodied-tasks-1945538792/) — arXiv:2506.00411 — 統一 backbone 同時做高階規劃與低階控制
- [Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/latent-reasoning-vla-latent-thinking-and-prediction-for-vision-language-action-m-1945391568/) — arXiv:2602.01166 — 將多模態 CoT 內化為連續 latent space
- [ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/) — arXiv:2601.11404（CVPR 2026, AgiBot）— 推理直接發生在動作空間，由 Explicit/Implicit Action Reasoner 雙模組構成，是與語言/視覺 CoT 明確區隔的第三種 CoT 路線

- [τ0-VLA: a Hierarchical Robot Foundation Model with World-Model-Guided Test-Time Computation]({{ site.baseurl }}/zh/vla/τ0-vla-a-hierarchical-robot-foundation-model-with-world-model-guided-test-time-c-1946673513/) — arXiv:2608.16885（AgiBot Finch）— 以 world-model 引導 beam search 評分候選子任務，將 test-time compute scaling 引入階層式 VLA 高階決策

### 3. Efficiency（壓縮 / 快速推論 / 資料效率訓練）

Scope：讓 VLA 可實際部署 — distillation、量化、edge/on-device 推論、延遲特性分析、小型模型。

代表論文：

- [VLA-Adapter: An Effective Paradigm for Tiny-Scale Vision-Language-Action Model]({{ site.baseurl }}/zh/vla/vla-adapter-an-effective-paradigm-for-tiny-scale-vision-language-action-model-1945538827/) — arXiv:2509.09372 (AAAI 2026) — 極小規模 VLA 範式，強調參數效率
- [EcoVLA: Energy-Efficient Device-Edge Co-Inference for VLA Models under Real-Time Constraints]({{ site.baseurl }}/zh/vla/ecovla-energy-efficient-device-edge-co-inference-for-vision-language-action-mode-1945364578/) — arXiv:2608.15502 — 能源最佳化 device-edge 協同推論
- [How Fast Can I Run My VLA? Demystifying VLA Inference Performance with VLA-Perf]({{ site.baseurl }}/zh/vla/how-fast-can-i-run-my-vla-demystifying-vla-inference-performance-with-vla-perf-1945391760/) — arXiv:2602.18397 — 跨 VLA + 推論系統組合的解析式效能/延遲模型
- [Offline Semantic Guidance for Efficient Vision-Language-Action Policy Distillation (VLA-AD)]({{ site.baseurl }}/zh/vla/offline-semantic-guidance-for-efficient-vision-language-action-policy-distillati-1945473850/) — arXiv:2605.16241 — 從 OpenVLA-7B teacher 蒸餾至 158M student
- [A Survey on Efficient Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/a-survey-on-efficient-vision-language-action-models-1945363892/) — arXiv:2510.24795 — 統一效率分類：模型設計 / 訓練 / 資料

- [VLaRL: Augmenting Vision-Language-Action Models with Simulation-Trained Latent-Conditioned Residual RL]({{ site.baseurl }}/zh/vla/vlarl-augmenting-vision-language-action-models-with-simulation-trained-latent-c-1790912345/) — arXiv:2609.30868（Microsoft Research，2026-09-25 新作）— 用凍結 VLA 自身的 latent 表示作為模擬到真實遷移介面，搭配輕量 mapper 對齊模擬/真實 latent 分佈，訓練殘差 RL 修正接觸豐富任務執行精度

- [Fast-VLA: You Only Think Once for Robot Manipulation]({{ site.baseurl }}/zh/vla/fast-vla-you-only-think-once-for-robot-manipulation-2610213890/) — arXiv:2610.21389（華為新加坡研究中心，2026-10-15 新作）— 每個 episode 僅呼叫一次凍結 VLM 建構固定 KV 任務記憶，輕量線上 actor 負責高頻閉環控制，RoboTwin 攤銷推論時間降低 10.9–17.1 倍

- [REACT: Rolling Denoising and Dual Decoupling for Reactive Robot Control with VLA Models]({{ site.baseurl }}/zh/vla/react-rolling-denoising-and-dual-decoupling-for-reactive-robot-control-with-vla-2610120070/) — arXiv:2610.12007（CoRL 2026 Spotlight，2026-10-08 新作）— 交錯時間步的滾動去噪持久動作緩衝區，搭配感知/VLM/去噪/執行四階段解耦，同時提升成功率、降低反應延遲並產生更平滑軌跡

### 4. Memory, History-Awareness & Long-Horizon Control

Scope：處理非 Markov 長 horizon 操作任務的記憶機制（顯式語言記憶、latent memory bank、關鍵幀/事件記憶、world-model imagination）。

代表論文：

- [MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation]({{ site.baseurl }}/zh/vla/memoryvla-perceptual-cognitive-memory-in-vision-language-action-models-for-robot-1945363954/) — arXiv:2508.19236 — Cognition-Memory-Action 框架
- [MemoryVLA++: Temporal Modeling via Memory and Imagination in Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/memoryvla-temporal-modeling-via-memory-and-imagination-in-vision-language-action-1945473250/) — arXiv:2606.09827 — 於去噪 latent space 加入 world-model imagination
- [Explicit Language Memory for Long-Horizon Planning in Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/explicit-language-memory-for-long-horizon-planning-in-vision-language-action-mod-1945364103/) — arXiv:2608.04765 — 每個決策步驟更新的自然語言記憶
- [EventVLA: Event-Driven Visual Evidence Memory for Long-Horizon Vision-Language-Action Policies]({{ site.baseurl }}/zh/vla/eventvla-event-driven-visual-evidence-memory-for-long-horizon-vision-language-ac-1945538699/) — arXiv:2606.20092 — 動態關鍵幀證據記憶
- [Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation (LaMem-VLA)]({{ site.baseurl }}/zh/vla/dual-latent-memory-in-vision-language-action-models-for-robotic-manipulation-1945391543/) — arXiv:2607.07608 — 雙重 latent 短/長期記憶

- [MEM: Multi-Scale Embodied Memory for Vision Language Action Models]({{ site.baseurl }}/zh/vla/mem-multi-scale-embodied-memory-for-vision-language-action-models-1996734521/) — arXiv:2603.03596（Physical Intelligence）— 短 horizon 影片記憶與長 horizon 語言記憶雙模態系統,支援長達十五分鐘的操作任務與情境中策略調整

### 5. Data, Benchmarks & Simulation

Scope：訓練語料、模擬環境，以及 VLA policy 的評測套件/穩健性壓力測試。

代表論文：

- [LIBERO-Para: A Diagnostic Benchmark and Metrics for Paraphrase Robustness in VLA Models]({{ site.baseurl }}/zh/vla/libero-para-a-diagnostic-benchmark-and-metrics-for-paraphrase-robustness-in-vla--1945766990/) — arXiv:2603.28301 — 揭露原版 LIBERO 對指令改寫的脆弱性
- [vla-eval: A Unified Evaluation Harness for Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/vla-eval-a-unified-evaluation-harness-for-vision-language-action-models-1945539244/) — arXiv:2603.13966 — 跨 18 個 benchmark、13 個 model server 的統一評測
- [VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks]({{ site.baseurl }}/zh/vla/vlabench-a-large-scale-benchmark-for-language-conditioned-robotics-manipulation--1945474246/) — arXiv:2412.18194 (ICCV 2025) — 長 horizon 語言條件操作 benchmark
- [VLA-REPLICA: A Low-Cost, Reproducible Benchmark for Real-World Evaluation of Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/vla-replica-a-low-cost-reproducible-benchmark-for-real-world-evaluation-of-visio-1945392290/) — arXiv:2605.20774 — 低成本可重現的真實世界評測 benchmark
- [Vision-Language-Action in Robotics: A Survey of Datasets, Benchmarks, and Data Engines]({{ site.baseurl }}/zh/vla/vision-language-action-in-robotics-a-survey-of-datasets-benchmarks-and-data-engi-1945392329/) — arXiv:2604.23001 (TMLR)
- [Scaling Sim-to-Real VLA Reinforcement Learning with Generative 3D Worlds]({{ site.baseurl }}/zh/vla/scaling-sim-to-real-vla-reinforcement-learning-with-generative-3d-worlds-1985671234/) — arXiv:2603.18532 (CoRL 2026) — 3D 世界生成模型驅動場景多樣性規模化 sim-to-real RL

- [EgoScale: Scaling Dexterous Manipulation with Diverse Egocentric Human Data]({{ site.baseurl }}/zh/vla/egoscale-scaling-dexterous-manipulation-with-diverse-egocentric-human-data-1955533518/) — arXiv:2602.16710（NVIDIA GEAR）— 驗證第一人稱人類影片資料規模與驗證損失間的對數線性 scaling law，可預測下游真實機器人表現
- [HuRo: Robotizing Human Videos for Scalable VLA Pretraining]({{ site.baseurl }}/zh/vla/huro-robotizing-human-videos-for-scalable-vla-pretraining-1964050194/) — arXiv:2609.10706（CoRL 2026）— 機器人化管線將異質人類影片轉換為機器人對齊格式，支援端到端 VLA 預訓練

- [RynnVLA-Latent: Scaling Robotic Manipulation Foundation Models with 3D-Grounded Latent Actions]({{ site.baseurl }}/zh/vla/rynnvla-latent-scaling-robotic-manipulation-foundation-models-with-3d-ground-2610343560/) — arXiv:2610.34356（DAMO Academy, Alibaba Group，2026-10-25 新作）— RynnLAM 以幾何監督與相機運動解耦從 30.1K 小時異質影片學習 3D 接地 latent action，4B policy 於 LIBERO 達 98.8%、RoboTwin 2.0 達 88.6%

- [Splat2Act: From Captured Scenes to Personalized VLA Manipulation]({{ site.baseurl }}/zh/vla/splat2act-from-captured-scenes-to-personalized-vla-manipulation-2611139450/) — arXiv:2610.13945（CoRL 2026，Georgia Tech / Toyota Research Institute / Waymo）— 僅需手持手機掃描與物件影像即可個人化 VLA policy 的全自動 real-to-sim-to-real 管線，真實 Stretch 3 機器人成功率與模擬高度吻合

### 6. Embodiment Diversity（人形 / 雙臂 / 四足 / 自駕）

Scope：跨具身與特定具身的 VLA 適配 — 人形全身操作、四足操作、雙臂靈巧操作、自駕 VLA。

代表論文：

- [WholeBodyVLA: Towards Unified Latent VLA for Whole-Body Loco-Manipulation Control]({{ site.baseurl }}/zh/vla/wholebodyvla-towards-unified-latent-vla-for-whole-body-loco-manipulation-control-1945392363/) — arXiv:2512.11047 (ICLR 2026) — 統一 latent VLA 做全身移動+操作
- [HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL]({{ site.baseurl }}/zh/vla/haf-adapting-generalist-vlas-to-humanoid-whole-body-loco-manipulation-via-hierar-1945364999/) — arXiv:2608.16837
- [Human-as-Humanoid: Enabling Zero-Shot Humanoid Learning from Ego-Exo Human Videos with Human-Aligned Embodiments]({{ site.baseurl }}/zh/vla/human-as-humanoid-enabling-zero-shot-humanoid-learning-from-ego-exo-human-videos-1945539450/) — arXiv:2606.32009
- [LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction]({{ site.baseurl }}/zh/vla/leverb-humanoid-whole-body-control-with-latent-vision-language-instruction-1945539712/) — arXiv:2506.13751 — 透過 latent action vocabulary + RL controller 的人形全身控制
- [ChainFlow-VLA: Causal Flow Planning with Vision-Language Models]({{ site.baseurl }}/zh/vla/chainflow-vla-causal-flow-planning-with-vision-language-models-1945365318/) — arXiv:2605.23270 — 自駕專用 AR+diffusion 軌跡生成
- [IronMind: Scaling Humanoid Dexterous Manipulation via Camera-Space Ego-Centric Pretraining]({{ site.baseurl }}/zh/vla/ironmind-scaling-humanoid-dexterous-manipulation-via-camera-space-ego-centric-pretraining-1790838047/) — arXiv:2609.39403（XPeng Robotics, 2026-09-30 當日新作）— 以相機空間動作表示取代人體重定向，統一第一人稱人類影片與異質機器人資料的動作介面，萬小時預訓練在真實人形機器人分佈外任務上達 55.0% 成功率

### 7. World Models Integration（World Action Models）

Scope：結合預測式 world/video model 與動作生成，提升泛化性、穩健性與模擬/規劃能力。與 [World Model Papers]({{ site.baseurl }}/zh/wm/) 頁面有主題重疊，此處聚焦「動作生成優先」的整合研究。

代表論文：

- [World Action Models: The Next Frontier in Embodied AI]({{ site.baseurl }}/zh/vla/world-action-models-the-next-frontier-in-embodied-ai-1945392639/) — arXiv:2605.12090 — 定義 WAM 分類：Cascaded vs Joint WAM
- [Do World Action Models Generalize Better than VLAs? A Robustness Study]({{ site.baseurl }}/zh/vla/do-world-action-models-generalize-better-than-vlas-a-robustness-study-1945392664/) — arXiv:2603.22078
- [In-Context World Modeling for Robotic Control]({{ site.baseurl }}/zh/vla/in-context-world-modeling-for-robotic-control-1945474654/) — arXiv:2606.26025
- [World Model for Robot Learning: A Comprehensive Survey]({{ site.baseurl }}/zh/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/) — arXiv:2605.00080
- [Robots Need More than VLA and World Models]({{ site.baseurl }}/zh/vla/robots-need-more-than-vla-and-world-models-1945392804/) — arXiv:2606.06556 — 立場論文，指出資料/具身/world-model 介面缺口

- [Vision-Language-Delta-Action: Learning Compact Deltas as Actionable Transition Interfaces for Robotic Manipulation]({{ site.baseurl }}/zh/vla/vision-language-delta-action-learning-compact-deltas-as-actionable-transition-i-2610258740/) — arXiv:2610.25874（百度 LoongForge，2026-10-19 新作）— 以緊湊 Delta 變數取代完整未來狀態預測，作為 VLA 與 WAM 之間的第三種中介轉變介面

### 8. Interpretability & Diagnostics（附加主題）

Scope：VLA 內部機制的因果分析、探測、失敗預測。

代表論文：

- [Embodied Interpretability: Linking Causal Understanding to Generalization in Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/embodied-interpretability-linking-causal-understanding-to-generalization-in-visi-1945539823/) — arXiv:2605.00321 (ICML 2026)
- [Sparse Autoencoders Reveal Interpretable and Steerable Features in VLA Models]({{ site.baseurl }}/zh/vla/sparse-autoencoders-reveal-interpretable-and-steerable-features-in-vla-models-1945539857/) — arXiv:2603.19183
- [Not All Features Are Created Equal: A Mechanistic Study of Vision-Language-Action Models]({{ site.baseurl }}/zh/vla/not-all-features-are-created-equal-a-mechanistic-study-of-vision-language-action-1945539900/) — arXiv:2603.19233 — 視覺路徑主導語言
- [Decoding Task Progress from VLA Representations]({{ site.baseurl }}/zh/vla/decoding-task-progress-from-vla-representations-1945539940/) — arXiv:2608.13474
- [Tri-Info: Generalizable, Interpretable Failure Prediction for VLA Models via Information Theory]({{ site.baseurl }}/zh/vla/tri-info-generalizable-interpretable-failure-prediction-for-vla-models-via-infor-1945392973/) — arXiv:2606.19998
- [Artificial Foveated Perception for Mitigating Shortcut Learning in Robotic Foundation Models]({{ site.baseurl }}/zh/vla/artificial-foveated-perception-for-mitigating-shortcut-learning-in-robotic-found-1972778734/) — arXiv:2607.10655（CoRL 2026, Yale/UConn/PKU/Imperial）— policy-agnostic 遮罩預測器，微調期間監督 policy 注意力以緩解 shortcut learning，推論時零額外開銷

- [FiberTune: Preserving Action-Fiber Visual Residuals in Vision-Language-Action Fine-Tuning]({{ site.baseurl }}/zh/vla/fibertune-preserving-action-fiber-visual-residuals-in-vision-language-action-fin-1982345671/) — arXiv:2606.08653（CoRL 2026）— 以線上動作探針濾除動作可預測方向，對殘餘做教師對齊與有效秩正則化，避免視覺結構坍縮

---

## 基礎/參考模型（不分主題，任何 survey 都應知道的里程碑）

1. [RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control]({{ site.baseurl }}/zh/vla/rt-2-vision-language-action-models-transfer-web-knowledge-to-robotic-control-1945474821/) — arXiv:2307.15818 (Google DeepMind) — 建立 VLA 典範
2. [OpenVLA: An Open-Source Vision-Language-Action Model]({{ site.baseurl }}/zh/vla/openvla-an-open-source-vision-language-action-model-1945393020/) — arXiv:2406.09246 — 開源 7B VLA
3. [π0: A Vision-Language-Action Flow Model for General Robot Control]({{ site.baseurl }}/zh/vla/pi0-a-vision-language-action-flow-model-for-general-robot-control-1945365620/) — arXiv:2410.24164 (Physical Intelligence, RSS 2025) — flow-matching 連續動作通用 policy
4. [GR00T N1: An Open Foundation Model for Generalist Humanoid Robots]({{ site.baseurl }}/zh/vla/gr00t-n1-an-open-foundation-model-for-generalist-humanoid-robots-1945393079/) — arXiv:2503.14734 (NVIDIA) — dual-system 人形基礎模型
5. [Helix: A Vision-Language-Action Model for Generalist Humanoid Control]({{ site.baseurl }}/zh/vla/helix-a-vision-language-action-model-for-generalist-humanoid-control-1945393112/) — Figure AI 官方部落格 — 首個支援人形上半身高頻全身控制的 VLA
6. [π*0.6: a VLA That Learns From Experience]({{ site.baseurl }}/zh/vla/pistar06-a-vla-that-learns-from-experience-1978234561/) — arXiv:2511.14759 (Physical Intelligence) — 首次系統性將 RL（Recap 方法）整合進 π 系列模型，讓 VLA 從真實世界自主經驗中持續自我改進
7. [π0.7: a Steerable Generalist Robotic Foundation Model with Emergent Capabilities]({{ site.baseurl }}/zh/vla/π07-a-steerable-generalist-robotic-foundation-model-with-emergent-capabilities-1951435101/) — arXiv:2604.15483 (Physical Intelligence) — 多樣情境條件訓練範式，以 episode metadata 與次目標圖片作為條件訊號，達成可組合泛化

---

## 每日 Paper 推送記錄

> 以下由排程任務自動新增，每篇新論文皆標註推送日期、所屬主題分類、來源（arXiv 當日新作 / top conference）。

### 推送日期: 2026-11-09

[FlowVLA: Enabling World Dynamics Understanding through Pluggable 3D Flow Learning]({{ site.baseurl }}/zh/vla/flowvla-enabling-world-dynamics-understanding-through-pluggable-3d-flow-2610161600/)

- **所屬主題**:Architecture Paradigms（架構典範：Autoregressive / Diffusion / Flow-matching / Hybrid）
- **來源**:arXiv:2610.16160,2026-10-12 發佈(本頁尚未記錄過,屬近期新作),已確認獲 CoRL 2026 接受(論文 metadata 明確標註「Accepted at Conference on Robot Learning (CoRL) 2026」),作者團隊來自韓國 Ajou University 與 Samsung Electronics
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受,且有 Samsung Electronics 產業實驗室參與;(2) 真正的方法論創新:首次提出完全訓練期專屬、零推論期開銷的重建引導 3D flow 監督框架,以點層級與 TCP 層級雙重 flow 設計將場景動態與機器人控制訊號耦合,不需任何額外 3D 感測器或推論期架構修改,並在兩種架構迥異的 VLA 骨幹(MLP-based Seer 與 flow-matching-based π0.5)上均驗證有效,填補了既有 3D-aware VLA 方法「需要額外感測器或改變推論架構」的方法論空白。
- **摘要**:論文指出現有 VLA 模型過度依賴 2D 影像-文字先驗,未能準確表徵與物理動作相關的 3D 世界動態,既有 3D-aware 方法雖整合深度圖或點雲改善空間理解,卻需要額外感測器與昂貴重訓練,且僅關注靜態幾何而忽略場景動態演變。作者提出 FlowVLA,以重建技術(VDPM)從 RGB 觀測中擷取時序一致的 3D 點軌跡,對齊至機器人基座座標系後定義為訓練期專屬的 3D flow 監督訊號,搭配基於運動幅度的 Top-K 關鍵點篩選,透過點層級 flow(預測任務關鍵 3D 點未來位移)與 TCP 層級 flow(聚合對齊機器人工具中心點軌跡)的雙層級設計,耦合場景動態與控制訊號,訓練後輔助頭即被捨棄、不影響推論效率。在 LIBERO benchmark 上,FlowVLA 於長 horizon 的 LIBERO-Long 子集上,Seer 骨幹成功率從 80.4% 提升至 87.8%,π0.5 骨幹從 92.4% 提升至 94.8%;在 LIBERO-Plus 零樣本穩健性評測中,Seer 平均成功率從 36.1% 提升至 41.1%。真實世界於 UR5e 平台上的七項任務評測顯示,Hang Cup 任務成功率從 46.7% 大幅提升至 86.7%,測試時視角變化下基線完全失敗(0%)而 FlowVLA 達到 46.7%。限制在於方法需要離線重建步驟產生 3D 點軌跡標籤,監督品質依賴重建模型準確度,且元件消融顯示多項設計選擇需共同作用才能達到最佳效果,並非單一關鍵機制主導。

### 推送日期: 2026-11-10

[FR-VLA: Implicit Force Reasoning VLA for Contact-Rich Manipulation]({{ site.baseurl }}/zh/vla/fr-vla-implicit-force-reasoning-vla-for-contact-rich-manipulation-2610259810/)

- **所屬主題**:Architecture Paradigms（架構典範：Autoregressive / Diffusion / Flow-matching / Hybrid）
- **來源**:arXiv:2610.25981,2026-10-19 發佈(本頁尚未記錄過,屬近期新作),已確認獲 CoRL 2026 接受(論文 metadata 明確標註「Accepted to CoRL 2026」),作者團隊來自新加坡南洋理工大學(NTU)電機與電子工程學院,以及新加坡科技研究局(A*STAR)旗下新加坡製造技術研究院(SIMTech)
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受;(2) 真正的方法論創新:首次將力覺整合進 VLA 這一問題明確框架為「模態接地」問題而非感測或融合問題,以可學習力查詢 token 從視覺語言情境推導出力許可訊號,明確分離「力相關性判斷」與「力表徵」兩個此前被混雜處理的子問題,並以消融實驗證實此分離設計相較單純依賴力矩幅度門控的簡化基線具有實質優勢(90% vs 70% 成功率),填補了既有力覺感知 VLA 僅提供「力曝光」而非「力接地」的方法論空白。暫未見大型科技公司直接參與(作者群為學術機構),未完全滿足標準二。
- **摘要**:論文指出將力覺整合進 VLA 模型,並非單純將力矩量測編碼為額外模態,而是要決定物理互動何時、以多強程度影響動作生成;既有力覺感知 VLA 通常透過固定路徑注入力訊號,未明確判斷該力訊號對當前動作是否相關。作者提出 FR-VLA,以可學習力查詢 token 構成 Implicit Force Reasoning Module,從視覺語言情境推斷出一個力許可訊號,再透過 Force Tokenizer(凍結 VQ-VAE 搭配 FiLM 調製)與 admission-conditioned attention 機制,將此訊號用於調節一條外部 tokenized 力路徑參與動作生成。在涵蓋 UR5e、UR3e 兩個機器人平台、五項接觸豐富操作任務的真實世界實驗中,FR-VLA 在全部六個評測階段皆取得最高成功率,平均成功率 58.3%,較最強基線高出 20.8 個百分點;消融實驗顯示移除力許可機制使成功率降至 35.0%,移除 Force Tokenizer 則降至 40.0%,驗證兩個元件的互補角色。限制在於精密操作中的細緻力條件修正動作仍具挑戰性,且評測任務數量與機器人平台多樣性相對有限,階段標籤產生亦依賴啟發式規則,其跨任務穩健性仍待更大規模驗證。

### 推送日期: 2026-11-11

[CoRE-VLA: Towards Scalable and Robust Vision-Language-Action Modeling via Conditional Routing of Experts]({{ site.baseurl }}/zh/vla/core-vla-towards-scalable-and-robust-vision-language-action-modeling-2607036930/)

- **所屬主題**:Architecture Paradigms（架構典範：Autoregressive / Diffusion / Flow-matching / Hybrid）
- **來源**:arXiv:2607.03693,2026 年 7 月 4 日首次發佈,2026 年 10 月 9 日修訂版(v2)確認獲 CoRL 2026(第十屆機器人學習會議)接受並發布 camera-ready 版本(論文 metadata 明確標註「Accepted at the 10th Conference on Robot Learning (CoRL 2026). Camera-ready version.」),本頁尚未記錄過,作者團隊來自浙江大學、上海創新研究院、復旦大學、南京大學與吉林大學
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受並發布 camera-ready 版本;(2) 真正的方法論創新:首次將 VLA 動作生成明確 formalize 為「情境條件化稀疏運算」,以感測器可用性與任務意圖兩種正交情境訊號雙重條件化 Mixture-of-Experts 式路由,解決既有稠密 VLA 架構在異質感測器組態與多樣任務負遷移兩個此前分開處理的問題上的耦合瓶頸,並透過消融實驗證實「以池化文字 token 作為任務意圖訊號」優於「直接以池化全模態表徵路由」,在 LIBERO 全部四個子套件取得當前最佳表現。暫未見大型科技公司直接參與(作者群為學術機構),未完全滿足標準二。
- **摘要**:論文指出 VLA 模型雖已推進通用機器人操作發展,但真實世界部署面臨機器人感測器組態的根本異質性——部分平台提供深度、觸覺或力回饋等輔助感知訊號,另一些則因硬體設計而缺乏這些感測器,即便感測器存在也可能運作中失效,而既有 VLA policy 透過共享稠密運算將動作生成與固定感測器組合緊密耦合,使其在感測器缺失時變得脆弱,也限制了跨多樣任務與長 horizon 行為的特化能力。作者提出 CoRE-VLA,以預訓練 VLM 編碼 RGB 觀測與語言指令,模態編碼器處理輔助深度輸入,flow-matching Action Diffusion Transformer 中的 CoRE 區塊先依池化文字 token 代表的任務意圖稀疏選擇最相關的動作側表徵,再依任務意圖與模態指示器條件化路由至通用專家或模態特化專家,使感測器可用性可直接閘控對應專家的啟用與否。在 LIBERO 全部四個子套件(Spatial、Object、Goal、Long)上,CoRE-VLA 以 98.7% 平均成功率超越 π0.5(96.9%)、OpenVLA-OFT(97.1%)、GR00T-N1.7(97.0%)等強力基線,在 LIBERO-Long 上優勢最為顯著(97.6% vs. 次佳 94.5%);在 RoboCasa GR1 Tabletop 與真實世界雙臂操作(Vegetables-Picking、Clothes-Folding、Fabric-Folding)評測中,CoRE-VLA 即便在推論時不使用輔助深度仍持續優於稠密 Action DiT 基線,啟用實體深度相機後表現進一步提升,且在 Fabric-Folding 可變形物體操作上展現強力零樣本泛化能力,搭配實體深度的版本在全部三項真實世界任務上均優於 π0.5 基線。限制在於論文僅以深度驗證輔助模態擴展性,觸覺、力回饋等其他模態的泛化效果尚待未來工作驗證,且兩階段訓練流程(先訓練稠密模型再轉換為專家路由架構)相較端到端訓練增加了工程複雜度。

### 推送日期: 2026-11-12

[Splat2Act: From Captured Scenes to Personalized VLA Manipulation]({{ site.baseurl }}/zh/vla/splat2act-from-captured-scenes-to-personalized-vla-manipulation-2611139450/)

- **所屬主題**:Data, Benchmarks & Simulation
- **來源**:arXiv:2610.13945,2026-10-09 發佈(本頁尚未記錄過,屬近期新作),已確認獲 CoRL 2026(第十屆機器人學習會議)camera-ready 版本接受,作者團隊來自喬治亞理工學院機器人與智慧型機械研究所(Institute for Robotics and Intelligent Machines, Georgia Institute of Technology)、Toyota Research Institute、Waymo LLC
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 camera-ready 接受,且有 Toyota Research Institute、Waymo 等大型產業實驗室參與;(2) 真正的方法論創新:首次將 real-to-sim-to-real 個人化管線從既有工作侷限的單一桌面場景,擴展至建築規模的室內環境,以全自動化(僅需一次手機掃描加物件影像)流程涵蓋 3D Gaussian Splatting 數位分身重建、容器自動發現、任務建構與特權模擬 oracle 示範生成,填補了既有 VLA 泛化研究較少觸及的「單一使用者真實環境部署個人化」這一實務落地問題的方法論空白,且真實世界驗證結果與模擬評測高度吻合。
- **摘要**:論文指出通用型操作 VLA policy(如 π0.5)在特定使用者的真實環境中部署時,開箱即用的拾取成功率趨近於零,而逐一為每位使用者收集真實示範的成本極其高昂。作者提出 Splat2Act,一套自動化 real-to-sim-to-real 管線,僅需一次 20-30 分鐘的手持手機掃描加上物件影像,即可建構涵蓋建築規模室內環境的 3D Gaussian Splatting 數位分身,自動發現桌面與非桌面容器,並以具特權的模擬 oracle 生成成功示範,全程不需真實機器人操作。應用於 101 個已掃描校園環境後,管線產出 852 個容器與超過 68,000 筆拾取示範,兩階段微調後的最強個人化 policy 在目標場景達到 62.5% 整體拾取成功率,部署於真實 Stretch 3 機器人後在 12 項任務子集上達到 63.9% 成功率,與模擬評測的 66.7% 高度吻合。限制在於真實世界驗證規模相對有限,且管線高度依賴物理模擬器對真實世界物理現象的擬真程度,sim-to-real 落差在更具挑戰性的操作任務上可能放大。
