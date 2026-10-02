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

- [Spatially Aware World Action Model via Geometric Latent Diffusion]({{ site.baseurl }}/zh/wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/) — arXiv:2609.02531（Google DeepMind 參與）— 在不改動凍結 VAE tokenizer 前提下將深度模態注入 RGB World Action Model 擴散骨幹（原始分類為 World Action Models / Video-Action Joint Modeling，歸入本類別待覆核）
- [World Action Models are Zero-shot Policies (DreamZero)]({{ site.baseurl }}/zh/wm/world-action-models-are-zero-shot-policies-dreamzero-1951337490/) — arXiv:2602.15922（NVIDIA，RoboArena 排行榜第一）— 以影片擴散骨幹聯合建模未來影格與動作序列，統一動作生成與影片預測
- [DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos]({{ site.baseurl }}/zh/wm/dreamdojo-a-generalist-robot-world-model-from-large-scale-human-videos-1955665089/) — arXiv:2602.06949（NVIDIA GEAR）— 以連續潛在動作作為代理動作機制，於 44,000 小時第一人稱人類影片上預訓練 world model
- [Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning]({{ site.baseurl }}/zh/wm/cosmos-policy-fine-tuning-video-models-for-visuomotor-control-and-planning-1963892209/) — arXiv:2601.16163（ICLR 2026, NVIDIA/Stanford）— 潛在影格注入機制統一動作生成、未來狀態預測與價值評估於同一擴散序列
- [Astra: General Interactive World Model with Autoregressive Denoising]({{ site.baseurl }}/zh/wm/astra-general-interactive-world-model-with-autoregressive-denoising-1978567891/) — arXiv:2512.08931（ICLR 2026, 清華/快手 Kling）— 噪聲即遮罩策略與混合動作專家路由，以單一自迴歸去噪架構統一處理異質動作模態

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

### 4. Model-Based RL / Latent Dynamics for Control

Scope：經典 model-based RL，用學習到的 latent 動態模型做規劃/想像式 policy 學習（不一定是 pixel 層級，與機器人無關）。

代表論文：

- DreamerV3（見上方基礎模型）
- [Dream-MPC: Gradient-Based Model Predictive Control with Latent Imagination]({{ site.baseurl }}/zh/wm/dream-mpc-gradient-based-model-predictive-control-with-latent-imagination-1945365146/) — arXiv:2605.04568 (ICML 2026)

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

### 推送日期: 2026-10-01

[Evaluating Gemini Robotics Policies in a Veo World Simulator]({{ site.baseurl }}/zh/wm/evaluating-gemini-robotics-policies-in-a-veo-world-simulator-1790838179/)

- **所屬主題**：World Model Evaluation & Physical-Reasoning Benchmarks
- **來源**：arXiv:2512.10675，Google DeepMind Gemini Robotics Team，2025-12-11 發佈 / 2026-01-06 修訂第二版（非 2026 年 9 月最新發佈，但作者群涵蓋 Gemini Robotics 核心團隊 23 位研究者，且本頁尚未記錄過，廣泛搜尋近一年 VLA/world-model 大型科技公司新作後確認為最具代表性、尚未收錄的選擇）
- **選用理由**：同時滿足三項選取標準——(1) Google DeepMind 出品，作者群涵蓋 Gemini Robotics Team 共 23 位研究者；(2) 方法論意義：首次系統性證明影片生成模型可同時支援政策評測的完整光譜（分佈內、分佈外泛化、安全紅隊測試），而非僅止於單一應用場景的展示；(3) 嚴謹的實證驗證規模——1600 餘次真實世界評測驗證預測保真度，遠超同類研究的驗證規模。
- **摘要**：論文建立了一套以 Veo 2 影片基礎模型為核心的生成式評測系統，結合動作條件化、多視角一致性生成、以及 NanoBanana 生成式影像編輯，能針對 Gemini Robotics 政策在分佈內與分佈外場景下的表現做準確預測（分佈內排序與真實評測 Pearson 相關係數佳,分佈外泛化軸向難度排序 MMRV=0.06、Pearson=0.86），並成功用於安全紅隊測試挖掘政策的潛在不安全行為。限制在於預測成功率存在系統性低估、短 horizon(8秒)rollout、依賴人工評分，顯示這是生成式世界模型作為機器人評測工具這一新興方向的早期但扎實的一步。

### 推送日期: 2026-10-02

[Percept-WAM: Perception-Enhanced World-Awareness-Action Model for Robust End-to-End Autonomous Driving]({{ site.baseurl }}/zh/wm/percept-wam-perception-enhanced-world-awareness-action-model-for-robust-end-1790912567/)

- **所屬主題**：World Models for Autonomous Driving
- **來源**：arXiv:2511.19221，2025-11-24 發佈（非 2026 年 9 月最新發佈，但已確認獲 CVPR 2026 接受，作者群來自 Yinwang Intelligent Technology／引望智能技術——華為旗下智慧駕駛子公司，AITO/華為 ADS 智駕系統背後團隊——與復旦大學，共 19 位研究者；本頁尚未記錄過，廣泛搜尋近一年自駕 world-model 大型科技公司新作後確認為最具代表性、尚未收錄的選擇）
- **選用理由**：同時滿足三項選取標準——(1) 已確認獲 CVPR 2026 接受（見 CVPR 2026 Open Access Repository 正式收錄頁面）；(2) 大型產業實驗室出品，Yinwang Intelligent Technology 為華為旗下智慧駕駛子公司，是 AITO/華為 ADS 智駕系統背後團隊；(3) 方法論意義：首度在單一 VLM 內隱式整合 2D/3D 場景理解能力，以專屬 World-PV/World-BEV token 取代既有問答式空間推理，是架構層級而非增量式的創新。
- **摘要**：論文針對現有 VLM-based 自駕系統空間定位能力薄弱的問題，提出 Percept-WAM，將 2D/3D 感知任務統一編碼為 World-PV（透視視角）與 World-BEV（鳥瞰視角）兩類 token，同時編碼空間座標與信心分數，並搭配網格條件化預測機制與 IoU-aware 信心度訓練策略，提升長尾、遠距、小物件場景下的感知穩定性。實驗顯示模型在 COCO 2D 偵測（51.7 mAP）與 nuScenes BEV 3D 偵測（58.9 mAP）上達到或超越傳統非 VLM 偵測器表現，整合軌跡解碼器後在 NAVSIM 上的 PDMS 指標超越強基線 DiffusionDrive 達 2.1 分。限制在於論文未充分討論雙重 token 表示與雙模式解碼帶來的計算成本與即時性權衡，這點對高度延遲敏感的自動駕駛應用而言是值得後續關注的落地議題。
