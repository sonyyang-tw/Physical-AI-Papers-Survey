---
layout: paper
title: "End-to-End Driving with Online Trajectory Evaluation via BEV World Model"
section: wm
page_id: "1945392255"
permalink: /en/wm/end-to-end-driving-with-online-trajectory-evaluation-via-bev-world-model-1945392255/
---

**Paper** : [End-to-End Driving with Online Trajectory Evaluation via BEV World Model](https://arxiv.org/abs/2504.01941)  
**Source** : arXiv / ICCV 2025 (accepted)  
**arXiv ID** : 2504.01941

### Abstract

End-to-end autonomous driving has made significant progress by integrating perception, prediction, and planning into a single fully differentiable framework. However, to fully realize its potential, effective online trajectory evaluation is indispensable for ensuring safety. Trajectory evaluation becomes more effective by predicting the future outcomes of a given trajectory, which can be achieved by using a world model to capture environmental dynamics and predict future states. Accordingly, the authors propose an end-to-end driving framework, WoTE, which leverages a BEV (bird's-eye-view) world model to predict future BEV states for trajectory evaluation. The proposed BEV world model has better latency efficiency than image-level world models and can be seamlessly supervised in training using an off-the-shelf BEV-space traffic simulator. The authors validate this framework on the NAVSIM benchmark as well as on the closed-loop Bench2Drive benchmark based on the CARLA simulator, achieving state-of-the-art performance. The code has been released on GitHub.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392255_wote_fig1.png) 

_Figure 1: WoTE concept diagram - previous end-to-end driving methods focus on learning high-quality trajectories (a); WoTE further uses a BEV world model to perform online evaluation of candidate trajectories (b)._

![Figure]({{ site.baseurl }}/assets/images/1945392255_wote_fig2.png) 

_Figure 2: Overall WoTE architecture - divided into two main parts: Trajectory Prediction (a BEV encoder encodes multi-view images to produce trajectory candidates) and Trajectory Evaluation (a BEV world model predicts future states and scores them)._

  * Problem addressed: Although end-to-end autonomous driving systems can already integrate perception, prediction, and planning, they lack an effective online trajectory evaluation mechanism to ensure safety. The authors identify two key technical challenges: first, a good representation of future scenes is needed — many existing autonomous-driving world models use diffusion models to predict future image-level scenes, which is computationally expensive and unsuitable for real-time driving; second, there is a lack of supervision signals for future states — a world model needs to imagine multiple future states for multiple candidate trajectories separately, but real-world datasets typically contain only one future state that actually occurred, unable to directly provide supervision for multiple futures.
  * Main method: Proposes the WoTE framework, the core of which is a BEV-space world model used to predict future BEV states to evaluate the quality of candidate trajectories. This BEV world model has higher latency efficiency than image-level world models (since it does not need to generate a complete pixel-level image), and can directly use an off-the-shelf BEV-space traffic simulator as a source of supervision signals, solving the problem of "lack of supervision for multiple futures." Trajectory evaluation is performed by comparing BEV features with trajectory embeddings, making the entire evaluation process differentiable, so it can be jointly optimized end-to-end with the perception and planning modules.
  * Difference from previous approaches: Compared with many previous model-based trajectory evaluation methods that rely on explicit trajectory representations and non-differentiable metrics (which limits their end-to-end optimization ability), and image-level world models that are computationally expensive due to diffusion generation, WoTE chooses to model the future in BEV space (rather than pixel space), balancing efficiency (no need to generate complete images) and differentiability (can be directly embedded in end-to-end training). Compared with model-free trajectory evaluation methods such as Hydra-MDP, WoTE demonstrates the advantages of a model-based approach by introducing a BEV world model.
  * Key design description: The overall pipeline can be understood as follows: the perception module first encodes sensor input into a BEV feature representation (semantic/geometric information of the scene from a bird's-eye view); the planning module proposes multiple candidate future trajectories; for each candidate trajectory, the BEV world model "imagines," in BEV space, how the scene would evolve after executing that trajectory (e.g., changes in the positions of other vehicles and pedestrians), producing a corresponding future BEV state prediction, rather than generating a complete pixel-level video frame; these predicted future BEV states and the trajectory itself are then encoded into feature vectors, and a differentiable scoring mechanism evaluates and ranks each candidate trajectory to select the safest/optimal trajectory to execute. During training, the BEV world model's predictions can be directly supervised using multiple future states generated by an off-the-shelf BEV-space traffic simulator, solving the limitation that real-world datasets only have a single true future.



### Result

  * WoTE achieves state-of-the-art performance on both the NAVSIM benchmark and the closed-loop Bench2Drive benchmark based on the CARLA simulator.
  * The paper specifically notes that WoTE outperforms Hydra-MDP, because Hydra-MDP uses a model-free trajectory evaluation approach while WoTE uses a model-based (BEV world model) approach, highlighting the advantages of the model-based method.
  * WoTE's code has been made public on GitHub (liyingyanUCAS/WoTE), and has already been cited by subsequent works (such as WPT and MindDrive) as a strong baseline, showing that its results have a certain degree of credibility and influence.
  * The abstract and available information do not provide a complete quantitative comparison table between WoTE and other contemporaneous BEV/world model methods (besides Hydra-MDP); the full text or the original paper's experimental tables need to be checked to obtain complete comparison data.



### Limitation

  * The paper's abstract does not contain an explicit self-stated Limitation section; the full text needs to be checked to confirm the limitations the authors state themselves.
  * Potential weaknesses inferred from the method design: although the BEV world model is more efficient than an image-level world model, the BEV representation itself is a dimensionality-reduced abstract representation, which may lose some information implicit in pixel-level details (such as fine textures and lighting changes). This kind of information may affect safety evaluation in certain edge cases (such as judging slippery road surfaces or visual occlusion caused by lighting), but the abstract does not discuss this trade-off. In addition, relying on an "off-the-shelf BEV-space traffic simulator" as the source of supervision means that the quality of the model's evaluation is to some extent limited by the fidelity and coverage of that simulator itself.



### Related work

  * WPT (World-to-Policy Transfer, arXiv:2511.20095) and MindDrive (arXiv:2512.04441) are subsequent works that cite WoTE as a strong baseline, showing that WoTE has continuing influence in the field of end-to-end autonomous-driving world models; it is worth tracking how these follow-up studies further improve on or challenge WoTE's design.
  * Belongs to the same autonomous-driving world model field as DriVerse (arXiv:2504.18576) but takes a different technical route, suitable for comparing the relative merits of "BEV-space trajectory evaluation" versus "pixel-level trajectory conditioned generation" as two different application orientations.
  * Degree worth surveying: high. WoTE has been proven to hold a landmark position in this sub-field (already cited and compared by multiple subsequent papers), making it suitable as an important reference point for understanding "how world models are integrated into end-to-end autonomous-driving decision frameworks."



### Conclusion

  * Overall assessment: Worth reference. WoTE proposes a solution that balances efficiency and effectiveness (modeling in BEV space rather than pixel space) for the specific engineering problem of "how to achieve efficient and differentiable online trajectory evaluation within an end-to-end autonomous-driving framework," and achieves SOTA performance on two benchmarks of different natures (NAVSIM open-loop, Bench2Drive closed-loop), demonstrating the robustness of the method. It has been accepted by ICCV 2025 and has become an important baseline for subsequent work, giving it high reference value.
  * Relationship with other important articles: WoTE belongs to the same autonomous-driving world model field as DriVerse, but represents two different technical routes: "decision-evaluation-oriented" versus "scene-generation-oriented." WoTE also directly compares against Hydra-MDP (a model-free method), demonstrating the advantages of a model-based (world model) approach on this task, and has been extended and cited by subsequent research such as WPT and MindDrive.
  * ROCm/AMD relevance: The paper focuses on the architectural design of the BEV world model and autonomous-driving benchmark testing, and does not mention the computing hardware platform used or any ROCm-related content. No clear connection to ROCm/AMD can be found from the available information; considering the "latency efficiency advantage" of the BEV world model relative to image-level models, this kind of efficiency-oriented architectural design would theoretically be easier to deploy on resource-constrained or non-NVIDIA hardware platforms (such as AMD GPUs), but the paper itself does not discuss this point, and it would need to be separately verified or tested.
