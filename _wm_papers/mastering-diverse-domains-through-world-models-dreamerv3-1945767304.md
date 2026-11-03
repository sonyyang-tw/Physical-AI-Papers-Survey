---
layout: paper
title: "Mastering Diverse Domains through World Models (DreamerV3)"
section: wm
page_id: "1945767304"
permalink: /wm/mastering-diverse-domains-through-world-models-dreamerv3-1945767304/
---

**Paper** : [Mastering diverse control tasks through world models](https://www.nature.com/articles/s41586-025-08744-2) (arXiv preprint: [Mastering Diverse Domains through World Models](https://arxiv.org/abs/2301.04104))  
**Source** : Nature (2025) / arXiv preprint  
**arXiv ID** : 2301.04104

### Abstract

DreamerV3 is a general-purpose reinforcement learning algorithm proposed by Danijar Hafner and colleagues (Google DeepMind) that improves behavior policies by learning a world model of the environment and "imagining" future scenarios within that model. Using a single fixed configuration, it outperforms specialized methods across more than 150 tasks spanning diverse domains (robot manipulation and locomotion, Atari 2D games, and 3D environments such as DMLab and Minecraft), without requiring extensive manual tuning for each new task. Its most representative achievement is being the first algorithm to learn to collect diamonds in Minecraft from scratch, without human data or curriculum design. The work was originally published as an arXiv preprint in 2023 and formally appeared in Nature in April 2025.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767304_dreamerv3_fig1.png) 

_Figure 1: Benchmark summary. Using fixed hyperparameters, Dreamer outperforms tuned expert algorithms across a variety of benchmarks and data budgets, and substantially outperforms PPO; at the same time, Dreamer learns to mine diamonds in Minecraft from scratch using only sparse rewards — a long-standing challenge that previous methods could only solve with human data or domain-specific heuristics._

![Figure]({{ site.baseurl }}/assets/images/1945767304_dreamerv3_fig2.png) 

_Figure 3 (a) World Model Learning: Dreamer's training pipeline. The world model (RSSM) encodes sensory input into discrete representations z_t, predicted by a sequence model with recurrent state h_t conditioned on action a_t; inputs are reconstructed to ensure the representation is informative, and the actor and critic learn actions and values from trajectories predicted in the abstract representation space of the world model._

  * **Problem addressed**: Existing reinforcement learning algorithms can be applied to tasks similar to their training settings, but adapting them to new application domains typically requires substantial human expertise and repeated trial and error to tune hyperparameters. There has been no general-purpose algorithm that works "out of the box" across domains.
  * **Main method**: Dreamer learns a world model of the environment (encoding sensory input into discrete categorical representations and predicting future representations and rewards), and then uses this world model to "imagine" multi-step future trajectories, training an actor-critic policy within this imagined space rather than relying solely on data from interacting with the real environment.
  * **Difference from prior approaches**: DreamerV3 introduces a series of robustness techniques — including normalization, loss balancing, and transformations of values — that allow the same fixed hyperparameter configuration to remain stable across rewards, observation spaces, and action spaces of very different scales, without requiring re-tuning for each domain. This stands in clear contrast to prior RL methods that required extensive domain-specific tuning.
  * **Key design details**: The world model encodes observations using categorical representations and uses a recurrent network to predict future latent representations and rewards. Behavior learning is carried out entirely through gradient updates on imagined latent trajectories, and there is a favorable scaling relationship between model size and both data efficiency and final performance — that is, larger models achieve greater data efficiency and better final results.

### Result

  * **Results**: Using a single fixed configuration, DreamerV3 outperforms domain-specialized methods across more than 150 tasks, spanning highly diverse environments including robot manipulation, locomotion, Atari, DMLab, and Minecraft. Its most representative achievement is on the Minecraft diamond-mining task — widely regarded as a difficult open-world problem requiring long-horizon exploration under pixel-based input and sparse rewards — where DreamerV3 is the first algorithm to complete the task from scratch without human demonstration data or curriculum learning.
  * **Main contributions**: Cross-domain generality (a single configuration applicable across many domains) and data efficiency (larger models directly translate into higher data efficiency and better final performance) are the paper's primary contributions.
  * **Fairness / points requiring verification**: The abstract and news summaries emphasize the overall description of "outperforming specialized methods," but do not provide a detailed cross-domain numerical comparison table. Whether DreamerV3 comprehensively outperforms the best "custom-tailored" specialized method on all 150+ tasks still needs to be verified against the full paper and subsequent reproduction studies (for example, whether it underperforms highly tuned specialized baselines on some subset of tasks).

### Limitation

  * The abstract does not explicitly state a specific limitations section, but based on the paper's positioning, one can infer that the Dreamer series relies on the predictive quality of the world model. If the environment dynamics are highly stochastic or difficult to capture with a compact latent representation (e.g., highly multi-agent or adversarial environments), the imagined trajectories from the world model may deviate from the real environment, affecting policy quality.
  * Further verification of the full text is needed regarding: computational and memory overhead (imagination-based rollout training is typically more computationally expensive than pure model-free RL), and whether performance still falls short of extremely tuned specialized SOTA methods on some tasks.

### Related work

  * DreamerV3 is the third generation of the Dreamer/DreamerV2 series, and represents a landmark extension of the model-based RL world model approach. Unlike GAIA, Genie, Cosmos, and other world models oriented toward generating video/scenes, DreamerV3 focuses more on the goal of "using a world model to improve the efficiency of RL policy learning."
  * No clear, direct successor work replacing DreamerV3 has been found so far (based on current search results), but the research direction combining model-based RL with world models remains active, and it is worth watching for future Dreamer variants that integrate large vision-language models.
  * **Assessment of how worth surveying this related work is**: High. DreamerV3 is an important milestone at the intersection of reinforcement learning and world models, and is well suited for methodological comparison with V-JEPA 2-AC (which also involves using world models for planning/control).

### Conclusion

  * **Overall assessment**: DreamerV3 is a highly influential general-purpose algorithm in the field of reinforcement learning. Its achievements — "a single configuration across multiple domains" and the "Minecraft diamond task" — are highly significant and worth serious reference, especially for researchers interested in how world models can improve sample efficiency and generalization.
  * **Relationship to other work**: Compared to the GAIA series, Genie 3, Cosmos 3, and other world models focused on generating video/interactive environments, DreamerV3 follows a route of "using world models to assist policy optimization." The two can be seen as different branches of world model application (generative simulation vs. decision-making/planning). Compared to V-JEPA 2-AC, both pursue planning with a learned world model, but DreamerV3 uses pixel-level/categorical representation-based reconstruction modeling, whereas V-JEPA 2 uses joint-embedding prediction (without pixel reconstruction) self-supervised representations.
  * **ROCm/AMD relevance**: The paper's abstract and technical reports do not mention the specific hardware platform or training infrastructure used, so no clear connection to ROCm/AMD can be identified. If this needs to be strengthened, one possible direction is to evaluate the training throughput and stability of Dreamer-style world models (including recurrent networks and actor-critic imagination-based training) on ROCm, but this is speculative and not addressed in the paper itself.
