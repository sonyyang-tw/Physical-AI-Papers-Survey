---
layout: paper
title: "MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation"
section: vla
page_id: "1945363954"
permalink: /en/vla/memoryvla-perceptual-cognitive-memory-in-vision-language-action-models-for-robot-1945363954/
---

**Paper** : [MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation](https://arxiv.org/abs/2508.19236)  
**Source** : arXiv (cs.RO / cs.CV), ICLR 2026  
**arXiv ID** : 2508.19236

### Abstract

This paper points out that robot manipulation tasks are inherently "non-Markovian," requiring temporal context to make correct decisions, yet mainstream VLA models typically ignore this, resulting in poor performance on long-horizon, temporally dependent tasks. Inspired by cognitive science—where humans rely on working memory to buffer short-term representations for real-time control, while the hippocampal system preserves verbatim episodic details and semantic gist of past experience to form long-term memory—the authors propose MemoryVLA, a "Cognition-Memory-Action" framework. A pretrained VLM encodes observations into perceptual and cognitive tokens forming working memory, while a "Perceptual-Cognitive Memory Bank" stores low-level details and high-level semantics extracted and consolidated from them. Working memory retrieves decision-relevant entries from the memory bank, adaptively fuses them with current tokens, and updates the memory bank by merging redundant information. Finally, these tokens condition a memory-guided diffusion action expert to produce temporally-aware action sequences.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945363954_memoryvla_fig1.png) 

_Figure 1: Motivating illustration. (a) In tasks like pressing a button, the visual state before and after the operation is nearly identical, highlighting the necessity of temporal modeling. (b) Humans process manipulation tasks through a dual memory system: perceptual memory and cognitive memory working in tandem._

![Figure]({{ site.baseurl }}/assets/images/1945363954_memoryvla_fig2.png) 

_Figure 2: Overall MemoryVLA architecture. RGB observations and language instructions are encoded by a 7B VLM into perceptual and cognitive tokens, forming short-term working memory, which is retrieved, fused, and consolidated via the Perceptual-Cognitive Memory Bank (PCMB), ultimately driving action decoding._

  * Problem addressed: robot manipulation tasks are inherently non-Markovian; VLA models that rely only on the current observation struggle with long-horizon tasks requiring reasoning dependencies across time steps.
  * Main method: proposes a three-stage Cognition-Memory-Action framework:
    * Cognition: a pretrained VLM encodes the current observation into "perceptual tokens" (low-level visual detail) and "cognitive tokens" (high-level semantics), which together form working memory.
    * Memory: a Perceptual-Cognitive Memory Bank stores low-level details and high-level semantics consolidated from past interactions; working memory queries this memory bank, retrieving entries relevant to the current decision and adaptively fusing them with current tokens; the memory bank itself is continuously updated by merging redundant entries.
    * Action: the fused tokens condition a "memory-conditioned diffusion action expert," which outputs temporally consistent action sequences.
  * Differences from prior approaches: compared to mainstream VLA models that make decisions based only on the current observation, this method explicitly emulates the human dual-track cognitive architecture of "working memory + long-term episodic/semantic memory," and integrates memory retrieval and fusion mechanisms directly into the action generation pipeline, rather than simply concatenating past frames into the input window.
  * Key method design description: the architecture can be imagined as a three-layer pipeline—input images/language are processed by the VLM to produce two types of tokens; these tokens simultaneously form immediate working memory and query an external memory bank for cross-temporal retrieval; the retrieved memory is fused with current working memory, then updated back into the memory bank through redundancy merging, forming a continuously evolving memory system; finally, this set of temporally-aware tokens enters the diffusion model to decode the action sequence.



### Result

  * Evaluated on more than 150 simulation and real-world tasks across three robot platforms. Simulation benchmarks: SimplerEnv-Bridge 71.9%, Fractal 72.7%, LIBERO-5 96.5%, Mikasa-Robo 41.2% success rate, all surpassing the state-of-the-art baselines CogACT and pi-0, leading by +14.6 on Bridge and +11.8 on Mikasa-Robo.
  * On 12 real-world tasks covering both general skills and long-horizon time-dependent scenarios, it achieves an 84.0% success rate, with long-horizon tasks improving by +26 compared to the strongest baseline.
  * Fairness: the comparison targets in the abstract are explicit (CogACT, pi-0), and the numbers are specific and come from multiple standard benchmarks (SimplerEnv, LIBERO, Mikasa-Robo), giving reasonable credibility; however, since this is a self-evaluation by the original authors, it still needs verification against whether other papers (such as follow-up MemoryVLA++ or EventVLA) reproduce these numbers differently or raise questions.



### Limitation

  * The abstract does not explicitly state limitations; the full text needs to be checked for discussion of potential bottlenecks such as memory bank scale growth, retrieval latency, or memory fusion accuracy.
  * Based on the follow-up paper MemoryVLA++ (by the same author group, June 2026), it can be inferred that MemoryVLA itself only handles "memory" (looking back at the past) and lacks "imagination" (predicting future states)—a gap explicitly identified and addressed by MemoryVLA++, which also indirectly reflects that MemoryVLA itself may still have limitations on tasks requiring forward-looking planning.



### Related work

  * There is a known newer follow-up study: the same author group published MemoryVLA++ (arXiv:2606.09827) in June 2026, adding a "world model-style imagination" mechanism on top of MemoryVLA's memory mechanism—a direct extension relationship worth tracking as a priority.
  * This series (MemoryVLA → MemoryVLA++) is judged to represent a main line of research in VLA memory mechanisms, worth including as a key reading in the survey.



### Conclusion

  * Overall assessment: this paper proposes a cognitive-science-inspired, well-structured memory framework, achieving significant and specific performance improvements on multiple public benchmarks and real robots (particularly the +26 improvement on long-horizon tasks, which is quite substantial). It is an important representative work in the direction of VLA memory research, worth referencing.
  * Relationship to other important papers: this paper explicitly uses CogACT and pi-0 as comparison baselines (challenge/surpass targets), and is itself later extended by the same author group as MemoryVLA++ (adding world model imagination capability); papers such as EventVLA and LaMem-VLA also implicitly list this type of "memory bank" method as a comparison target in their abstracts (e.g., EventVLA mentions the information bottleneck problem of existing memory-augmented methods).
  * ROCm/AMD gaps to address: the abstract does not mention any specific hardware or framework information. The diffusion-based action expert and VLM encoder in this method may have considerable inference latency requirements; this type of memory bank retrieval and fusion mechanism requires low-latency execution on real robots. If deploying on the ROCm platform, one may need to evaluate operator support and optimization for diffusion model iterative decoding and memory retrieval operations, but the abstract itself does not provide sufficient information to support this—it is speculative rather than a conclusion drawn by the paper.
