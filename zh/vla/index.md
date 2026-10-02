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

- [EgoScale: Scaling Dexterous Manipulation with Diverse Egocentric Human Data]({{ site.baseurl }}/zh/vla/egoscale-scaling-dexterous-manipulation-with-diverse-egocentric-human-data-1955533518/) — arXiv:2602.16710（NVIDIA GEAR）— 驗證第一人稱人類影片資料規模與驗證損失間的對數線性 scaling law，可預測下游真實機器人表現
- [HuRo: Robotizing Human Videos for Scalable VLA Pretraining]({{ site.baseurl }}/zh/vla/huro-robotizing-human-videos-for-scalable-vla-pretraining-1964050194/) — arXiv:2609.10706（CoRL 2026）— 機器人化管線將異質人類影片轉換為機器人對齊格式，支援端到端 VLA 預訓練

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

### 推送日期: 2026-10-01

[IronMind: Scaling Humanoid Dexterous Manipulation via Camera-Space Ego-Centric Pretraining]({{ site.baseurl }}/zh/vla/ironmind-scaling-humanoid-dexterous-manipulation-via-camera-space-ego-centric-pretraining-1790838047/)

- **所屬主題**：Embodiment Diversity（人形 / 雙臂 / 四足 / 自駕）
- **來源**：arXiv:2609.39403，2026-09-30 當日新作，XPeng Robotics（小鵬機器人）World Model Team
- **選用理由**：同時滿足三項選取標準——(1) 大型產業實驗室出品，XPeng Robotics 為估值 63 億美元、正量產人形機器人 Iron 的公司；(2) 真正的方法論創新：以相機空間動作表示取代傳統人體重定向，從根本上解決第一人稱人類影片用於機器人預訓練的具身差距問題；(3) 提供罕見的完整規模化曲線（250h 至 10,000h）搭配真實人形機器人閉迴圈驗證，而非僅止於模擬。
- **摘要**：論文針對第一人稱人類影片訓練人形機器人靈巧操作時的兩大障礙——具身差距與資料品質問題——提出 IronMind。核心方法是用相機空間（而非軀幹座標系）作為人類與機器人共享的動作介面，搭配語意維度對齊與多階段資料策展管線，處理超過一萬小時混合語料。在萬小時預訓練規模下，真實機器人六項分佈外任務平均成功率達 55.0%，遠高於 5,000 小時以下的最高 11.7%，相機空間表示也明顯優於軀幹座標系基線（55.0% vs. 26.7%）。限制在於世界先驗監督在開迴圈指標為正、卻在真實機器人閉迴圈評測中造成效能下降，顯示該設計選擇的效益尚未完全釐清。

### 推送日期: 2026-10-02

[VLaRL: Augmenting Vision-Language-Action Models with Simulation-Trained Latent-Conditioned Residual RL]({{ site.baseurl }}/zh/vla/vlarl-augmenting-vision-language-action-models-with-simulation-trained-latent-c-1790912345/)

- **所屬主題**：Efficiency（壓縮 / 快速推論 / 資料效率訓練）—— 更精確地說是「VLA 後訓練精修」新興子領域
- **來源**：arXiv:2609.30868，2026-09-25 發佈（一週內新作），Microsoft Research（Namiko Saito、Kinam Kim、Heecheol Kim、Katsushi Ikeuchi、Yasuyuki Matsushita，合作機構涵蓋 KAIST、東京大學、大阪大學）
- **選用理由**：同時滿足選取標準中的兩項——(1) 大型科技公司出品，Microsoft Research 為公認的業界頂尖研究機構；(2) 真正的方法論創新：利用凍結 VLA 自身的視覺-語言 latent 表示作為模擬到真實遷移介面,而非傳統像素層級對應,並以輕量 mapper 模組明確處理 latent 空間本身仍存在的模擬-真實落差。目前尚未見正式頂會接受通知,暫以 Microsoft Research 出品與方法論創新作為收錄依據,未滿足標準一(頂會接受)。
- **摘要**：論文提出 VLaRL,讓凍結 VLA 的殘差 RL 完全在模擬環境中訓練並直接部署至真實機器人,無需任何真實世界 RL 或線上適應。核心方法是利用 VLA 內部的視覺-語言 latent 表示同時作為殘差控制的條件訊號與模擬-真實遷移介面,並學習一個輕量 mapper 模組將模擬 latent 對齊至真實 latent 分佈。在四項接觸豐富操作任務與兩個 VLA 骨幹（Flower、GR00T N1.7）構成的全部八種組合中,VLaRL 均提升真實世界成功率；消融實驗顯示移除 mapper 後,方塊推動與杯子疊放任務在全部 40 次真實機器人試驗中完全失敗,而完整版分別達 50.0% 與 70.0% 成功率,凸顯 latent 分佈對齊的關鍵作用。限制在於任務多樣性有限、且依賴「數位分身」場景複現能力,其資料收集成本與泛化範圍仍待更廣泛驗證。
