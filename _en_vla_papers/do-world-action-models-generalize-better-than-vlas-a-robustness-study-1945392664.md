---
layout: paper
title: "Do World Action Models Generalize Better than VLAs? A Robustness Study"
section: vla
page_id: "1945392664"
permalink: /en/vla/do-world-action-models-generalize-better-than-vlas-a-robustness-study-1945392664/
---

**Paper** : [Do World Action Models Generalize Better than VLAs? A Robustness Study](https://arxiv.org/abs/2603.22078)  
**Source** : arXiv (cs.RO)  
**arXiv ID** : 2603.22078

### Abstract

This paper provides an empirical test of the widely assumed claim that "World Action Models (WAMs) generalize better than traditional VLAs." The authors point out that robot action planning requires not only understanding the environment's current state but also predicting how the environment will evolve in response to actions; VLA has achieved considerable success by combining large-scale vision-language models with an action expert, but its performance is limited by the scope of its training data, resulting in limited generalization to unseen scenarios and fragility to various situational perturbations. Recently, world models have been re-proposed as an alternative — the so-called WAM — built on top of world models trained on large volumes of video data to predict future states, which after minor adjustment can decode their latent representations into robot actions; it has been argued that their explicit dynamics-prediction ability, combined with spatiotemporal priors gained from web-scale video pretraining, allows WAMs to generalize better than VLAs. This paper compares several representative SOTA VLA policies against recently released WAMs on two benchmarks, LIBERO-Plus and RoboTwin 2.0-Plus, under a variety of visual and language perturbations.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392664_wamvla_robust_fig1.png) 

_Figure 1: Examples of perturbations on RoboTwin 2.0-Plus tasks. (Definitions of the various noise N, lighting L, and other perturbation codes are detailed in the paper's Appendix A.)_

![Figure]({{ site.baseurl }}/assets/images/1945392664_wamvla_robust_fig3.png) 

_Figure 3: Examples of future images predicted by Cosmos-Policy. Shows a comparison between ground-truth images (GT) and Cosmos-Policy's predicted images (Pred.) under three types of perturbation in LIBERO-Plus (noise, lighting, background changes), illustrating the dynamics-prediction ability of its world model._

  * **Problem addressed**: Testing an industry-popular but as-yet rigorously unverified hypothesis — whether WAMs really generalize better than VLAs and are more resistant to visual/language perturbations.
  * **Main method**: This is an empirical comparative study (a robustness study), not a new-model paper:
    * Selects several representative SOTA VLA policies (e.g., π_0.5) and recently released WAMs (e.g., LingBot-VA, Cosmos-Policy).
    * Evaluates them on two benchmarks, LIBERO-Plus and RoboTwin 2.0-Plus, which are extended versions of the original LIBERO / RoboTwin 2.0 benchmarks with "various visual and language perturbations" added, used to test model robustness under out-of-distribution (OOD) conditions.
    * Systematically compares the change in success rate across different model families under perturbation, thereby testing whether WAM's claimed generalization advantage over VLA actually holds.
  * **Difference from prior approaches**: Previous claims that WAM is superior to VLA have mostly been theoretical speculation (based on WAM's explicit dynamics prediction and web-video priors); this paper is the first to empirically test this hypothesis using a systematic perturbation benchmark, rather than merely comparing standard (unperturbed) task success rates.

### Result

  * WAMs show stronger robustness: LingBot-VA achieves a 74.2% success rate on RoboTwin 2.0-Plus, and Cosmos-Policy achieves an 82.2% success rate on LIBERO-Plus.
  * VLAs (e.g., π_0.5) can also achieve similar robustness on some tasks, but typically require larger, more diverse robot datasets and diversified learning objectives to do so.
  * Fairness: this is an independent third-party comparative study (not self-reported by the model proposers), which is more objective than self-reported results in single-model papers, and is one of the few papers on this list specifically addressing the question of whether other papers' results hold up. Still, it should be noted that the choice of which VLAs/WAMs to compare and whether the benchmark design itself favors a particular class of methods could affect the generality of the conclusions; it is recommended to verify the specific list of perturbation types and the breakdown of each model's performance under each perturbation type in the full text, and whether evaluation code has been released (the authors mention that the RoboTwin2.0-Plus evaluation code has been released) for others to reproduce.

### Limitation

  * Self-stated limitations: the abstract emphasizes that "for VLA to achieve similar robustness, it typically requires large and diverse robot training data and diversified learning objectives," implying this is a limitation of the VLA camp rather than WAM being inherently superior; but this may also reflect that WAM's relative advantage in low-data scenarios is merely conditional (i.e., depends on whether VLA has sufficient data).
  * From the results: even the best-performing WAMs (Cosmos-Policy 82.2%, LingBot-VA 74.2%) still do not achieve success rates close to 100%, showing that even though WAMs are relatively robust, there is still a significant failure rate under strong perturbations; which specific perturbation types (visual vs. language) cause larger drops needs to be verified in the full text.

### Related work

  * This paper is highly complementary in topic to "World Action Models: The Next Frontier in Embodied AI" (2605.12090) on this list: the former is a classification/naming survey, the latter is an empirical test; it is recommended to read them together.
  * No direct follow-up research updating this paper has been found so far (within the current search scope); but its open evaluation code (RoboTwin2.0-Plus) may be cited by follow-up papers as a standard comparison benchmark, worth continued tracking.
  * Degree to which it merits surveying: high. As one of the few papers to empirically test the popular hypothesis that "WAM is superior to VLA," it has high reference value for researchers who want to objectively assess the value of the WAM paradigm.

### Conclusion

  * Overall assessment: highly worth referencing. This is a comparative study providing empirical evidence rather than merely theoretical claims, helping avoid overly optimistic interpretations of the WAM paradigm, and is an important reference for assessing whether to invest in the WAM direction.
  * Relationship to other papers: this paper directly tests the core hypothesis mentioned in survey articles such as "World Action Models: The Next Frontier in Embodied AI" (2605.12090) — that WAM has advantages in dynamics prediction and video priors — and compares specific models such as π_0.5 (VLA), LingBot-VA, and Cosmos-Policy (WAM), which can be seen as a balancing verification of the optimistic narrative in this field.
  * ROCm/AMD relevance: no clear connection to ROCm/AMD is apparent from the abstract's content, as the paper does not mention the hardware platform used for training/inference; however, since the models mentioned in the paper (especially Cosmos-Policy, which may be related to the NVIDIA Cosmos platform) are mostly developed and evaluated within the NVIDIA ecosystem, this also indirectly indicates that the evaluation and deployment toolchain in the WAM field is currently predominantly NVIDIA-based. If AMD/ROCm wants to enter this field, it may need to strengthen compatibility support for the corresponding video diffusion models and robot policy evaluation toolchains (this is an inferred observation, not an explicit conclusion of the paper).
