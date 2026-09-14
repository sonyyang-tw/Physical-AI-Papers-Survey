---
layout: paper
title: "LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction"
section: vla
page_id: "1945539712"
permalink: /en/vla/leverb-humanoid-whole-body-control-with-latent-vision-language-instruction-1945539712/
---

**Paper** : [LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction](https://arxiv.org/abs/2506.13751)  
**Source** : arXiv (cs.RO)  
**arXiv ID** : 2506.13751

### Abstract

LeVERB is the first latent vision-language instruction framework designed for humanoid Whole-Body Control (WBC). Existing VLA systems typically assume a precise low-level controller and a hand-designed action "vocabulary" (such as end-effector poses or root velocities), restricting them to quasi-static tasks and preventing them from performing the agile whole-body motions required by humanoid robots. The authors make two contributions: (1) the first sim-to-real, vision-language-enabled, closed-loop humanoid WBC benchmark, covering more than 150 tasks across 10 major categories; (2) the LeVERB framework itself, a hierarchical "latent action vocabulary" system, in which a high-level vision-language policy learns a latent action vocabulary from synthetically rendered human motion demonstrations, while a low-level, reinforcement-learning-trained WBC policy converts these latent instructions into dynamics-level control commands.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539712_leverb_fig1.png) 

_Figure 1: Overview of the paper's contributions — the top shows a photorealistic and dynamically accurate humanoid vision-language whole-body control benchmark; the middle shows a dual-process VLA model trained purely on synthetic data and deployed zero-shot in the real world; the bottom shows an overview of the model architecture, which decouples vision-language processing from dynamics-level action processing._

![Figure]({{ site.baseurl }}/assets/images/1945539712_leverb_fig2.png) 

_Figure 2: Details of the data collection and training pipeline. Step 1: collect a synthetic photorealistic dataset of retargeted motions in IsaacSim and annotate it with text instructions; Step 2: train LeVERB-VL with a motion trajectory reconstruction task to obtain a normalized latent verb vocabulary and cache the latent verb for each trajectory in the dataset; Step 3: condition LeVERB-A on this latent verb, where the model is distilled from a teacher tracking policy via DAgger._

  * **Problem addressed**: Existing VLA models assume a precise, hand-designed action vocabulary (such as end-effector poses), which is suitable only for quasi-static manipulation tasks and cannot cover the highly dynamic whole-body control required by humanoid robots (e.g., coordinated walking, fall recovery, whole-body manipulation, and locomotion).
  * **Main method**: LeVERB adopts a two-layer (System 2 / System 1) hierarchical architecture.
    * High level (System 2): a vision-language policy that uses a CVAE (conditional variational autoencoder) architecture to learn a structured "latent action vocabulary" space, aligning visual and language inputs to a unified latent action distribution, rather than relying on manually defined action primitives.
    * Low level (System 1): a reinforcement-learning-trained whole-body control (WBC) reactive controller that takes the latent "verb" output from the high level and converts it into concrete control commands at the robot dynamics level.
  * **Differences from prior approaches**: Previous hierarchical VLA methods typically used a hand-designed, discrete, and semantically limited action interface between high and low levels (such as end-effector target points); LeVERB replaces this interface with a learned continuous latent space, so that the action vocabulary itself is learned from data and can express richer, more dynamic whole-body behaviors.
  * **Key design**: To address the scarcity of robot-specific visual data, the authors built a data synthesis pipeline: collecting diverse human motions, retargeting them onto the humanoid robot, and rendering them photorealistically in randomized scenes, then using a VLM to annotate semantically similar language instructions, thereby producing paired "robot-specific video-language" data to train the high-level VLA.



### Result

  * On the authors' own benchmark, LeVERB achieves an 80% zero-shot success rate on simple visual navigation tasks, with an overall average success rate of 58.5%, 7.8x higher than a naive hierarchical VLA implementation.
  * The team also demonstrated dynamics-level zero-shot sim-to-real transfer on a real Unitree G1 humanoid robot.
  * Fairness: since the benchmark is self-built by the authors (there is no independent, large-scale third-party reproduction of these numbers on the same benchmark yet), and the comparison baseline is mainly a "naive hierarchical VLA implementation" implemented by the authors themselves, whether this comparison is representative requires verification against other papers or subsequent benchmark results.



### Limitation

  * The paper itself: the details found so far show a high reliance on the synthetic data pipeline (human motion retargeting and rendering); a domain gap between real and synthetic data may exist, and the abstract does not explicitly mention how the authors quantify this gap.
  * From the results, the overall success rate of 58.5% indicates a substantial failure rate remains in most (non-simple-navigation) task categories, suggesting complex whole-body manipulation tasks remain challenging for this framework; the full text needs to be checked for specific failure modes (e.g., which task categories perform worst).



### Related work

  * There is known follow-up research that directly builds on LeVERB's latent action concept: WholeBodyVLA (arXiv 2512.11047, ICLR 2026), titled "Towards Unified Latent VLA for Whole-Body Loco-Manipulation Control," which extends the approach to unified whole-body loco-manipulation control.
  * Worth surveying: medium-high. This field (humanoid whole-body VLA) is developing rapidly and already has direct follow-up work; it is recommended to track WholeBodyVLA and other whole-body control research based on latent action vocabularies.



### Conclusion

  * Overall assessment: worth referencing. LeVERB's idea of replacing hand-designed action interfaces with a "latent action vocabulary" is a concrete, sim-to-real-validated solution to combining humanoid whole-body control with VLA, and has already produced follow-up research (WholeBodyVLA), showing its methodology has influence.
  * Relationship to other papers: LeVERB challenges the traditional hierarchical VLA assumption of a precise low-level controller and hand-designed action vocabulary; its follow-up work WholeBodyVLA further extends this concept.
  * ROCm/AMD relevance: no clear connection to ROCm/AMD can be discerned from the abstract's content; the paper does not mention the specific training/inference hardware platform or framework details. To assess feasibility of training/deployment on AMD hardware, the full text's model scale, training infrastructure, and latency requirements would need to be checked.
