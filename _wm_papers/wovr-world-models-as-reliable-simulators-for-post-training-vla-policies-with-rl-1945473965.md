---
layout: paper
title: "WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL"
section: wm
page_id: "1945473965"
permalink: /wm/wovr-world-models-as-reliable-simulators-for-post-training-vla-policies-with-rl-1945473965/
---

**Paper** : [WoVR: World Models as Reliable Simulators for Post-Training VLA Policies with RL](https://arxiv.org/abs/2602.13977)  
**Source** : arXiv (cs.RO, cs.AI), CoRL Preprint  
**arXiv ID** : 2602.13977

### Abstract

Reinforcement learning (RL) holds promise for unlocking capabilities in vision-language-action (VLA) models beyond what imitation learning can achieve, but RL requires extensive real-world interaction, making it difficult to deploy directly on physical robots. Recent research has attempted to use learned world models as simulators for policy optimization; however, closed-loop imagined rollouts inevitably suffer from hallucination and long-horizon error accumulation, which not only degrade visual fidelity but also mislead policy optimization, providing unreliable learning signals. This paper proposes WoVR, a reliable world-model-based RL framework for post-training VLA policies. WoVR does not assume the world model is fully faithful; instead, it explicitly regulates how RL interacts with imperfect imagined dynamics: it improves rollout stability through a controllable action-conditioned video world model, reshapes imagined interaction through Keyframe-Initialized Rollouts (KIR) to reduce effective error depth, and maintains alignment between the policy and the simulator through "World Model-Policy Co-evolution." Experiments show that WoVR enables stable long-horizon imagined rollouts and effective policy optimization, achieving strong performance on LIBERO and consistent real-world performance gains across multiple robot platforms.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473965_wovr_fig1.png) 

_Figure 2 (original numbering): WoVR overview — building a reliable reinforcement learning framework by strengthening the world model as a controllable simulator, reducing error depth with Keyframe-Initialized Rollouts (KIR), and maintaining policy-model alignment with PACE._

![Figure]({{ site.baseurl }}/assets/images/1945473965_wovr_fig2.png) 

_Figure 3 (original numbering): Action-conditioned world model architecture, based on a video diffusion backbone with a dual-channel action injection design achieving frame-level controllability and stable chunked autoregressive generation._

  * **Problem being addressed**: when a world model is used as an RL simulator, closed-loop imagined rollouts become distorted due to hallucination and long-horizon error accumulation, causing policy optimization to receive unreliable learning signals, making it difficult to directly treat an "imperfect world model" as a real environment.
  * **Main method**: WoVR consists of three core components:
    * A controllable action-conditioned video world model, improving the stability and visual fidelity of rollouts.
    * **Keyframe-Initialized Rollouts (KIR)**: reinitializes imagined interaction from keyframes to shorten the "effective error depth," reducing the damage that long-horizon error accumulation does to policy learning.
    * **World Model–Policy Co-evolution**: lets the policy's rollout data feed back into updating the world model, and the improved world model in turn produces better imagined data for training the policy, forming a loop in which the policy and simulator align and co-evolve with each other.
  * **Difference from prior approaches**: prior methods mostly assumed the world model was "accurate enough" to be used directly as a simulator; WoVR takes the opposite approach, explicitly acknowledging the world model's imperfection and designing mechanisms (KIR, co-evolution) to actively regulate/mitigate the contamination of RL training signals by hallucination and error accumulation, rather than simply pursuing higher accuracy in the world model itself.
  * **Description of key design**: the overall pipeline is: teleoperated/real data → train a controllable action-conditioned video world model → the VLA policy performs imagined rollouts within the world model (restarting from keyframes via KIR to limit error depth) → RL uses these imagined rollouts to update the policy → new behavioral data produced by the policy feeds back to update the world model (co-evolution) → the cycle repeats iteratively, progressively validated through deployment on real robot platforms.



### Result

  * On the LIBERO benchmark, WoVR raises the average success rate from 39.95% to 69.2% (+29.3 percentage points), and real-robot task success rate from 61.7% to 91.7% (+30.0 percentage points).
  * Under a stronger baseline setting (a base policy fully SFT-trained on trajectories, already at 88.1%), GRPO reaches 89.7% and WMPO reaches 92.4%, while WoVR still achieves the highest average success rate at 95.9%.
  * Deployed on two real robot platforms: the Franka platform improves by +28.9 percentage points and the AgileX Piper platform improves by +13.4 percentage points, both outperforming the comparison methods.
  * The world model itself achieves SOTA quality while maintaining efficient rollouts (23 FPS).
  * Fairness: these figures (69.2%, 91.7%, 95.9%, etc.) come from the paper's own self-reported results, which are inherently self-comparative in nature. According to comments from another paper (Sword, arXiv:2605.07288), WoVR shows notably weak style robustness under out-of-distribution (OOD) conditions—generation style starts deviating from ground truth from around the 15th frame onward—suggesting that the magnitude of its real-world improvement may vary with scene/style distribution. This point requires cross-checking the experimental setup differences between the original paper and the Sword paper.



### Limitation

  * The paper itself emphasizes that it "does not assume the world model is fully faithful," which means its design starting point already acknowledges the existence of hallucination and error accumulation problems in the world model, and mitigates rather than fully solves them through KIR and co-evolution.
  * According to independent commentary from another paper (Sword), WoVR has relatively weak robustness to out-of-distribution/style shift (under OOD conditions, generation style starts deviating from ground truth around frame 15), suggesting that its method's ability to generalize to scenes outside the training distribution may be limited; it needs to be verified whether the original paper discusses this limitation.
  * The abstract and available information do not provide the scale of computational resources required for world model training and rollouts, nor do they discuss whether there is a systematic analysis of safety/failure modes; this needs to be verified against the full paper.



### Related work

  * Related contemporaneous/follow-up research includes: Sword (arXiv:2605.07288, Style-Robust World Models), which lists WoVR as one of its comparison baselines and points out its weakness in style robustness; World-VLA-Loop (arXiv:2602.06508); and a comprehensive survey on world models for robot learning from May 2026 (arXiv:2605.00080), which classifies WoVR as a representative method of "explicit world model-policy co-evolution." There is also the tutorial-style literature "From World Models to World Action Models" (arXiv:2607.00836).
  * Worth surveying: high. The co-evolution concept proposed by WoVR is already regarded as one of the important paradigms in this field and has been cited/compared by multiple follow-up papers; it is recommended to track it together with Sword and World-VLA-Loop for a more complete comparative view.



### Conclusion

  * Overall assessment: this is a paper of representative significance for the direction of "world models as RL simulators." Its KIR and co-evolution designs target the long-standing core pain point of unreliable world model simulators, with a significant improvement magnitude (+29-30 percentage points on LIBERO), making it worth in-depth reference. However, note that its style robustness has been questioned by a later paper (Sword), so it should not be considered as having fully solved the world model hallucination problem.
  * Relationship to other important papers: WoVR challenges the earlier approach of "assuming the world model is faithful enough to be used directly as a simulator" (as in earlier world-model-based RL work), and is in turn further challenged by Sword regarding its style robustness; it also belongs to the same lineage as World-VLA-Loop, representing the "policy-world model closed-loop co-optimization" approach.
  * Areas for ROCm/AMD to strengthen: the paper focuses on algorithm/framework design and does not mention the specific training hardware platform used (most likely the NVIDIA GPU ecosystem), and does not discuss ROCm compatibility. If AMD wants to reproduce this kind of world-model RL post-training pipeline on the MI300 series, it would need to independently validate the performance and stability of the diffusion/video generation model and RL rollout pipeline on ROCm—this is a clear gap that needs to be addressed.
