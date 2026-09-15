---
layout: paper
title: "Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation"
section: vla
page_id: "1945391543"
permalink: /vla/dual-latent-memory-in-vision-language-action-models-for-robotic-manipulation-1945391543/
---

**Paper** : [Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation (LaMem-VLA)](https://arxiv.org/abs/2607.07608)  
**Source** : arXiv (cs.RO / cs.CV)  
**arXiv ID** : 2607.07608

### Abstract

This paper points out that mainstream VLA models, under the Markov assumption, mainly rely on the current observation to predict actions, making them ill-suited to long-horizon tasks with temporal dependencies. Existing memory-augmented VLA methods either expand the observation window or retrieve history from a memory bank as auxiliary context on the policy side, but in both cases the memory always exists outside the native latent embedding space of VLA inference, preventing historical experience from being fluidly interwoven with multimodal reasoning and action generation. To address this, the authors propose LaMem-VLA, a "latent-memory-native" framework that reconstructs historical experience as latent memory tokens directly interwoven with VLA reasoning. Its core consists of four collaborative components: (i) a curator that organizes historical experience into two complementary memory vaults, short-term and long-term; (ii) a seeker that queries both vaults using multimodal cognition to retrieve context-relevant evidence; (iii) a condenser that reconstructs the retrieved evidence into compact short-term and long-term latent memory tokens; and (iv) a weaver that injects these memory tokens together with the current observation and instruction into a single continuous embedding sequence. By representing, retrieving, and consuming historical experience within the same continuous latent space, LaMem-VLA allows memory to directly participate in VLA reasoning within a bounded context and guide action generation. The authors conduct extensive experiments on SimplerEnv and LIBERO, confirming the superiority of LaMem-VLA.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391543_lamemvla_fig1.png) 

_Figure 1: Comparison of paradigms for memory-augmented VLA models. Unlike prior approaches that store historical experience in an auxiliary memory bank and then consume memory via retrieval, this figure compares the design philosophy and information flow of different memory mechanisms._

![Figure]({{ site.baseurl }}/assets/images/1945391543_lamemvla_fig2.png) 

_Figure 2: LaMem-VLA framework architecture. Given an instruction and the current observation, the vision-language encoder first encodes the input into a multimodal representation, and then a dual-scale latent memory mechanism performs memory writing, retrieval, and fusion, driving action generation._

  * Problem addressed: Existing memory-augmented VLA methods treat memory as "external auxiliary context on the policy side," with memory existing outside the native latent embedding space of VLA, which prevents historical experience from naturally intertwining with multimodal reasoning and action generation, limiting the effective use of memory.
  * Main method: The paper proposes the "latent-memory-native" framework LaMem-VLA, composed of four collaborative components:
    * Curator: organizes historical experience into two complementary memory vaults — a short-term vault and a long-term vault.
    * Seeker: uses current multimodal cognition to query both vaults, retrieving evidence relevant to the current context.
    * Condenser: reconstructs and compresses the retrieved evidence into compact short-term and long-term "latent memory tokens."
    * Weaver: weaves these latent memory tokens together with the current observation and instruction into a single continuous embedding sequence, fed directly into the VLA's reasoning pipeline.
  * Difference from prior approaches: The core difference lies in the "representation space" of memory — this method keeps memory representation, retrieval, and consumption entirely within the same continuous latent space as VLA reasoning ("latent-memory-native"), rather than treating memory as an external module (e.g., textual memory, a separate memory bank) that is spliced into the policy input after the fact as in prior methods. This allows memory to directly and smoothly participate in the reasoning and action-generation process within a bounded context, rather than serving merely as additional context.
  * Description of the key methodological design: This architecture can be envisioned as a "memory production line" — the curator first packages raw historical experience into the short-term/long-term vaults; the seeker actively searches the vaults for relevant evidence based on the current task's needs; the condenser compresses the found evidence into compact latent vectors (rather than retaining the original high-dimensional data); finally, the weaver stitches these compressed memory vectors together with the embedded representations of the current frame and instruction into a continuous sequence, feeding it directly into the VLA's multimodal reasoning backbone, so that memory and current reasoning occupy the same computational space and are seamlessly connected.

### Result

  * Extensive experiments are conducted on two public benchmarks, SimplerEnv and LIBERO. The abstract states that they "demonstrate the superiority" of LaMem-VLA, but does not provide specific quantitative numbers (such as success-rate percentages or relative improvement magnitudes) in the abstract.
  * Fairness: since the abstract does not provide specific experimental data, it is impossible to judge the specific magnitude and persuasiveness of its effect here; the full text needs to be checked for detailed success rates, ablation results, and confirmation of which baselines it was compared against (whether it includes contemporary memory-augmented VLAs such as MemoryVLA or EventVLA).

### Limitation

  * The abstract does not explicitly state limitations. Inferring from the architectural design, the four-stage pipeline (curator → seeker → condenser → weaver) involves multiple retrieval and compression operations, which may introduce additional inference latency; meanwhile, the capacity management and update strategy of the "short-term/long-term vaults" (when old memories are evicted) is not explained in the abstract and needs to be verified in the full text.
  * The absence of specific quantitative results in the abstract is also a transparency limitation of this paper, making it difficult to independently assess its effectiveness and robustness.

### Related work

  * The abstract explicitly frames "existing memory-augmented VLA methods placing memory outside the native latent space" as its critique of prior methods (possibly including explicit textual memory such as Explicit Language Memory, as well as approaches that treat memory as an external retrieval module), implying a challenge/contrast relationship, though it does not name specific papers.
  * This paper is judged to belong to the same 2026 VLA latent-memory research group as MemoryVLA/MemoryVLA++ (which likewise uses token-form latent memory but emphasizes a "perception-cognition" dual track rather than "short-term-long-term") and EventVLA (which emphasizes sparse event memory rather than continuous latent memory); their design philosophies are similar but the detailed approaches differ, making them worth comparing side by side in a survey, so its related work has moderately high survey value.

### Conclusion

  * Overall assessment: The design philosophy of LaMem-VLA — "keeping memory in the same latent space throughout" — has methodological appeal (avoiding the representational gap between memory and reasoning), and its four-stage pipeline (curator/seeker/condenser/weaver) has a clear architecture with well-defined division of labor; however, since the abstract lacks specific quantitative results, its actual effectiveness still needs to be verified in the full text and confirmed through subsequent community reproduction.
  * Relationship to other important papers: this paper, together with MemoryVLA/MemoryVLA++ (perception-cognition memory vaults), EventVLA (sparse event memory), and Explicit Language Memory (explicit textual memory), jointly form a diverse roadmap of 2026 VLA memory-mechanism research; each makes different trade-offs on "memory representation form" (latent vectors vs. text) and "memory organization" (short-term/long-term vs. perception/cognition vs. sparse events), making them suitable to compare side by side under the same survey topic.
  * Gaps regarding ROCm/AMD: the abstract does not mention any hardware platform information. This method involves multi-stage memory retrieval and latent-vector compression operations; the degree of operator support for such non-standard attention/retrieval computations may differ across hardware platforms, but the paper itself provides no measured data or hardware discussion, so no clear connection to ROCm/AMD is apparent; this is speculation, not a conclusion of the paper.
