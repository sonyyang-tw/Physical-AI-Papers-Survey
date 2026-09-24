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

### 3. World Models for Autonomous Driving

Scope：用於駕駛場景生成、模擬、閉環評測與規劃的影片/latent world model。

代表論文：

- [DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting and Motion Alignment]({{ site.baseurl }}/zh/wm/driverse-navigation-world-model-for-driving-simulation-via-multimodal-trajectory-1945539343/) — arXiv:2504.18576 (ACM MM 2025)
- [End-to-End Driving with Online Trajectory Evaluation via BEV World Model (WoTE)]({{ site.baseurl }}/zh/wm/end-to-end-driving-with-online-trajectory-evaluation-via-bev-world-model-1945392255/) — arXiv:2504.01941 (ICCV 2025)
- [DreamerAD: Efficient Reinforcement Learning via Latent World Model for Autonomous Driving]({{ site.baseurl }}/zh/wm/dreamerad-efficient-reinforcement-learning-via-latent-world-model-for-autonomous-1945365119/) — arXiv:2603.24587
- [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)]({{ site.baseurl }}/zh/wm/other-vehicle-trajectories-are-also-needed-a-driving-world-model-unifies-ego-oth-1945392511/) — arXiv:2503.09215
- [Toward Physically Consistent Driving Video World Models under Challenging Trajectories (PhyGenesis)]({{ site.baseurl }}/zh/wm/toward-physically-consistent-driving-video-world-models-under-challenging-traje-1985672345/) — arXiv:2603.24506 — 物理條件生成器修正反事實/違反物理軌跡，提升碰撞等極端情境生成一致性

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

_(尚無記錄 — 排程啟動後將自動累積)_

### 推送日期: 2026-09-08

[Spatially Aware World Action Model via Geometric Latent Diffusion]({{ site.baseurl }}/zh/wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/) — World Action Models (Video-Action Joint Modeling) — arXiv 2609.02531，2026年9月2日新作，尚未於本頁記錄過

選中原因：作者群包含 Google DeepMind 研究員 Cordelia Schmid，符合「科技大廠/知名實驗室出品」準則；方法論上首次以「不改動凍結 VAE tokenizer」的方式將深度模態無縫注入既有 RGB World Action Model 擴散骨幹，屬於真正的架構創新而非既有技巧的小幅組合；同時在 RoboCasa、LIBERO-Plus 模擬 benchmark 與真實 UR5 機械臂上都取得 state-of-the-art 結果，驗證完整度高。

本文提出 SA-WAM，解決現有 World Action Models 僅在 RGB 觀測空間運作、缺乏顯式 3D/深度資訊的問題。核心方法是用非線性編碼將無界深度訊號映射進凍結 VAE tokenizer 的有界輸入域，使同一個預訓練影片擴散骨幹能同時做 action、RGB、depth 的聯合去噪預測。關鍵結果：在 RoboCasa 上僅用 50 筆示範即達 76.6% 成功率，超越 Cosmos-Policy baseline 9.5 個百分點，並在真實 UR5 機械臂隨機化環境評測中同樣勝出。限制與重要性：論文未公開 LIBERO-Plus 與真實世界實驗的精確數字，量化透明度有待改進，但其「幾何感知 + 保留預訓練先驗」的設計思路對 World Action Model 邁向 3D-aware 世代具有指標意義。

### 推送日期: 2026-09-09

[World Action Models are Zero-shot Policies (DreamZero)]({{ site.baseurl }}/zh/wm/world-action-models-are-zero-shot-policies-dreamzero-1951337490/) — Robot-Specific Action-Conditioned World Models（主題分類2）— arXiv:2602.15922，2026年2月17日提交，top conference caliber 出品（第三方 RoboArena 排行榜驗證第一名）、尚未於本頁記錄過

選中原因：作者群為 NVIDIA 主導的大型團隊（含 Linxi "Jim" Fan、Jan Kautz、Yuke Zhu 等知名研究者），符合「科技大廠/知名實驗室出品」準則；以「video as dense world representation」的視角將動作生成與影片預測統一為單一擴散骨幹的聯合去噪任務，是與既有 VLA 動作解碼、甚至既有 cascaded WAM 設計明確區隔的架構創新，而非既有技巧的小幅組合；在第三方維護的 RoboArena 公開排行榜（2026年4月）上以 1750 Elo 排名第一，領先 π0.5（1622）與 π-FAST（1592），驗證具高度公信力。

DreamZero 解決「VLA 語意泛化強、但物理動作泛化弱」的問題：以 Wan2.1-I2V-14B-480P 影片擴散模型為骨幹，聯合建模未來影片幀與動作序列，並透過系統/實作/模型三層優化讓 14B 參數模型達到 7Hz 即時閉環控制。關鍵結果：相較 state-of-the-art VLA 在新任務/新環境泛化上提升逾 2 倍，僅用 10-20 分鐘跨具身影片示範即可取得逾 42% 相對效能提升，僅用 30 分鐘 play data 即可少樣本適應全新機器人具身（YAM）。限制：作者自陳在需要次毫米級精度的高精度操作任務（如插銷、精密組裝）上仍繼承行為克隆的通病，且 14B 影片擴散模型即便優化後也僅達 7Hz，相較輕量 VLA 的推論延遲仍是實際部署瓶頸。

### 推送日期: 2026-09-10

[DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos]({{ site.baseurl }}/zh/wm/dreamdojo-a-generalist-robot-world-model-from-large-scale-human-videos-1955665089/) — Robot-Specific Action-Conditioned World Models（主題分類2，兼具資料規模化元素）— arXiv:2602.06949，2026年2月6日提交，top conference caliber 出品（NVIDIA GEAR 主導，作者含 Jitendra Malik、Pieter Abbeel、Yuke Zhu、Linxi "Jim" Fan 等）、尚未於本頁記錄過

選中原因：作者群為 NVIDIA GEAR 大型團隊，並有 UC Berkeley 知名學者（Jitendra Malik、Pieter Abbeel）加入，符合「科技大廠/知名實驗室出品」準則；以「連續潛在動作」作為統一代理動作機制，首次將 world model 預訓練資料規模化到 44,000 小時第一人稱人類影片（約 96 倍於現有最多樣機器人資料集），並設計蒸餾管線達成 10.81 FPS 即時推論，是資料規模化與工程落地並重的架構創新，而非既有技巧的小幅組合；與同團隊 EgoScale（arXiv:2602.16710，本次同時推送至 VLA Papers 頁面）共享資料與基礎設施，構成 NVIDIA GEAR「人類資料規模化」路線的 world model 端。

DreamDojo 解決「機器人 world model 高度依賴機器人自身資料、規模與多樣性有限」的問題：在 44K 小時人類第一人稱影片上預訓練基礎 world model，以連續潛在動作作為代理動作表示，克服人類影片缺乏動作標籤的障礙，並在小規模目標機器人資料上完成後訓練以獲得精確可控性。關鍵結果：蒸餾後模型達到 10.81 FPS 即時速度且上下文一致性提升，在多個分布外 benchmark 上驗證了模擬開放世界、接觸豐富任務的能力，支援即時遠端操作、策略評估、模型式規劃等應用。主要限制：仍需機器人資料後訓練才具備精確可控性，顯示人類到機器人的域落差依然存在；10.81 FPS 相較輕量 VLA policy 仍屬較高延遲，作為 policy-in-the-loop 使用時仍是部署瓶頸。

### 推送日期: 2026-09-11

[Inference-time Physics Alignment of Video Generative Models with Latent World Models]({{ site.baseurl }}/zh/wm/inference-time-physics-alignment-of-video-generative-models-with-latent-world-mo-1959634541/) — World Model Evaluation & Physical-Reasoning Benchmarks（主題分類5，兼具與基礎模型 V-JEPA 2 的下游應用關係）— arXiv:2601.10553，2026年1月15日提交（2月27日修訂v2），top conference caliber（ICCV 2025 Perception Test PhysicsIQ Challenge 冠軍）、尚未於本頁記錄過

選中原因：作者群包含 Meta FAIR 資深研究員 Nicolas Ballas 與 Michal Drozdzal（Ballas 為 V-JEPA/JEPA 系列共同主導者），符合「科技大廠/知名實驗室出品」準則；直接以 ICCV 2025 Perception Test PhysicsIQ Challenge 官方排行榜第一名（62.64%，超越前 SOTA 7.42 個百分點）驗證，屬第三方獨立評測背書的 top-conference-caliber 成果；方法論上首次將「提升影片生成物理合理性」重新定義為推論時對齊問題，以潛在世界模型 V-JEPA 2 作為獎勵訊號引導多條候選去噪軌跡，是與既有訓練時修正方案明確區隔的架構創新，而非既有技巧的小幅組合。

本文提出 WMReward，解決影片生成模型視覺逼真但常違反物理法則的問題：利用 V-JEPA 2 的物理先驗作為獎勵函數，在推論階段對多條候選去噪軌跡進行搜尋與引導，將測試時運算規模化應用於物理合理性對齊，無需重新訓練生成模型本身。關鍵結果：在 ICCV 2025 PhysicsIQ Challenge 奪冠（62.64%，超越前 SOTA 7.42 個百分點），並在影像/多幀/文字條件式生成情境下皆顯著提升物理合理性，經人類偏好研究驗證且未犧牲視覺品質。主要限制：仍會在流體潑濺等急遽物理事件上失敗，顯示受限於底層世界模型（V-JEPA-2）本身的物理理解上限，且推論時大量增加運算成本，對即時應用的適用性有限。

### 推送日期: 2026-09-14

[Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning]({{ site.baseurl }}/zh/wm/cosmos-policy-fine-tuning-video-models-for-visuomotor-control-and-planning-1963892209/) — Robot-Specific Action-Conditioned World Models（主題分類2）— arXiv:2601.16163，2026年1月22日提交，已被 ICLR 2026 接受（top conference caliber）、尚未於本頁記錄過

選中原因：作者群包含 NVIDIA 研究員（Ming-Yu Liu、Jinwei Gu 等）與史丹佛大學知名學者（Chelsea Finn、Shuran Song、Percy Liang），符合「科技大廠/知名實驗室出品」準則；已被 ICLR 2026 正式接受，同時符合「top conference caliber」準則；核心的「潛在影格注入」（latent frame injection）機制在不修改預訓練影片模型架構的前提下，將動作生成、未來狀態預測與價值評估統一表述為同一擴散序列的生成任務，是與既有「影片模型+額外動作頭+多階段訓練」範式明確區隔的架構創新，而非既有技巧的小幅組合；在模擬與真實世界雙軌評測上均取得 state-of-the-art 結果，驗證完整度高。

Cosmos Policy 解決「將預訓練影片模型的時空先驗適配為機器人 policy 需要額外架構元件與多階段訓練」的問題：以「潛在影格注入」機制，將機器人動作、未來狀態與價值估計都編碼為 Cosmos-Predict2 影片擴散模型序列中的潛在影格，僅需單一階段的機器人示範資料後訓練即可完成適配，並支援測試時規劃。關鍵結果：LIBERO 模擬 benchmark 達 98.5% 平均成功率、RoboCasa 達 67.1%，均為 state-of-the-art；真實世界 ALOHA 雙臂任務上勝過從頭訓練的 diffusion policy、既有影片模型 policy 及 π0.5、OpenVLA-OFT+ 等 SOTA VLA 模型；並能以自身 rollout 經驗持續精煉 world model 與價值函數。主要限制：高度依賴 Cosmos-Predict2 這一特定預訓練骨幹，遷移至其他影片模型的有效性未驗證，且真實世界評測僅限 ALOHA 雙臂平台，跨具身可遷移性與高頻控制場景下的推論延遲問題論文討論相對簡略。

### 推送日期: 2026-09-15

[Pelican-Sim 1.0: A General World Model Simulator for Embodied Intelligence]({{ site.baseurl }}/zh/wm/pelican-sim-1-0-a-general-world-model-simulator-for-embodied-intelligence-1968596049/) — Robot-Specific Action-Conditioned World Models（主題分類2）— arXiv:2609.12036，2026年9月10日新作，arXiv 當日新作（前五日提交）

選中原因：作者群出自 AgiBot 旗下 Beijing Innovation Center of Humanoid Robotics（與本頁已收錄之 τ0-WM 同源機構），符合「科技大廠/知名實驗室出品」準則；提出的「Action-visual injection」（以 URDF 與相機渲染的動作影片橋接動作與像素）搭配稀疏 MoE 層吸收異質具身動態衝突，是首次系統性同時解決跨具身通用性與動作可控性的架構設計，屬方法論創新而非既有技巧的小幅組合；訓練資料規模達約 100 萬筆真實與模擬軌跡，並在三個獨立 benchmark（AgiBotWorld Beta、RoboMIND、RoboTwin）與四項下游應用上均取得驗證，完整度高。

Pelican-Sim 1.0 解決現有機器人 world model 難以跨異質具身通用、且動作條件與像素預測耦合不足的問題：以 28 維統一動作值空間表示跨主流具身動作，並透過 Action-visual injection 將 URDF/相機渲染的動作影片注入 28 層 Video DiT 骨幹（Context Block 注入動作影片殘差、動作值 embedding 做 scale-and-shift 調變），輔以稀疏 MoE 層降低模態衝突，再以因果適配與少步驟蒸餾將 35 步擴散 rollout 壓縮為 4 步自迴歸生成（5.67 倍加速）。關鍵結果：PSNR 較最強基線在三個 benchmark 上分別提升 4.636、2.080、10.343；下游應用上，RoboTwin 每任務加入 500 筆生成軌跡可將 policy 成功率從 70% 提升至 93%，policy 評估 Pearson 相關係數達 0.994。主要限制：作為技術報告尚未見明確會議接受狀態，四項下游應用的量化驗證僅限於 RoboTwin 單一 benchmark，且蒸餾後 4 步自迴歸模擬器在長 horizon rollout 下是否累積誤差放大未見充分討論。

### 推送日期: 2026-09-16

[GE-Act 2.0: Pretraining and Scaling a World-Action Model for Robotic Manipulation]({{ site.baseurl }}/zh/wm/ge-act-2-0-pretraining-and-scaling-a-world-action-model-for-robotic-manipulation-1972876063/) — Robot-Specific Action-Conditioned World Models（主題分類2，兼具資料規模化元素）— arXiv:2609.05588，2026年9月4日新作，AgiBot Research Team 技術報告（top-conference caliber 尚未正式標記）、尚未於本頁記錄過

選中原因：作者群為 AgiBot Research Team（46 位作者的大型工業研究團隊），符合「科技大廠/知名實驗室出品」準則，且為本頁已收錄之 τ0-WM 同源機構，是 Genie Envisioner 系列的直接後繼者；方法論上首次系統性地以完全從零訓練（而非繼承既有預訓練影片生成器）的方式建構 WAM，並以 CoAE / SVP / IDM 三模組解耦架構搭配 knowledge-aligned selective optimization（KASO）驗證資料規模化規律，是與既有「借用式」WAM 路線明確區隔的架構與實證創新，而非既有技巧的小幅組合；評測涵蓋 100 項任務、20 個技能群組、held-out 場景/背景/光照/物件，資料規模橫跨 300 至 30,000 小時，屬工業級投入。雖尚未見正式會議接受標記，但方法論嚴謹度與規模符合 top-conference caliber 水準。

GE-Act 2.0 解決「WAM 專屬預訓練與資料規模化規律始終未被系統性驗證」的問題：以 control-oriented autoencoder（CoAE）、single-step visual planner（SVP）、inverse dynamics model（IDM）三模組從零訓練，並以 KASO 過濾監督訊號不匹配的預測未來後聯合訓練。關鍵結果：零樣本（無任務專屬微調）情境下，將共訓練資料規模從 300 小時擴大到 30,000 小時，G1-OP 成功率從 17.1% 提升至 44.1%、G2-90D 從 13.4% 提升至 31.1%（僅佔資料不到 2% 卻提升 17.7 個百分點，顯示跨具身遷移能力），且技能覆蓋率與 OOD 成功率 Pearson 相關係數達 0.80。主要限制：技術報告尚未標記正式會議接受狀態，且所有評測皆基於 AgiBot 自身平台，跨機構第三方驗證仍待補足。


### 推送日期: 2026-09-17

[GeniWorld: A Generalizable Interactive World Model for Robotic Manipulation via Visual Actions]({{ site.baseurl }}/zh/wm/geniworld-a-generalizable-interactive-world-model-for-robotic-manipulation-1978234598/) — Robot-Specific Action-Conditioned World Models（主題分類2）— arXiv:2608.06332，2026年8月6日提交，尚未於本頁記錄過

選中原因：作者群來自 Shenzhen International Graduate School, Tsinghua University 與 Tencent Robotics X（並有 HKUST、Shenzhen Technology University 參與），符合「科技大廠/知名實驗室出品」準則；首次系統性提出「視覺動作」（將數值動作透過 URDF 渲染轉為視覺化機器人運動）作為 world model 條件化訊號，取代既有直接以數值動作向量或末端執行器/骨架姿態條件化的範式，明確解耦具身運動學與環境動態，是與既有 action-conditioned world model（如 Ctrl-World、IRASim、EnerVerse-AC）方法論明確區隔的創新，而非既有技巧的小幅組合；在標準化 RoboTwin2.0 benchmark 上與三個既有基線完整比較，並於真實機器人平台驗證 policy 評估與資料生成兩項下游應用，完整度高。

GeniWorld 解決既有 action-conditioned world model 因數值動作向量缺乏空間對齊、且低維動作條件化將具身運動與環境動態糾纏在一起，導致模型對未見場景泛化不佳、易發生場景過擬合的問題：核心方法是以具身專屬運動學模型將數值動作轉為稠密視覺動作（URDF 渲染），編碼為與場景觀測空間對齊的潛在表示後，輸入以因果注意力建構的自迴歸 DiT，以 flow matching 預測未來影片，並透過 KV caching 實現閉環互動。關鍵結果：在 RoboTwin2.0 的 Clean-to-Clean 與 Clean-to-Random（零樣本 OOD）雙評測設定下六項生成品質指標全面優於既有基線，場景偏移下 FID/FVD 僅 13.08/20.15（IRASim 則惡化至 174.52/191.26）；推論取樣步數從 50 降至 5 步時品質幾乎不衰退，達成約 10 倍加速並在真實硬體上實現約 8Hz 互動速率；下游應用上，僅用 25 筆真實示範搭配合成資料即可將分布外任務成功率大幅提升（如空間重排任務從 37.5% 提升至 62.5%）。主要限制：依賴具身專屬 URDF 運動學建模，增加跨具身部署工程成本，且真實世界驗證僅涵蓋四項操作任務，跨任務類型與跨具身的泛化能力尚待更廣泛驗證。

### 推送日期: 2026-09-21

[Astra: General Interactive World Model with Autoregressive Denoising]({{ site.baseurl }}/zh/wm/astra-general-interactive-world-model-with-autoregressive-denoising-1978567891/) — Robot-Specific Action-Conditioned World Models（主題分類2，兼具 World Models for Autonomous Driving 跨場景元素）— arXiv:2512.08931，2025年12月9日提交（2026年1月27日修訂v3），已被 ICLR 2026 正式接受（top conference caliber）、尚未於本頁記錄過

選中原因：已被 ICLR 2026 正式接受，符合「top conference caliber」準則；作者群來自清華大學與快手科技（Kuaishou Technology）Kling 團隊（含 Xin Tao、Pengfei Wan 等可靈影片生成模型核心研究者），符合「科技大廠/知名實驗室出品」準則；提出「噪聲即遮罩」(noise-as-mask) 訓練策略與混合動作專家 (MoAE) 路由機制，首次以單一自迴歸去噪架構統一處理自駕、機器人操作、開放世界探索等異質動作模態的互動式世界模型，是與既有僅針對單一領域客製化動作條件化方式的方法明確區隔的架構與訓練策略創新，而非既有技巧的小幅組合；在 Sekai、SpatialVID、RT-1、nuScenes、Multi-Cam Video 等五個獨立公開資料集上完整驗證，涵蓋多元應用場景。

Astra 解決現有影片生成模型僅能產生短暫自成一體片段、無法對外部刺激（智能體移動、視角變化、控制訊號）產生動態回應的長 horizon 一致 rollout，且既有自迴歸延伸方法難以兼顧歷史一致性與動作回應性、易發生誤差累積的問題：核心方法為自迴歸去噪架構搭配時間因果注意力聚合過去觀測，以噪聲即遮罩策略削弱歷史脈絡主導性、迫使模型整合動作線索，並以輕量 ACT-Adapter 將動作訊號注入去噪過程，再以 MoAE 動態路由異質動作模態至專屬專家。關鍵結果：在自建 Astra-Bench 上全面勝過 Wan-2.1、Matrix-Game、YUME 等既有 SOTA 方法，於視覺品質與動作對齊指標上均取得領先，且在長距離 rollout 下維持穩定性（既有方法常見誤差累積與畫面漂移）；消融實驗證實 ACT-Adapter 優於既有 cross-attention adapter、noise-as-mask 確實緩解視覺慣性問題。主要限制：作者明確坦承推論效率仍是主要瓶頸，多步去噪加自迴歸 rollout 使即時部署（尤其線上控制、互動式機器人等延遲敏感場景）面臨挑戰，未來需仰賴蒸餾等壓縮策略降低推論成本。

### 推送日期: 2026-09-22

[NVIDIA OmniDreams: Real-Time Generative World Model for Closed-Loop Autonomous Vehicle Simulation]({{ site.baseurl }}/zh/wm/nvidia-omnidreams-real-time-generative-world-model-for-closed-loop-autonomous-ve-1982345698/) — World Models for Autonomous Driving（主題分類3，兼具 Robot-Specific Action-Conditioned World Models 的 WAM 後期訓練元素）— arXiv:2606.03159，2026年6月2日提交（7月23日修訂v2），NVIDIA 大型研究團隊技術報告（top-conference caliber 尚未正式標記，但方法論與規模符合水準）、尚未於本頁記錄過

選中原因：作者群為 NVIDIA 大型研究團隊（含 Sanja Fidler 等知名研究者），符合「科技大廠/知名實驗室出品」準則；首次系統性地將 Self Forcing 蒸餾與漸進式長 context 教師策略應用於自駕領域，達成單視角 68 FPS、多視角 105 FPS 的即時閉環模擬速度，並整合進 NVIDIA AlpaSim 取代既有重建式 NuRec 渲染器，是與既有僅產出離線高品質影片的生成式 world model（GAIA-1/GAIA-2、DriveDreamer）明確區隔的工程與方法論創新；同時驗證同一骨幹可後期訓練為 World-Action Model，以五分之一參數量超越 VLA-based Alpamayo 1.5，將「世界模型」與「動作生成」統一於單一架構，訓練資料規模達 21,000 小時，屬工業級投入。

OmniDreams 解決以重建為基礎（3DGS/NeRF）的閉環自駕模擬器受限於原始擷取資料、難以合成未曾記錄過的長尾現象（極端天氣、罕見動態代理行為）的問題：核心方法是從 Cosmos-Predict 2.5 擴散骨幹中/後期訓練，以首幀影像、文字提示、世界場景地圖三種訊號為條件，透過 Diffusion Forcing 轉為因果自迴歸模型，再以 Self Forcing 蒸餾（結合自我 rollout 與 Distribution Matching Distillation）大幅提速，並以漸進式長 context 教師策略緩解長 rollout 畫面漂移。關鍵結果：單視角 2B 模型於單顆 GB300 GPU 達 68 FPS；蒸餾後模型 FVD 24.8 甚至優於雙向教師模型的 26.8；漸進式長 context 教師將 20 秒 rollout 的 FVD 漂移從 299.9 大幅降至 172.9；後期訓練的 World-Action Model 在 574 場景 NuRec 資料集上以約 20 億參數（Alpamayo 1.5 的五分之一）將整體碰撞率從 6.9% 降至 4.2%。主要限制：影片生成式模擬相較重建式模擬器需要遠高得多的運算資源，目前以固定長度區塊生成、無法在區塊內即時修改軌跡，WAM 評測結果作者自陳仍屬初步性質。

### 推送日期: 2026-09-24

[Toward Physically Consistent Driving Video World Models under Challenging Trajectories (PhyGenesis)]({{ site.baseurl }}/zh/wm/toward-physically-consistent-driving-video-world-models-under-challenging-traje-1985672345/) — World Models for Autonomous Driving（主題分類3）— arXiv:2603.24506，2026年3月25日提交（4月1日修訂v2），尚未於本頁記錄過

選中原因：作者群來自浙江大學、小米汽車（Xiaomi EV）、香港理工大學與深圳灣實驗室聯合團隊，小米汽車作為自駕領域積極投入的科技大廠，符合「科技大廠/知名實驗室出品」準則；首次系統性地將「軌跡可行性物理推理」形式化為獨立的反事實軌跡修正訓練任務，並與物理增強影片生成器串接，明確區隔於既有僅將結構化條件視為「條件到像素」翻譯任務的自駕 world model（MagicDrive-V2、DiST-4D 等），是方法論創新而非既有技巧的小幅組合；以 CARLA 模擬器建構物理豐富異質資料集彌補真實資料中極端物理事件的稀缺性，並在三個資料集上與三個既有基線完整比較，驗證完整度高。

PhyGenesis 解決現有自駕影片 world model 在具挑戰性或反事實軌跡條件下（如模擬器/規劃系統產生的不完美軌跡）常產生嚴重物理不一致與視覺偽影的問題：核心方法是物理條件生成器透過反事實軌跡修正訓練任務，將物理違反的軌跡輸入轉換為合理的 6-DoF 車輛運動，再由以 WAN2.1 初始化的物理增強影片生成器在真實與 CARLA 模擬混合的異質資料上訓練，產出高保真多視角駕駛影片。關鍵結果：在 nuScenes 常態軌跡與 CARLA Ego/ADV 物理違反軌跡三個資料集上，視覺品質（FID/FVD）、物理一致性（PHY）與人類偏好率全面超越 UniMLVG、MagicDrive-V2、DiST-4D 三個基線，在最具挑戰性的 CARLA ADV 上差距尤為顯著（PHY 0.87 對比次佳基線 0.56）；消融實驗證實異質訓練資料使 CARLA ADV 上的 FVD 相對改善約 13.4%。主要限制：論文正文未見獨立的作者自陳 Limitation 段落，CARLA 生成資料與真實資料間的視覺風格落差仍需額外風格轉換模型彌合，且反事實軌跡修正目前聚焦碰撞與偏離道路兩類事件，對更廣泛物理違反情境的泛化能力有待驗證。
