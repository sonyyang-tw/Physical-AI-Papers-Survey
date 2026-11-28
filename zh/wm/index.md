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

- [WorldDrive: Bridging Scene Generation and Planning via Unifying Vision and Motion Representation]({{ site.baseurl }}/zh/wm/worlddrive-bridging-scene-generation-and-planning-driving-with-world-2603149480/) — arXiv:2603.14948（NeurIPS 2026，澳門大學 / Afari Intelligent Drive / 山東大學）— 以軌跡詞彙表為條件統一視覺與動作表徵，讓場景生成學得的編碼器直接遷移繼承至規劃器，搭配 Future-aware Rewarder 蒸餾未來潛在表徵實現低延遲即時規劃

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

- [GRAIL: Generating Humanoid Loco-Manipulation from World Models]({{ site.baseurl }}/zh/wm/grail-generating-humanoid-loco-manipulation-from-world-models-2606051600/) — arXiv:2606.05160（CoRL 2026 Oral，最佳論文獎決選，NVIDIA DAIR / UCLA）— 將影片世界模型嵌入完整指定的 3D 資產管線，部署前完全數位化生成人形機器人 loco-manipulation 示範，真實 Unitree G1 達 84% 拾取成功率與 90% 爬樓梯成功率

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

_(目前無待歸檔項目 — 近 7 天內尚無新推送記錄。)_
