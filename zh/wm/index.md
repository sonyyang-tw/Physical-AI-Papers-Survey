---
layout: default
title: "World Model Papers"
permalink: /zh/wm/
---

# World Model Papers

本頁由自動化 Paper Survey Harness 維護，每日依照下方主題分類，挑選一篇當日新發布（arXiv）或近期重要的 top conference 論文，撰寫完整導讀並建立子頁面。

每篇論文標題皆為連結，點擊可進入該論文的完整 survey 子頁面（Abstract / Method / Result / Limitation / Related work / Conclusion）。

與 [VLA Papers]({{ site.baseurl }}/zh/vla/) 頁面互為姊妹主題：此處聚焦「預測/模擬優先」的 world model 研究（影片/latent 動態預測），VLA 頁面則聚焦「動作生成優先」的研究，兩者在 World Action Model 交界處有重疊，互相引用參照。

---

## 基礎/參考模型（不分主題，任何 survey 都應知道的里程碑）

1. [GAIA-1: A Generative World Model for Autonomous Driving]({{ site.baseurl }}/zh/wm/gaia-1-a-generative-world-model-for-autonomous-driving-1945473423/) — arXiv:2309.17080 (Wayve)
2. [Mastering Diverse Domains through World Models (DreamerV3)]({{ site.baseurl }}/zh/wm/mastering-diverse-domains-through-world-models-dreamerv3-1945767304/) — arXiv:2301.04104 / Nature 2025
3. [Genie 3: A New Frontier for World Models]({{ site.baseurl }}/zh/wm/genie-3-a-new-frontier-for-world-models-1945364950/) — DeepMind 官方部落格
4. [How Cosmos 3 Helps Physical AI Think Before It Acts]({{ site.baseurl }}/zh/wm/how-cosmos-3-helps-physical-ai-think-before-it-acts-1945539515/) — NVIDIA 官方技術報告
5. [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning]({{ site.baseurl }}/zh/wm/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planni-1945474552/) — arXiv:2506.09985 (Meta)
6. [GAIA-2: A Controllable Multi-View Generative World Model for Autonomous Driving]({{ site.baseurl }}/zh/wm/gaia-2-a-controllable-multi-view-generative-world-model-for-autonomous-driving-1945539764/) — arXiv:2503.20523 (Wayve)

---



## 基礎/參考模型（不分主題，任何 survey 都應知道的里程碑）

1. [GAIA-1: A Generative World Model for Autonomous Driving]({{ site.baseurl }}/zh/wm/gaia-1-a-generative-world-model-for-autonomous-driving-1945473423/) — arXiv:2309.17080 (Wayve)
2. [Mastering Diverse Domains through World Models (DreamerV3)]({{ site.baseurl }}/zh/wm/mastering-diverse-domains-through-world-models-dreamerv3-1945767304/) — arXiv:2301.04104 / Nature 2025
3. [Genie 3: A New Frontier for World Models]({{ site.baseurl }}/zh/wm/genie-3-a-new-frontier-for-world-models-1945364950/) — DeepMind 官方部落格
4. [How Cosmos 3 Helps Physical AI Think Before It Acts]({{ site.baseurl }}/zh/wm/how-cosmos-3-helps-physical-ai-think-before-it-acts-1945539515/) — NVIDIA 官方技術報告
5. [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning]({{ site.baseurl }}/zh/wm/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planni-1945474552/) — arXiv:2506.09985 (Meta)
6. [GAIA-2: A Controllable Multi-View Generative World Model for Autonomous Driving]({{ site.baseurl }}/zh/wm/gaia-2-a-controllable-multi-view-generative-world-model-for-autonomous-driving-1945539764/) — arXiv:2503.20523 (Wayve)

---

## 主題分類 (Topic Taxonomy)

### 1. Video-Generation World Models（通用/基礎，非機器人專用）

Scope：大規模文字/動作條件影片生成器，定位為通用「世界模擬器」（類遊戲、開放領域），非機器人專用。

代表論文：見上方基礎模型 Genie 3、Cosmos 3。

- [Rethinking Video Autoencoders for Interactive World Models (CADRE)]({{ site.baseurl }}/zh/wm/rethinking-video-autoencoders-for-interactive-world-models-2610301290/) — arXiv:2610.30129（Kyutai / UC Berkeley，2026-10-21 新作）— 開源因果 diffusion 表示 autoencoder 家族，系統性研究互動式 world model 應如何在時空壓縮上取捨，230 毫秒內反應、20 fps，構成延遲-品質前沿大部分最優點

### 2. Robot-Specific Action-Conditioned World Models（操作任務）

Scope：直接與機器人動作空間耦合的 world model，用於規劃、policy imagination 或 policy-in-the-loop rollout。

代表論文：

- [Ctrl-World: A Controllable Generative World Model for Robot Manipulation]({{ site.baseurl }}/zh/wm/ctrl-world-a-controllable-generative-world-model-for-robot-manipulation-1945391989/) — arXiv:2510.10125 (ICLR 2026) — 可控多視角生成式 world model，透過想像 rollout 提升 policy 成功率
- [τ0-WM: A Unified Video-Action World Model for Robotic Manipulation]({{ site.baseurl }}/zh/wm/τ0-wm-a-unified-video-action-world-model-for-robotic-manipulation-1945767449/) — arXiv:2606.01027 (AGIBOT) — 統一影片-動作 world model
- [WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation]({{ site.baseurl }}/zh/wm/weaver-better-faster-longer-an-effective-world-model-for-robotic-manipulation-1945767558/) — arXiv:2606.13672 — 多視角 world model (flow-matching)
- [VLAW: Iterative Co-Improvement of Vision-Language-Action Policy and World Model]({{ site.baseurl }}/zh/wm/vlaw-iterative-co-improvement-of-vision-language-action-policy-and-world-model-1945474219/) — arXiv:2602.12063 — VLA policy 與 world model 迭代共同改進
- [Pelican-Sim 1.0: A General World Model Simulator for Embodied Intelligence]({{ site.baseurl }}/zh/wm/pelican-sim-1-0-a-general-world-model-simulator-for-embodied-intelligence-1968596049/) — arXiv:2609.12036（AgiBot）— 統一 28 維動作值空間搭配 action-visual injection 與稀疏 MoE，處理跨具身 world model
- [GE-Act 2.0: Pretraining and Scaling a World-Action Model for Robotic Manipulation]({{ site.baseurl }}/zh/wm/ge-act-2-0-pretraining-and-scaling-a-world-action-model-for-robotic-manipulation-1972876063/) — arXiv:2609.05588（AgiBot）— 完全從零訓練 WAM（不繼承既有影片生成器），驗證 300 至 30,000 小時的資料規模化規律
- [GeniWorld: A Generalizable Interactive World Model for Robotic Manipulation via Visual Actions]({{ site.baseurl }}/zh/wm/geniworld-a-generalizable-interactive-world-model-for-robotic-manipulation-1978234598/) — arXiv:2608.06332（Tsinghua SIGS / Tencent Robotics X）— 以 URDF 渲染的視覺動作取代數值動作條件化，解耦具身運動學與環境動態，大幅提升零樣本 OOD 泛化
- [Do Robotic World Models Really Follow Actions? Diagnosing and Aligning Action-Conditioned Generation for Policy Learning]({{ site.baseurl }}/zh/wm/worldsync-diagnosing-and-aligning-action-conditioned-world-models-1791131205/) — arXiv:2608.24885（北京大學 / 北京人形機器人創新中心）— WorldEcho 診斷 benchmark 揭露 AC-WM 在非專家動作下的失效，WorldSync 以動作覆蓋擴增、表徵 grounding、介入效果對齊三軸線訓練提升忠實度

- [Spatially Aware World Action Model via Geometric Latent Diffusion]({{ site.baseurl }}/zh/wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/) — arXiv:2609.02531（Google DeepMind 參與）— 在不改動凍結 VAE tokenizer 前提下將深度模態注入 RGB World Action Model 擴散骨幹（原始分類為 World Action Models / Video-Action Joint Modeling，歸入本類別待覆核）
- [World Action Models are Zero-shot Policies (DreamZero)]({{ site.baseurl }}/zh/wm/world-action-models-are-zero-shot-policies-dreamzero-1951337490/) — arXiv:2602.15922（NVIDIA，RoboArena 排行榜第一）— 以影片擴散骨幹聯合建模未來影格與動作序列，統一動作生成與影片預測
- [DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos]({{ site.baseurl }}/zh/wm/dreamdojo-a-generalist-robot-world-model-from-large-scale-human-videos-1955665089/) — arXiv:2602.06949（NVIDIA GEAR）— 以連續潛在動作作為代理動作機制，於 44,000 小時第一人稱人類影片上預訓練 world model
- [Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning]({{ site.baseurl }}/zh/wm/cosmos-policy-fine-tuning-video-models-for-visuomotor-control-and-planning-1963892209/) — arXiv:2601.16163（ICLR 2026, NVIDIA/Stanford）— 潛在影格注入機制統一動作生成、未來狀態預測與價值評估於同一擴散序列
- [Astra: General Interactive World Model with Autoregressive Denoising]({{ site.baseurl }}/zh/wm/astra-general-interactive-world-model-with-autoregressive-denoising-1978567891/) — arXiv:2512.08931（ICLR 2026, 清華/快手 Kling）— 噪聲即遮罩策略與混合動作專家路由，以單一自迴歸去噪架構統一處理異質動作模態

- [Agentic World Action Models]({{ site.baseurl }}/zh/wm/agentic-world-action-models-2610301360/) — arXiv:2610.30136（UC Berkeley / NVIDIA / 賓夕法尼亞大學，2026-10-21 新作）— 以 Mixture-of-Transformers 聯合去噪程式碼、未來影片、機器人動作三流，首次將程式碼即規劃整合進 world action model 的生成過程

- [RoboJEPA: Scaling Robotic Latent World Models]({{ site.baseurl }}/zh/wm/robojepa-scaling-robotic-latent-world-models-2610105150/) — arXiv:2610.10515（Meta FAIR，2026-10-07 新作）— 首次為多具身機器人潛在世界模型建立嚴謹 scaling law，8B 參數為目前最大 JEPA predictor

- [RynnWorld-Latent: A Cross-Embodiment World Model Conditioned on Universal Latent Actions]({{ site.baseurl }}/zh/wm/rynnworld-latent-a-cross-embodiment-world-model-conditioned-on-universal-2610367910/) — arXiv:2610.36791（DAMO Academy, Alibaba Group，2026-10-27 新作）— 以 RynnLAM 3D 接地 latent action 作為跨具身共享條件介面，支援數位遙操作與 latent action 合成雙路線資料生成引擎

- [AnyWorld: Factorized Egocentric World Models for Cross-Embodiment Generalization]({{ site.baseurl }}/zh/wm/anyworld-factorized-egocentric-world-models-for-cross-embodiment-2608292420/) — arXiv:2608.29242（CoRL 2026，XPeng Robotics / 南洋理工大學 / A*STAR）— 將人類第一人稱互動分解為動作/相機/具身三因子，無需配對人類-機器人示範即可重組出多樣機器人原生 rollout，真實 IRON 人形機器人抓取成功率從 20.0% 提升至 55.0%

- [AuroraWorld: Structured 4D World Modeling for Exo-to-Ego Video Generation in Robot Manipulation]({{ site.baseurl }}/zh/wm/auroraworld-structured-4d-world-modeling-for-exo-to-ego-video-generation-2611001770/) — arXiv:2611.00177（香港科技大學(廣州) / 新南威爾斯大學，2026-10-30 新作）— 將 exo-to-ego 影片合成重新形式化為結構化 4D 具身世界表徵推論，以空間/時間/動作三互補元件作為生成先驗，彌補機器人第一人稱資料稀缺的瓶頸

- [DepthWorld: 3D World Model for Robot Manipulation]({{ site.baseurl }}/zh/wm/depthworld-3d-world-model-for-robot-manipulation-2610087800/) — arXiv:2610.08780（CoRL 2026，Czech Technical University in Prague / CIIRC）— 以校準管線（DROID-3D）從既有遙操作資料中挖掘密集 3D 監督，搭配空間潛在拼貼在不破壞預訓練先驗下聯合預測多視角 RGB 與度量深度，深度監督使 RGB 預測提升 +1.48 dB PSNR

- [GR00T 2: Scaling Robot Foundation Models for Generalization, Dexterity, and Adaptation]({{ site.baseurl }}/zh/wm/gr00t-2-scaling-robot-foundation-models-for-generalization-dexterity-and-adaptation-2611090001/) — NVIDIA GEAR 技術白皮書，2026-11-09 CoRL 2026 正式發表 — 新一代 world-action model，單一 2B 參數 checkpoint 涵蓋夾爪、靈巧手、人形三種具身，X-Adaptability 使人類示範技能可零遠端操作遷移至新機器人，Dexter-50 零樣本成功率 40%、5 次示範提升至 95%

### 3. World Models for Autonomous Driving

Scope：用於駕駛場景生成、模擬、閉環評測與規劃的影片/latent world model。

代表論文：

- [DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment]({{ site.baseurl }}/zh/wm/driverse-navigation-world-model-for-driving-simulation-via-multimodal-trajectory-1945539343/) — arXiv:2504.18576 (ACM MM 2025)
- [End-to-End Driving with Online Trajectory Evaluation via BEV World Model (WoTE)]({{ site.baseurl }}/zh/wm/end-to-end-driving-with-online-trajectory-evaluation-via-bev-world-model-1945392255/) — arXiv:2504.01941 (ICCV 2025)
- [DreamerAD: Efficient Reinforcement Learning via Latent World Model for Autonomous Driving]({{ site.baseurl }}/zh/wm/dreamerad-efficient-reinforcement-learning-via-latent-world-model-for-autonomous-1945365119/) — arXiv:2603.24587
- [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)]({{ site.baseurl }}/zh/wm/other-vehicle-trajectories-are-also-needed-a-driving-world-model-unifies-ego-oth-1945392511/) — arXiv:2503.09215
- [Toward Physically Consistent Driving Video World Models under Challenging Trajectories (PhyGenesis)]({{ site.baseurl }}/zh/wm/toward-physically-consistent-driving-video-world-models-under-challenging-traje-1985672345/) — arXiv:2603.24506 — 物理條件生成器修正反事實/違反物理軌跡，提升碰撞等極端情境生成一致性

- [NVIDIA OmniDreams: Real-Time Generative World Model for Closed-Loop Autonomous Vehicle Simulation]({{ site.baseurl }}/zh/wm/nvidia-omnidreams-real-time-generative-world-model-for-closed-loop-autonomous-ve-1982345698/) — arXiv:2606.03159（NVIDIA）— Self Forcing 蒸餾與漸進式長 context 教師策略，達成單視角 68 FPS、多視角 105 FPS 即時閉環模擬

- [Percept-WAM: Perception-Enhanced World-Awareness-Action Model for Robust End-to-End Autonomous Driving]({{ site.baseurl }}/zh/wm/percept-wam-perception-enhanced-world-awareness-action-model-for-robust-end-1790912567/) — arXiv:2511.19221（CVPR 2026，Yinwang Intelligent Technology／華為智駕子公司＋復旦大學）— 首度在單一 VLM 內隱式整合 2D/3D 場景理解，以 World-PV/World-BEV token 取代問答式空間推理，感知與規劃基準雙重驗證

- [UniFuture: A 4D Driving World Model for Future Generation and Perception]({{ site.baseurl }}/zh/wm/unifuture-a-4d-driving-world-model-for-future-generation-and-perception-1996734598/) — arXiv:2503.13587（ICRA 2026）— Dual-Latent Sharing 將影像與深度映射至共享 latent 空間，Multi-scale Latent Interaction 強制雙向時空一致性，同時提升未來生成與幾何感知表現

### 4. Model-Based RL / Latent Dynamics for Control

Scope：經典 model-based RL，用學習到的 latent 動態模型做規劃/想像式 policy 學習（不一定是 pixel 層級，與機器人無關）。

代表論文：

- DreamerV3（見上方基礎模型）
- [Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination]({{ site.baseurl }}/zh/wm/dream-mpc-gradient-based-model-predictive-control-with-latent-imagination-1945365146/) — arXiv:2605.04568 (ICML 2026)

- [SuperMimic: Scaling Humanoid Whole-Body Control with One Differentiable World Model]({{ site.baseurl }}/zh/wm/supermimic-scaling-humanoid-whole-body-control-with-one-differentiable-world-mod-2610284800/) — arXiv:2610.28480（CoRL 2026 Oral，UC Berkeley）— 可微分 world model 與 policy 共同訓練，BPTT 解析梯度取代 model-free RL，GPU 工時降低超過 1000 倍

- [How to Learn from What a Human Would Avoid? Intervention-Aware World Models with Real-World RL for Dexterous Manipulation (WHIRL)]({{ site.baseurl }}/zh/wm/whirl-intervention-aware-world-models-with-real-world-rl-for-dexterous-manipulation-2611139451/) — arXiv:2609.06009（CoRL 2026，HKUST-GZ / Italian Institute of Technology / 浙江大學）— 將人類介入訊號轉化為逐狀態介入機率預測頭，作為 actor 端風險塑形項主動規避危險區域，真實 LEAP Hand 達 96.7% 成功率並降低介入負擔最多 84%

### 5. World Model Evaluation & Physical-Reasoning Benchmarks

Scope：評估 world model 物理一致性、可控性、具身實用性的 benchmark/診斷工具。

代表論文：

- [PhyGround: Benchmarking Physical Reasoning in Generative World Models]({{ site.baseurl }}/zh/wm/phyground-benchmarking-physical-reasoning-in-generative-world-models-1945539592/) — arXiv:2605.10806
- [WorldBench: Benchmarking Physical Understanding of World Models by Isolating Physics Concepts]({{ site.baseurl }}/zh/wm/worldbench-benchmarking-physical-understanding-of-world-models-by-isolating-phys-1945392538/) — arXiv:2601.21282
- [RoboWM-Bench: A Benchmark for Evaluating World Models in Robotic Manipulation]({{ site.baseurl }}/zh/wm/robowm-bench-a-benchmark-for-evaluating-world-models-in-robotic-manipulation-1945365171/) — arXiv:2604.19092
- [WorldOlympiad: Can Your World Model Survive a Triathlon?]({{ site.baseurl }}/zh/wm/worldolympiad-can-your-world-model-survive-a-triathlon-1945767203/) — arXiv:2606.11129
- [iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework]({{ site.baseurl }}/zh/wm/iworld-bench-a-benchmark-for-interactive-world-models-with-a-unified-action-gene-1945539121/) — arXiv:2605.03941

- [Inference-time Physics Alignment of Video Generative Models with Latent World Models]({{ site.baseurl }}/zh/wm/inference-time-physics-alignment-of-video-generative-models-with-latent-world-mo-1959634541/) — arXiv:2601.10553（Meta FAIR, ICCV 2025 PhysicsIQ Challenge 冠軍）— 以 V-JEPA 2 作為獎勵訊號，於推論階段引導候選去噪軌跡以提升物理合理性
- [Evaluating Gemini Robotics Policies in a Veo World Simulator]({{ site.baseurl }}/zh/wm/evaluating-gemini-robotics-policies-in-a-veo-world-simulator-1790838179/) — arXiv:2512.10675（Google DeepMind, Gemini Robotics Team, 2025-12-11 發佈 / 2026-01-06 修訂）— 以 Veo 2 影片基礎模型搭配生成式場景編輯，建立涵蓋分佈內評測、分佈外泛化、安全紅隊測試的全光譜政策評測系統，1600+ 真實評測驗證預測保真度

### 6. World Models as Data Engines / Simulators for Robot Learning

Scope：明確用 world model 生成合成訓練資料、擴增模擬、縮小 sim-to-real 落差。

代表論文：

- [WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL]({{ site.baseurl }}/zh/wm/wovr-world-models-as-reliable-simulators-for-post-training-vla-policies-with-rl-1945473965/) — arXiv:2602.13977
- [Interactive World Simulator for Robot Policy Training and Evaluation]({{ site.baseurl }}/zh/wm/interactive-world-simulator-for-robot-policy-training-and-evaluation-1945767226/) — arXiv:2603.08546
- [Targeting World Models to Compromise Robot Learning Pipelines]({{ site.baseurl }}/zh/wm/targeting-world-models-to-compromise-robot-learning-pipelines-1945473989/) — arXiv:2606.09499 — world model 資料下毒的對抗式/安全性新興子主題
- [Cosmos Predict 2.5 & Transfer 2.5: Evolving the World Foundation Models for Physical AI]({{ site.baseurl }}/zh/wm/cosmos-predict-25-and-transfer-25-evolving-the-world-foundation-models-for-physi-1945767248/) — NVIDIA 官方技術報告
- [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations]({{ site.baseurl }}/zh/wm/mimicgen-a-data-generation-system-for-scalable-robot-learning-using-human-demons-1945473767/) — arXiv:2310.17596 (CoRL 2023, baseline)
- [Dreamitate: Real-World Visuomotor Policy Learning via Video Generation]({{ site.baseurl }}/zh/wm/dreamitate-real-world-visuomotor-policy-learning-via-video-generation-1945364542/) — arXiv:2406.16862 (CoRL 2024, baseline)

- [Training Controllable World Models via Action Influence Maximization]({{ site.baseurl }}/zh/wm/training-controllable-world-models-via-action-influence-maximization-2610273870/) — arXiv:2610.27387（CoRL 2026，Princeton University / Columbia University）— 證明資料集條件互資訊是模型可解釋動作資訊量的上界，提出主動資料收集演算法 AIM，達成 85 倍資料效率提升

### 7. World Models Surveys & Taxonomy Papers（meta-tracking 主題）

Scope：定期重新定義此領域的綜述論文。

代表論文：

- [World Model for Robot Learning: A Comprehensive Survey]({{ site.baseurl }}/zh/wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/) — arXiv:2605.00080
- [World Models for Robotic Manipulation: A Survey]({{ site.baseurl }}/zh/wm/world-models-for-robotic-manipulation-a-survey-1945391939/) — arXiv:2606.00113
- [A Step Toward World Models: A Survey on Robotic Manipulation]({{ site.baseurl }}/zh/wm/a-step-toward-world-models-a-survey-on-robotic-manipulation-1945392081/) — arXiv:2511.02097
- [From World Models to World Action Models: A Concise Tutorial for Robotics]({{ site.baseurl }}/zh/wm/from-world-models-to-world-action-models-a-concise-tutorial-for-robotics-1945539286/) — arXiv:2607.00836 — 銜接 VLA/WAM 姊妹主題
- [Aether: Geometric-Aware Unified World Modeling]({{ site.baseurl }}/zh/wm/aether-geometric-aware-unified-world-modeling-1945539008/) — arXiv:2503.18945 (ICCV 2025 Outstanding Paper)

---

## 相關 NeurIPS 2026 Workshop（可作為推播來源）

- "Robot Learning with World Models" — robowm-ws.github.io（Sydney, Dec 2026，camera-ready 11/30）
- "World Models in Physical AI" — worldmodels-physicalai.com（Sydney, Dec 2026，camera-ready 11/30）

## 與 VLA 主題的邊界

τ0-WM、VLAW、WoVR 等論文位於「world action model」交界處，歸類於本頁第2/6類，但同時與 [VLA Papers]({{ site.baseurl }}/zh/vla/) 頁面第7類「World Models Integration」重疊。

---

## 每日 Paper 推送記錄

> 以下由排程任務自動新增，每篇新論文皆標註推送日期、所屬主題分類、來源（arXiv 當日新作 / top conference）。

### 推送日期: 2026-10-27

[Agentic World Action Models]({{ site.baseurl }}/zh/wm/agentic-world-action-models-2610301360/)

- **所屬主題**:Robot-Specific Action-Conditioned World Models（操作任務）
- **來源**:arXiv:2610.30136,2026-10-21 發佈(本頁尚未記錄過,屬近期新作),UC Berkeley / NVIDIA / 賓夕法尼亞大學聯合發表(作者群涵蓋 Ken Goldberg、Trevor Darrell、Linxi "Jim" Fan、Yuke Zhu、Guanzhi Wang 等業界與學界知名研究者)
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 大型產業實驗室與頂尖學術機構聯合出品,NVIDIA 與 UC Berkeley 在機器人學習領域具高度影響力;(2) 真正的方法論創新:首次將「程式碼即規劃」直接整合進 world action model 的聯合去噪過程,以 Mixture-of-Transformers 架構同時生成程式碼、未來影片、機器人動作三個耦合的生成流,填補了既有 WAM 缺乏技能組合結構、既有 agentic robotics 缺乏物理動態 grounding 的方法論空白。目前尚未見正式頂會接受通知,暫以產業/學界聯合出品與方法論創新作為收錄依據,未滿足標準一(頂會接受)。
- **摘要**:論文指出近期 world action model 提供視覺前瞻與未來預測,卻缺乏可組合技能重複使用的機制;agentic robotics 提供程式化技能結構,卻往往缺乏物理動態的預測性 grounding。作者提出 AW-0,一套整合程式碼規劃與聯合影片/動作預測的 agentic world action model 框架,以統一 Mixture-of-Transformers 架構同時建模程式碼、未來影片、機器人動作三個耦合生成流,程式碼專家以 LLaDA 風格遮罩擴散生成參數化技能常式,影片與動作專家則以 continuous flow matching 生成未來視覺狀態與低階動作。作者並提出自動化標註管線,結合 Gemini 3.1 Pro 撰寫技能程式、Claude Opus 4.8 擔任協調者蒸餾技能庫,為機器人與人類影片標註對齊程式。在 RoboTwin 2.0 上,AW-0 平均成功率達 50.7%,優於 π0.5(41.3%)、DreamZero(25.6%)等基線;混合執行模式在隨機化設定下達到 29.2% 成功率,為所有方法最高。在 8 項真實世界雙臂操作任務上同樣展現效能與語言遵循能力的提升。限制在於程式 grounding 依賴標註準確性與技能覆蓋範圍,混合執行雖提升分佈外穩健性卻會降低乾淨設定下的效能,且系統目前不會從自身互動中線上學習。

### 推送日期: 2026-10-28

[SuperMimic: Scaling Humanoid Whole-Body Control with One Differentiable World Model]({{ site.baseurl }}/zh/wm/supermimic-scaling-humanoid-whole-body-control-with-one-differentiable-world-mod-2610284800/)

- **所屬主題**:Model-Based RL / Latent Dynamics for Control
- **來源**:arXiv:2610.28480,2026-10-20 發佈(本頁尚未記錄過,屬近期新作),已確認獲 CoRL 2026 接受為 Oral,UC Berkeley(作者群含 Pieter Abbeel、Koushil Sreenath 等業界與學界知名研究者)
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受為 Oral(見論文 metadata「Accepted at CoRL 2026 (Oral)」與項目頁 supermimic.github.io),且出自 UC Berkeley 頂尖機器人學習團隊;(2) 真正的方法論創新:首次以單一可微分 world model 分攤人形全身動作追蹤的跨動作學習成本,搭配 BPTT 解析策略梯度取代傳統 model-free RL 的高變異梯度估計,將訓練算力需求從叢集級(128 顆 GPU、7 天)降低至單一 GPU、數小時量級,GPU 工時降低超過 1000 倍,並完成真實 Unitree G1 機器人零樣本遷移驗證。
- **摘要**:論文指出追蹤大規模人類動作資料集是實現通用人形全身控制的主流途徑,但既有 model-free RL 管線規模化成本高昂,要嘛透過有損蒸餾合併動作專家、要嘛暴力投入叢集級算力。作者提出 SuperMimic,以單一可微分 world model(從標準剛體模擬器 MuJoCo Warp 的紀錄軌跡擬合而成)分攤所有動作共享的動態特性學習,world model 與追蹤 policy 在同一迴圈中共同訓練,透過對短想像 rollout 的 BPTT 取得解析策略梯度。在單一 H100 GPU 上訓練 3 小時,SuperMimic 即超越 SONIC 基線(128 顆 L40 GPU 訓練 7 天)的正規化回報,GPU 工時降低超過 1000 倍,在 129,514 個 benchmark 動作中僅失敗 25 個(基線失敗 179 個,含全部空翻與側滾翻);以兩顆 GPU 訓練 9.8 小時後達到零失敗。訓練出的 policy 可零樣本遷移至真實 Unitree G1,完成側滾翻、180 度空翻等高難度特技動作。限制在於 benchmark 動作同時是訓練動作,失敗率數字衡量覆蓋率而非對全新動作的泛化能力,且 world model 需與 policy 同步每次迭代更新,其擬合品質是整體訓練流程的潛在瓶頸。

### 推送日期: 2026-10-29

[RynnWorld-Latent: A Cross-Embodiment World Model Conditioned on Universal Latent Actions]({{ site.baseurl }}/zh/wm/rynnworld-latent-a-cross-embodiment-world-model-conditioned-on-universal-2610367910/)

- **所屬主題**:Robot-Specific Action-Conditioned World Models（操作任務）
- **來源**:arXiv:2610.36791,2026-10-27 發佈(本頁尚未記錄過,屬近期新作),DAMO Academy(阿里巴巴集團)、Hupan Lab、Hong Kong Embodied AI Lab、香港中文大學(CUHK)聯合發表
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 大型產業實驗室出品,DAMO Academy 為阿里巴巴集團旗下頂尖研究機構,與同日收錄於 VLA 頁面的姊妹論文 RynnVLA-Latent 共享同一組作者與核心技術基礎;(2) 真正的方法論創新:首次將 3D 接地 latent action(RynnLAM)同時用於 policy 預訓練監督與 world model 條件化兩端,並明確以「資料生成引擎」定位支援數位遙操作與 latent action 合成兩條資料生成路線,在 23 個資料集、約 5.535 億影格規模上完成預訓練,並於兩個真實機器人平台(Marvin-WUJI、Astribot-S1)完成閉環驗證。目前尚未見正式頂會接受通知,暫以產業實驗室出品與方法論創新作為收錄依據,未滿足標準一(頂會接受)。
- **摘要**:論文指出從異質互動影片學習可控世界動態極具挑戰,因為不同機器人具身使用互不相容的動作空間,人類影片又缺乏原生控制標籤。作者提出 RynnWorld-Latent,使用姊妹論文 RynnVLA-Latent 提出的 RynnLAM 3D 接地 latent action 作為共享條件介面,結合全域 action token 與恆等初始化的局部條件路徑,將動作與未來影片 latent 對齊,在 23 個資料集約 5.535 億影格上預訓練後透過後訓練適配至目標機器人。框架支援數位遙操作與 latent action 合成兩種資料生成路線,合成資料 mid-training 將 π₀ 在 LIBERO-Plus 上的成功率從 53.6% 提升至 79.4%,兩種生成路線也都在 Marvin-WUJI 與 Astribot-S1 兩個真實機器人平台的四項任務上提升了閉環成功率,例如 π₀.₅ 的 Steak-Serving 任務透過合成資料 mid-training 從 40.00% 提升至 60.00%。限制在於 latent action 可能同時編碼相機運動與操作資訊,定性動作跟隨與影像預測指標不足以確立物理正確性,真實世界成功率僅基於每任務 35 次試驗,且部分任務上 Real + Digital Teleop 甚至優於使用 RynnWorld 生成資料的設定,顯示合成資料品質在特定具身/任務組合下仍有改進空間。

### 推送日期: 2026-11-02

[Rethinking Video Autoencoders for Interactive World Models (CADRE)]({{ site.baseurl }}/zh/wm/rethinking-video-autoencoders-for-interactive-world-models-2610301290/)

- **所屬主題**:Video-Generation World Models（通用/基礎，非機器人專用）
- **來源**:arXiv:2610.30129,2026-10-21 發佈(本頁尚未記錄過,屬近期新作),Kyutai(法國知名 AI 實驗室)、LIGM/ENPC/IP Paris/CNRS/UGE、UC Berkeley 聯合發表
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 大型產業實驗室出品,Kyutai 為具國際知名度的法國 AI 實驗室,並與 UC Berkeley 研究者合作;(2) 真正的方法論創新:首次將「video autoencoder 的時空壓縮設計」本身作為可系統性研究的自由變數,開源一整個涵蓋七種壓縮程度、僅瓶頸層不同、其餘訓練 recipe 完全共享的 causal diffusion representation autoencoder 家族,使研究者得以公平分離 autoencoder 選擇對 world model 延遲與品質的獨立影響,填補既有文獻中「autoencoder 選擇被視為既定事實而非研究對象」的方法論空白,並歸納出四項可直接指導業界壓縮策略選擇的具體準則。目前尚未見正式頂會接受通知,暫以產業實驗室出品與方法論創新作為收錄依據,未滿足標準一(頂會接受)。
- **摘要**:論文指出互動式 video world model 的每影格成本、動作延遲與生成品質皆繼承自其 video autoencoder,但既有 world model 普遍沿用 text-to-video 生成模型的 autoencoder,這類 autoencoder 為離線生成設計且訓練資料與程式碼未公開,無法在其他壓縮程度下重新訓練以系統性研究。作者提出 CADRE,一套開源的 causal diffusion representation autoencoder 家族,家族成員共享凍結 DINOv3 特徵提取器與自我蒸餾至一到數步的 diffusion 解碼器,僅在小型瓶頸層的時空壓縮程度上有所差異。作者在操作與導航兩大領域、各兩個環境上,於每個壓縮點訓練相同的 1.2B 參數 world model,系統性比較延遲-品質權衡。CADRE 在單張 H100 上達 20 fps、反應延遲低於 230 毫秒,於 48 項與 Wan 2.2、LTX-2、Cosmos 等既有 autoencoder 的比較中,42 項同時更快且品質更佳。研究並歸納四項發現:強壓縮下 diffusion 解碼器比感知式迴歸更清晰;機器人操作中時間壓縮放在 autoencoder 比放在 world model 更有效;操作與導航場景需要相反的壓縮策略(靜止相機偏好時間壓縮、移動相機偏好空間壓縮);靜止相機下粗糙空間 token 對動作品質與動作遵循的傷害遠大於對影像品質的傷害。限制在於每個 world model 僅針對單一環境訓練,這些準則能否延伸至通用型 world model 與 policy 訓練/規劃任務仍是open 問題,且操作資料多採用靜止相機,移動式手腕相機場景的壓縮策略尚未直接驗證。

### 推送日期: 2026-11-03

[AnyWorld: Factorized Egocentric World Models for Cross-Embodiment Generalization]({{ site.baseurl }}/zh/wm/anyworld-factorized-egocentric-world-models-for-cross-embodiment-2608292420/)

- **所屬主題**:Robot-Specific Action-Conditioned World Models（操作任務）
- **來源**:arXiv:2608.29242,2026 年 8 月 29 日首次發佈,2026 年 9 月 1 日修訂版(v2),專案頁已確認獲 CoRL 2026 接受,本頁尚未記錄過,作者團隊來自南洋理工大學、新加坡 A*STAR 高等智能計算研究所、XPENG Robotics、浙江大學、香港中文大學聯合發表
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 大型產業實驗室出品,XPENG Robotics 為具國際知名度的人形機器人廠商,並與南洋理工大學、A*STAR、浙江大學等學術機構合作,專案頁確認獲 CoRL 2026 接受;(2) 真正的方法論創新:首次提出統一的動作-相機-具身分解介面,將單一未配對的人類第一人稱互動視為可重複使用的種子,重組為多樣機器人領域的視覺經驗,並透過受控能力介入實驗(而非僅報告整體平均增益)嚴謹驗證「視覺重組」與「動作校準」兩者缺一不可——純動作層級的反事實配對無法可靠學習語言接地的空間目標選擇,填補了既有人類影片利用方法「不會從無配對人類互動直接渲染完整機器人原生影片」的方法論空白。
- **摘要**:論文指出大規模收集接觸豐富的機器人操作經驗仍是可泛化操作學習的主要瓶頸,人類第一人稱影片雖提供豐富物理互動,但每段錄影僅捕捉特定身體、相機軌跡、環境下的單一經驗切片。作者提出 AnyWorld,將互動分解為動作(渲染骨架控制影片)、相機(Plücker 光線嵌入)、具身(初始影格+文字標籤)三個條件,以隱擴散影片模型實現,訓練分為大規模人類互動(EgoDex)預訓練與無配對混合具身微調兩階段,無需任何人類-機器人影格層級對應關係。可控性評測顯示 AnyWorld 在 ActionAlign、CameraAlign、EmbodAcc 三項指標上全面優於 WAN Fun-Control 與 Cosmos-Predict2.5 基線,平均可控性分數達 0.778,同時維持具競爭力的 VBench 影片品質。在下游 VLA 適配任務上,加入 AnyWorld 生成資料後,RoboCasa GR1 的 18 項任務成功率從 49.8% 提升至 54.6%,真實 IRON 機器人 20 次抓取試驗成功率從 20.0% 大幅提升至 55.0%,巨集平均增益達 19.9 個百分點,受控能力介入實驗證實視覺重組與動作校準兩者缺一不可。

### 推送日期: 2026-11-09

[DepthWorld: 3D World Model for Robot Manipulation]({{ site.baseurl }}/zh/wm/depthworld-3d-world-model-for-robot-manipulation-2610087800/)

- **所屬主題**:Robot-Specific Action-Conditioned World Models（操作任務）
- **來源**:arXiv:2610.08780,2026-10-06 發佈(本頁尚未記錄過,屬近期新作),已確認獲 CoRL 2026 接受(論文 metadata 明確標註「Accepted at the Conference on Robot Learning (CoRL) 2026」,專案頁 jaibardhan.com/depthworld 亦確認),作者團隊來自捷克技術大學布拉格分校(Czech Technical University in Prague)旗下 Czech Institute of Informatics, Robotics and Cybernetics(CIIRC)
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受;(2) 真正的方法論創新:首次提出結合學習式立體深度與跨 episode 聯合因子圖的機器人接地校準管線(DROID-3D),搭配不需破壞性重新初始化即可注入深度監督的空間潛在拼貼架構,同時解決「大規模 3D 監督從何而來」與「如何在不破壞預訓練影片先驗前提下吸收監督」兩個前後銜接的問題,填補既有影片 world model 僅以 RGB 訓練、rollout 無法組成一致 3D 世界的方法論空白。暫未見大型科技公司直接參與(作者群為學術機構),未完全滿足標準二。
- **摘要**:論文指出現有以影片為基礎的 world model 僅以 RGB 訓練,rollout 雖逐影格視覺合理卻無法組成一致的 3D 世界,直接加入幾何監督的「自然解法」因機器人遙操作資料集幾何標註品質不足、且既有加入空間模態的架構方式（VAE 通道擴展、雙分支 U-Net）需要破壞性重新初始化而損害預訓練先驗,無法直接套用。作者提出兩階段校準管線:Stage 1 以學習式全局匹配網路(S²M²)恢復逐視角度量深度並以 RoMa-v2 對應關係驅動 bundle adjustment 強制多視角一致;Stage 2 將 URDF 渲染至各外部視角錨定機器人基座座標系,建構橫跨同一機器人所有 episode 的聯合因子圖以分離逐場景外部參數雜訊與共享運動學參數,應用於 DROID 資料集後產出涵蓋 71,100 個 episode、28 台機器人的 DROID-3D 校準資料集。接著訓練 DepthWorld,透過空間潛在拼貼將多視角 RGB 與深度獨立編碼進同一潛在網格供單一 U-Net 聯合去噪,保持預訓練 SVD VAE 不變,並以 DPT 點圖頭對機器人座標系 3D 點圖進行細粒度幾何監督。校準精度上,相較 PointWorld 式逐場景精修基線,外部相機重投影誤差中位數從 5.84 像素降至 0.25 像素,且消除基線約 18% 的收斂失敗率;世界模型預測品質上,深度監督在相同訓練預算下使外部視角 RGB 預測提升 +1.48 dB PSNR、手腕視角提升 +1.02 dB PSNR,同時產生準確度量深度。限制在於校準管線目前僅於 DROID 資料集驗證,且手腕視角的整體預測品質仍明顯遜於外部視角,為瓶頸所在。

### 推送日期: 2026-11-10

[Training Controllable World Models via Action Influence Maximization]({{ site.baseurl }}/zh/wm/training-controllable-world-models-via-action-influence-maximization-2610273870/)

- **所屬主題**:World Models as Data Engines / Simulators for Robot Learning
- **來源**:arXiv:2610.27387,2026-10-19 發佈(本頁尚未記錄過,屬近期新作),論文 metadata 明確標註「31 pages, 13 figures, CoRL 2026」確認獲 CoRL 2026 接受,作者團隊來自美國普林斯頓大學(Princeton University)與哥倫比亞大學(Columbia University),成員包含 Dhruv Shah、Benjamin Eysenbach、Jaime Fernández Fisac 等研究者
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受,出自普林斯頓大學 PRISM Lab 等頂尖學術團隊;(2) 真正的方法論創新:首次以貝氏法則與 KL 散度非負性,嚴謹證明資料集條件互資訊是任何以該資料訓練出的 world model 所能表現動作影響力的理論上界,將「world model 能力受限於資料而非模型容量」這一此前僅為直覺猜測的假說,轉化為具理論基礎且可操作的主動資料收集演算法 AIM,並在像素層級機器人操作任務上實證達成 85 倍資料效率提升,填補了既有「優化資料收集分佈以改善 world model 可控性」這一子領域相對未被充分探索的方法論空白。
- **摘要**:論文指出以成功、目標導向示範訓練而成的動作條件式影片生成式模型,往往會忽略所下達的動作指令,無論實際要求為何都生成一個看似合理、近乎專家水準的未來畫面,作者將此失效追溯至訓練資料缺乏足夠的「動作影響力」——專家示範的動作分佈狹窄,使下一狀態的預測無需真正關注動作即可完成,為任何模型容量都無法突破的可控性設下低上限。作者首先證明資料集條件互資訊是模型可解釋動作資訊量的理論上界,並據此提出 Action Influence Maximization(AIM),一套主動資料收集演算法,透過資料密度估計優化一個結合「動作資訊性轉變」與「參考狀態覆蓋率」的內在獎勵,聚焦資料收集於資料集解釋最差的狀態-動作配對。在像素層級機器人操作任務中,AIM 是唯一能持續改善可控性的方法:在 3000 筆專家示範基礎上額外加入 500 筆主動收集的 episode,即可匹配以 30 萬筆專家 episode 訓練出的 world model 在末端執行器可控性上的表現,相當於 85 倍的資料量縮減。限制在於重新訓練多個學習式密度獎勵模型帶來的實作複雜度與運算強度較高,序列式強化學習近似方法也不保證能在 AIM 情境式 bandit 問題上達成改進,且論文本身定位為機器人模擬環境中的概念驗證,將此方法遷移至通用型模型持續改進仍待未來工作證明。

### 推送日期: 2026-11-11

[GR00T 2: Scaling Robot Foundation Models for Generalization, Dexterity, and Adaptation]({{ site.baseurl }}/zh/wm/gr00t-2-scaling-robot-foundation-models-for-generalization-dexterity-and-adaptation-2611090001/)

- **所屬主題**:Robot-Specific Action-Conditioned World Models（操作任務）
- **來源**:NVIDIA GEAR 技術白皮書(非傳統 arXiv 論文,發布於 research.nvidia.com/labs/gear/gr00t-2),2026 年 11 月 9 日於 CoRL 2026(第十屆機器人學習會議)正式發表會上公開發布,本頁尚未記錄過,作者團隊為 NVIDIA GEAR 研究室
- **選用理由**:同時滿足全部三項選取標準——(1) 大型產業實驗室出品,NVIDIA 為機器人基礎模型領域最具影響力的產業實驗室之一,於 CoRL 2026 正式發表會壓軸環節公開發表(由 NVIDIA 機器人主管 Jim Fan 親自主講);(2) 明確針對頂會發表,CoRL 2026 為機器人學習領域頂級會議,Google DeepMind、Meta、Tesla、Boston Dynamics 等同為會議鑽石級贊助商;(3) 真正的方法論創新:首次將 GR00T 系列從傳統 VLA 正式轉型為 world-action model,以單一 2B 參數 checkpoint 同時涵蓋平行夾爪、靈巧手、人形三種具身,並在超過 40 萬小時人類第一人稱影片規模上驗證「世界-動作聯合預測」可解鎖 X-Adaptability(無需目標機器人遠端操作示範即可學會新技能)這一此前模型未見的湧現能力。雖為產業白皮書形式而非傳統同行評審論文格式,但其技術內容、實驗規模與頂會發表時機均符合本頁收錄標準。
- **摘要**:論文指出既有 VLA 基礎模型雖能跨任務、跨具身遷移語言條件化操作技能,但普遍未直接學習場景動態本身,難以善用遠超機器人遠端操作資料規模的人類影片與手持裝置資料。作者提出 GR00T 2,一個 world-action model,建立在 Cosmos-Predict2.5-2B 影片擴散 transformer 之上,在每個控制步驟接收最近 0.8 秒多視角影片歷史、機器人本體感覺狀態與語言指令,以 flow matching 聯合生成未來多視角影片與動作區塊,使動作得以依循模型對未來的想像;預訓練資料涵蓋 402,730 小時人類第一人稱影片、10,184 小時手持 UMI 夾爪示範、23,500 小時機器人遠端操作資料。論文同時提出 GR00T 2 Turbo 輕量版本,以更高壓縮比影片表示使模型可在 Unitree G1 人形機器人自身的 Jetson Thor 上以 124 毫秒單步預測即時運行。在 Dexter-50 跨具身遷移基準(50 項目標機器人從未示範過的任務)上,GR00T 2 零樣本成功率達 40%,每任務 5 次示範(不到 3 分鐘機器人資料、單張 RTX 5090 上 30 分鐘微調)即可提升至 95%;結合推理 agent 的 agentic 控制下,YAM 機械臂三種玩具連續組裝每百次試驗成功 97 次以上;GR00T 2 Turbo 於 Unitree G1 上舀取遞送爆米花 48 次試驗全部成功。限制在於白皮書坦承評測任務集合經過篩選(僅納入 5 次示範可達 80% 以上成功率的任務),可能使報告的平均成功率高於任意新任務上的真實表現;權重與完整程式碼預計延至 2026 年 12 月才開源,目前僅釋出部分人類影片資料集,社群短期內尚無法獨立復現全部數字;GR00T 2 Turbo 雖速度大幅領先,但在多項靈巧操作任務上表現仍遜於完整版 GR00T 2。

### 推送日期: 2026-11-12

[How to Learn from What a Human Would Avoid? Intervention-Aware World Models with Real-World RL for Dexterous Manipulation (WHIRL)]({{ site.baseurl }}/zh/wm/whirl-intervention-aware-world-models-with-real-world-rl-for-dexterous-manipulation-2611139451/)

- **所屬主題**:Model-Based RL / Latent Dynamics for Control
- **來源**:arXiv:2609.06009,2026-09-05 發佈(本頁尚未記錄過,屬近期新作),論文 metadata 明確標註「Accepted by CoRL 2026」確認獲 CoRL 2026(第十屆機器人學習會議)接受,作者團隊來自香港科技大學(廣州)(HKUST-GZ)、義大利技術研究院(Italian Institute of Technology)、浙江大學
- **選用理由**:同時滿足三項選取標準中的兩項——(1) 已確認獲 CoRL 2026 接受;(2) 真正的方法論創新:首次將人在環路(HIL)RL 中操作者的二元化介入決策,轉化為前瞻式逐狀態介入機率預測,新增第四個預測頭與動態、獎勵、終止三頭並列,並將此預測轉化為 actor 端的風險塑形項,使 policy 從被動反應式修正轉變為主動規避操作者認為危險的區域,填補了既有 HIL RL 管線僅將人類介入視為事後糾正訊號而浪費其隱含前瞻風險資訊的方法論空白。暫未見大型科技公司直接參與(作者群為學術機構),未完全滿足標準二。
- **摘要**:論文指出多指靈巧操作的真實世界 RL 訓練因高維動作空間與硬體損壞的高昂代價而受限,人在環路 RL 雖允許操作者在危險發生前介入,但既有管線普遍將這類介入視為被動反應式修正,捨棄了操作者接管決策本身所蘊含的前瞻性安全訊號。作者提出 WHIRL,核心為一個具介入感知能力的 latent world model,具備動態、獎勵、終止與一個新穎的逐狀態介入機率預測頭,後者學習預測未來狀態下人類接管的可能性,並據此提供 actor 端風險塑形項,勸阻 policy 進入介入傾向高的區域。在 16 自由度 LEAP Hand 上涵蓋凸面與不規則物件抓取、稜柱操作、長 horizon 多階段任務的評測顯示,WHIRL 在複雜抓取任務上達到 96.7% 成功率,同時將操作者介入負擔降低最多 84%。限制在於評測侷限於單一機器手平台,且介入機率預測頭的訓練品質高度依賴操作者介入行為的一致性,不同操作者風格差異對學習結果的影響尚未見系統性量化分析。
