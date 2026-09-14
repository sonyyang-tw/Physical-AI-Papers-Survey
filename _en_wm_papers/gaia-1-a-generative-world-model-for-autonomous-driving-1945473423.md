---
layout: paper
title: "GAIA-1: A Generative World Model for Autonomous Driving"
section: wm
page_id: "1945473423"
permalink: /en/wm/gaia-1-a-generative-world-model-for-autonomous-driving-1945473423/
---

**Paper** : [GAIA-1: A Generative World Model for Autonomous Driving](https://arxiv.org/abs/2309.17080)  
**Source** : arXiv (Technical Report, Wayve)  
**arXiv ID** : 2309.17080

### Abstract

GAIA-1 (Generative AI for Autonomy) is a generative world model proposed by Wayve for autonomous-driving scene generation. The model takes video, text, and action as three input modalities, casting the world-modeling problem as an unsupervised sequence-modeling problem: inputs are first mapped to discrete tokens, and the next token is predicted autoregressively. The model exhibits emergent properties such as learning high-level scene structure and dynamics, contextual awareness, generalization ability, and understanding of geometric relationships. The authors argue that this kind of representation, which captures expectations about future events, combined with the ability to generate realistic samples, can accelerate and strengthen the training of autonomous-driving technology.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473423_gaia1_fig1.png) 

_Figure 1: GAIA-1 multimodal video generation - future rollouts conditioned on actions._

![Figure]({{ site.baseurl }}/assets/images/1945473423_gaia1_fig2.png) 

_Figure 2: Architecture of GAIA-1 - encoding video/text/action into tokens, autoregressive world model, video decoder._

  * Problem addressed: Autonomous-driving systems need to effectively predict the various potential outcomes the world may evolve into after a vehicle takes an action, but real-world scenes are complex and unstructured, making them difficult to exhaustively model.
  * Main method: Treats world modeling as an unsupervised sequence-modeling problem, mapping video, text, and action inputs into a discrete token space, then training an autoregressive next-token prediction model (similar to the approach used by language models, but applied to multimodal driving data).
  * Difference from previous approaches: Compared with traditional autonomous-driving approaches that use explicit rules or supervised perception-prediction-planning pipelines, GAIA-1 adopts a generative, data-driven approach, learning scene dynamics directly from large-scale video data, and supports fine-grained control of the generated driving scenario via text and action conditioning (e.g., specifying weather, other vehicles' behavior, etc.).
  * Key design: Architecturally, it is divided into a tokenizer/encoder part that encodes raw sensory input (video frames, text, action) into discrete tokens, and a Transformer-like autoregressive world model that performs next-token prediction over the token sequence; at the generation stage, the predicted tokens are then decoded back into video frames, achieving simulation and imagination of future scenes.



### Result

  * The results emphasized in the abstract are mostly qualitative descriptions: the model demonstrates understanding of high-level scene structure and dynamics, contextual awareness, generalization to new scenes, and understanding of geometric relationships, and can generate realistic driving videos with fine-grained control according to text/action input.
  * The abstract itself does not provide specific quantitative metrics (such as FID or visual quality scores); the full text/technical report needs to be consulted for detailed data.
  * Whether it is fair, or whether other papers' results disagree: comparison data on GAIA-1 in other papers (such as GAIA-2 or subsequent autonomous-driving world model papers) needs to be checked, as the abstract does not provide quantitative metrics that can be cross-validated.



### Limitation

  * The paper's abstract does not explicitly state a limitation section.
  * Based on the abstract and the motivation described in the subsequent GAIA-2 paper, it can be inferred that GAIA-1 may have shortcomings in multi-camera consistency, fine-grained control, and multi-agent interaction modeling, which is also what GAIA-2 specifically emphasizes addressing, indicating that GAIA-1's capabilities in these areas are limited.
  * The full text needs to be checked further to understand specific weaknesses such as computational cost, generation resolution, and time-length limits.



### Related work

  * GAIA-2 (arXiv:2503.20523) is the direct successor to GAIA-1, improving on multi-camera consistency, fine-grained control, and multi-agent interaction, and is worth reading alongside as a point of comparison.
  * No other newer research has been found that directly challenges or replaces GAIA-1; but overall, world models/video generation models (such as the NVIDIA Cosmos series and the Genie series) are developing rapidly in the same period, worth surveying further.
  * Degree worth surveying: medium-high. The GAIA series is a representative work of autonomous-driving-specific world models, suitable for comparing architecture and application scenarios with general-purpose world models (Genie, Cosmos).



### Conclusion

  * Overall assessment: GAIA-1 is an early landmark work of generative world models in the autonomous-driving field, successfully transferring LLM-style discrete-token autoregressive modeling to multimodal driving data, which has landmark significance and is worth reading as an introduction to understanding the context of "world models applied to autonomous driving."
  * Relationship with other articles: GAIA-1 pioneered Wayve's GAIA series of world models, subsequently replaced/extended by GAIA-2 (latent diffusion architecture); methodologically, it belongs to a different route from DreamerV3 (RL-oriented world model) and V-JEPA 2 (self-supervised representation-based world model) — GAIA-1 follows the generative token autoregressive route — and can serve as an important case for the methodological classification of world models.
  * ROCm/AMD relevance: The abstract does not mention any specific hardware platform or training infrastructure details, so no clear connection to ROCm/AMD can be found; if this needs to be strengthened, a potential direction AMD could focus on is the training efficiency and ecosystem support of large-scale multimodal sequence models (GPT-like architectures) on ROCm, but this is only speculation, as the paper itself does not touch on this issue.
