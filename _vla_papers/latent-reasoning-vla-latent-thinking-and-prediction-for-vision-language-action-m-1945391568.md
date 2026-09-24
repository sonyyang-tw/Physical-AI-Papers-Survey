---
layout: paper
title: "Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models"
section: vla
page_id: "1945391568"
permalink: /vla/latent-reasoning-vla-latent-thinking-and-prediction-for-vision-language-action-m-1945391568/
---

**Paper** : [Latent Reasoning VLA: Latent Thinking and Prediction for Vision-Language-Action Models](https://arxiv.org/abs/2602.01166)  
**Source** : arXiv, Accepted by ICML 2026  
**arXiv ID** : 2602.01166

### Abstract

Vision-Language-Action (VLA) models can benefit from Chain-of-Thought (CoT) reasoning, but existing approaches incur high inference latency overhead and rely on discrete reasoning representations (text/visual tokens) that mismatch with continuous perception and control signals. This paper proposes Latent Reasoning VLA (LaRA-VLA), a unified VLA framework that internalizes multimodal CoT reasoning into a continuous latent representation for embodied action generation. LaRA-VLA performs reasoning and prediction simultaneously in latent space, requiring no explicit CoT text generation at inference time, thereby enabling efficient, action-oriented control. To realize this latent embodied reasoning, the authors propose a curriculum-based training paradigm that gradually transitions from explicit text/visual CoT supervision to latent reasoning, ultimately allowing the latent reasoning dynamics to condition action generation. The authors constructed two structured CoT datasets and validated the approach on simulation benchmarks and long-horizon real-robot manipulation tasks, showing that LaRA-VLA consistently outperforms current state-of-the-art VLA methods while reducing inference latency by up to 90% compared to explicit CoT methods.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391568_lara_vla_fig1.png) 

_Figure 1: Comparison of CoT forms — (a) text CoT explicitly generates reasoning tokens; (b) most visual CoT represents reasoning via discrete visual target tokens; (c) LaRA-VLA internalizes both text and visual reasoning into a continuous latent representation._

![Figure]({{ site.baseurl }}/assets/images/1945391568_lara_vla_fig2.png) 

_Figure 2: Overview of the LaRA-VLA method architecture — training proceeds in three stages: (i) explicit CoT fine-tuning while aligning visual prediction latents with inverse dynamics representations, (ii) a latentization stage, and (iii) an action learning stage._

  * **Problem addressed**: Explicit CoT-VLA methods (e.g., generating a chain of text reasoning) are effective but slow down inference, and the text/discrete-token form of reasoning is mismatched with the continuous nature of visual perception and continuous action control.
  * **Main method**: LaRA-VLA "internalizes" multimodal CoT reasoning into a continuous latent vector representation, allowing the model to simultaneously perform "thinking" (latent thinking) and "prediction" in latent space; at inference time it skips the explicit text CoT generation step and produces actions directly from the latent reasoning state.
  * **Differences from prior approaches**: Existing CoT-VLA methods (e.g., DeepThinkVLA, which follows an explicit text CoT + RL alignment route) still require actually generating a text or visual reasoning chain at inference time, incurring latency; LaRA-VLA instead makes reasoning "implicit," using explicit CoT supervision only during training to gradually guide the model to express its reasoning process via latent vectors, requiring no textual output at inference time.
  * **Architecture/pipeline description**: Training adopts a three-stage curriculum: (1) first train with explicit text and visual CoT supervision so the model learns "how to reason"; (2) gradually transition and compress this explicit reasoning into a continuous latent representation; (3) in the final stage, let the latent reasoning dynamics directly condition the action generation module, completing an end-to-end "latent thinking → action" pipeline. The training data includes two structured CoT datasets built by the authors.



### Result

  * LaRA-VLA comprehensively outperforms current state-of-the-art VLA methods on simulation benchmarks and long-horizon real-robot manipulation tasks.
  * Inference latency is reduced by up to 90% compared to explicit CoT-based methods.
  * The abstract does not provide specific quantitative figures such as task success rates; the full text needs to be checked for detailed data. The paper has been accepted at ICML 2026, indicating it has passed peer review.
  * Fairness: the claim of "consistently outperforming SOTA" in the abstract needs verification against whether other papers (e.g., DeepThinkVLA) report comparable figures on the same benchmarks, as they may use different benchmarks or task settings requiring further cross-checking.



### Limitation

  * The abstract does not explicitly list limitations, but it can be inferred from the method design that: while "latentizing" reasoning reduces latency, it may sacrifice a degree of interpretability (one can no longer directly read the model's reasoning process as with explicit CoT); this point is not mentioned in the abstract, and the full text needs to be checked for any discussion of the interpretability/debuggability tradeoff.
  * Curriculum-based training requires a multi-stage process that gradually transitions from explicit to latent reasoning, which may involve higher training complexity and greater data/compute requirements; the abstract does not provide specific training cost information.



### Related work

  * The abstract mentions comparison with "current state-of-the-art VLA methods" but does not list specific paper names, which may include explicit CoT-VLA methods such as DeepThinkVLA.
  * No newer related research was found (this paper itself is a relatively recent work, submitted in February 2026, revised in May, and accepted at ICML 2026).
  * Worth surveying related work: high. This paper and DeepThinkVLA offer two different solutions to the question of "whether CoT is effective for VLA" — "explicit CoT + RL causal alignment" versus "latent CoT" — reading both together provides a fairly comprehensive understanding of the current divergence in technical approaches in this field, well worth an in-depth comparison.



### Conclusion

  * This paper proposes a concrete solution (latent reasoning) to the practical pain point of VLA inference latency, and has been accepted at ICML 2026, giving it a degree of academic recognition; it is worth referencing, especially for readers concerned with real robot deployment latency/real-time performance.
  * Relationship to other important papers: this paper forms an interesting contrast with DeepThinkVLA (paper 1 on the list) — DeepThinkVLA argues that explicit CoT + causal alignment (RL) is necessary for reasoning to be truly effective, while LaRA-VLA argues that "internalizing" reasoning into a latent representation balances effectiveness and efficiency. The two can be seen as a debate between "explicit vs. implicit" reasoning routes, well worth studying together to judge which tradeoff better suits a given application scenario.
  * Relevance to ROCm/AMD: this paper focuses on reducing inference latency to support real-time control, a topic potentially related to papers on inference efficiency/deployment such as VLA-Perf and EcoVLA (papers 5 and 6 on this list), but the abstract does not mention specific hardware platforms or frameworks, so no direct technical connection to ROCm/AMD can be discerned; the full text's experimental hardware environment (whether primarily NVIDIA GPUs) needs to be checked.
