---
layout: paper
title: "Let It Be Simple: One-Step Action Generation for Vision-Language-Action Models"
section: vla
page_id: "1945767397"
permalink: /en/vla/let-it-be-simple-one-step-action-generation-for-vision-language-action-models-1945767397/
---

**Paper** : [Mastering diverse control tasks through world models](https://www.nature.com/articles/s41586-025-08744-2)（arXiv preprint: [Mastering Diverse Domains through World Models](https://arxiv.org/abs/2301.04104)）  
**Source** : Nature（2025）／arXiv preprint  
**arXiv ID** : 2301.04104

### Abstract

DreamerV3 is a general-purpose reinforcement learning algorithm proposed by Danijar Hafner and colleagues (Google DeepMind), which improves its behavior policy by learning a world model of the environment and "imagining" future scenarios within that model. A single configuration can outperform specialized methods across more than 150 tasks spanning diverse domains (robot manipulation and locomotion, Atari 2D games, DMLab, and 3D environments like Minecraft), without requiring extensive manual tuning for each new task. Its signature achievement is being the first algorithm to learn to mine diamonds in Minecraft from scratch, without human data or curriculum design. This research was originally published as an arXiv preprint in 2023, and was formally published in the journal Nature in April 2025.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767397_letitbesimple_fig1.png) 

_Figure 1: Benchmark summary. Using fixed hyperparameters, Dreamer outperforms tuned expert algorithms across multiple benchmarks and data budgets, and substantially outperforms PPO; at the same time, Dreamer learns to mine diamonds in Minecraft from scratch using only sparse rewards, a long-standing challenge that previously required human data or domain-specific heuristics to solve._

![Figure]({{ site.baseurl }}/assets/images/1945767397_letitbesimple_fig2.png) 

_Figure 3 (a) World Model Learning: Dreamer's training pipeline. The world model (RSSM) encodes sensory input into a discrete representation z_t, predicted by a sequence model with recurrent state h_t conditioned on action a_t; inputs are reconstructed to ensure the representation carries sufficient information, while the actor and critic learn action and value functions from trajectories of abstract representations predicted by the world model._

  * Problem addressed: Existing reinforcement learning algorithms, while usable for tasks similar to their training scenario, typically require substantial human expertise and repeated trial and error to tune hyperparameters when applied to a new application domain, lacking a general-purpose algorithm that works "out of the box" across domains.
  * Main method: Dreamer learns a world model of the environment (encoding sensory input into discrete categorical representations, and predicting future representations and rewards), then uses this world model to "imagine" multi-step future trajectories, training an actor-critic policy within the imagined space rather than relying solely on data from interacting with the real environment.
  * Differences from prior approaches: DreamerV3 introduces a series of robustness techniques—including value normalization, loss balancing, and transformations—that allow the same fixed set of hyperparameters to stably operate across rewards, observation spaces, and action spaces of vastly different scales, without needing to be retuned for each domain. This stands in clear contrast to previous RL methods that required extensive domain-specific tuning.
  * Key design: The world model encodes observations using categorical representations, and uses a recurrent network to predict future latent representations and rewards; behavior learning takes place entirely through gradient updates on imagined latent trajectories. There is a favorable scaling relationship between model size, data efficiency, and final performance—that is, larger models yield better data efficiency and final results.



### Result

  * Results: DreamerV3, with a single fixed configuration, outperforms domain-specialized methods across more than 150 tasks, spanning highly diverse environments including robot manipulation, locomotion, Atari, DMLab, and Minecraft. Its most representative achievement is on the Minecraft diamond-mining task—a widely recognized challenge requiring long-horizon strategy exploration under pixel input and sparse rewards—where DreamerV3 is the first algorithm to complete the task from scratch without human demonstration data or curriculum learning.
  * Main enhancements: cross-domain generality (a single configuration applicable across multiple domains) and data efficiency (increasing model size directly translates into higher data efficiency and final performance) are the paper's main contributions.
  * Fairness/points requiring verification: the abstract and news summaries emphasize an overall description of "outperforming specialized methods," but do not provide a detailed cross-domain numerical comparison table; whether DreamerV3 fully outperforms the best specialized method "tailor-made for each task" across all 150+ tasks still requires checking the full paper and subsequent reproduction studies (e.g., whether a subset of tasks show slightly lower performance than highly tuned specialized baselines).



### Limitation

  * The abstract does not explicitly state a specific limitations section, but based on the paper's positioning, it can be inferred that: the Dreamer series relies on the quality of the world model's predictions; if the environment dynamics are highly stochastic or difficult to capture with a compact latent representation (e.g., highly multi-agent or adversarial environments), the imagined trajectories from the world model may deviate from the real environment, thereby affecting policy quality.
  * Further verification of the full text is needed to understand: the computational and memory overhead (imagination-based rollout training is typically more compute-intensive than pure model-free RL), and whether the method still underperforms extremely tuned specialized SOTA methods on some tasks.



### Related work

  * DreamerV3 is the third generation of the Dreamer/DreamerV2 series, a representative extension of the model-based RL world model line; unlike GAIA, Genie, Cosmos, and other world models oriented toward generating video/scenes, DreamerV3 focuses more on "using a world model to improve RL policy learning efficiency."
  * No clear directly-replacing follow-up research to DreamerV3 was found (as of the current search results), but the research direction combining model-based RL with world models remains active, and it is worth watching for a next-generation Dreamer variant that integrates large vision-language models.
  * Assessment of how much this related work merits surveying: high. DreamerV3 is a significant milestone at the intersection of reinforcement learning and world models, suitable for methodological comparison with V-JEPA 2-AC (which also involves using world models for planning/control).



### Conclusion

  * Overall assessment: DreamerV3 is a highly influential general-purpose algorithm in the field of reinforcement learning; its achievements of "a single configuration across multiple domains" and the "Minecraft diamond task" are highly indicative, well worth serious reference, especially for researchers concerned with improving sample efficiency and generalization via world models.
  * Relationship to other papers: Compared with GAIA series, Genie 3, Cosmos 3, and other world models focused on generating video/interactive environments, DreamerV3 takes the route of "using a world model to assist policy optimization"; the two can be seen as two different branches of world model applications (generative simulation vs. decision planning). Compared with V-JEPA 2-AC, both pursue planning with a learned world model, but DreamerV3 uses pixel-level/categorical representation reconstruction-based modeling, while V-JEPA 2 uses joint embedding prediction (without reconstructing pixels) self-supervised representation.
  * ROCm/AMD relevance: the paper's abstract and technical reports do not mention the specific hardware platform or training infrastructure used, so no clear connection to ROCm/AMD can be discerned; if reinforcement is needed, one could speculate about evaluating the training throughput and stability of Dreamer-style world models (including recurrent networks and actor-critic imagination-based training) on ROCm, but this is speculative and not addressed by the paper itself.
