---
layout: paper
title: "From World Models to World Action Models: A Concise Tutorial for Robotics"
section: wm
page_id: "1945539286"
permalink: /en/wm/from-world-models-to-world-action-models-a-concise-tutorial-for-robotics-1945539286/
---

**Paper** : [From World Models to World Action Models: A Concise Tutorial for Robotics](https://arxiv.org/abs/2607.00836)  
**Source** : arXiv (not yet designated for a specific conference; accompanied by a GitHub page clearlab-sustech/WorldModelSurvey)  
**arXiv ID** : 2607.00836

### Abstract

This paper does not aim to provide an exhaustive survey, but rather a concise tutorial on "world models" and "world action models" for the field of robotics. After reading this tutorial, readers should clearly understand what constitutes a "world," how world models and world action models are defined, and what roles they play in robotic AI systems. The tutorial also develops a unified perspective for comparing representative approaches, such as World Labs' spatial intelligence model, Yann LeCun's JEPA framework, and NVIDIA's Cosmos platform, clarifying the differences among these models in terms of representation, predictive capability, and interaction mechanisms.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539286_wamtutorial_fig1.png) 

_Figure 1: Illustration of the components of a world._

![Figure]({{ site.baseurl }}/assets/images/1945539286_wamtutorial_fig2.png) 

_Figure 8: Taxonomy of world action models — coupling future observation prediction with robot action generation in different ways._

  * **Problem addressed**: Terms such as "world model" and "world action model" in the field of robotics lack a clear, unified definition and comparative framework, making it difficult for beginners to quickly grasp the core concepts and the differences between representative methods.
  * **Main method**: This paper is presented in tutorial form rather than as an exhaustive survey. It first defines "what constitutes a world," then defines the concepts of world models and world action models, and explains their role in robotic AI systems; finally it establishes a unified comparative perspective for analyzing several representative platforms/frameworks side by side.
  * **Difference from previous approaches**: Unlike the three exhaustive surveys mentioned above (which review large amounts of literature and build taxonomies), this paper is positioned as a "conceptual tutorial," with the goal of helping readers build a clear mental model rather than providing detailed literature coverage; its comparison objects are also more focused on well-known, representative platform-level works (World Labs, JEPA, NVIDIA Cosmos) rather than a broad list of academic papers.
  * **Key design description**: The tutorial's structure is expected to unfold sequentially as follows: (1) the definition and scope of a "world"; (2) the definition of a world model — emphasizing the representational capacity to "predict how the environment will evolve"; (3) the definition of a world action model — building on the world model to further integrate "action," so that the model can not only predict environmental evolution but also connect the prediction to concrete action decisions; (4) using a unified comparative framework to analyze the World Labs spatial intelligence model, LeCun's JEPA (Joint Embedding Predictive Architecture), and the NVIDIA Cosmos platform one by one along three dimensions: representation, predictive capability, and interaction mechanism.



### Result

  * The "result" of this tutorial lies in providing a clear, unified conceptual framework and comparative perspective, helping readers clarify how well-known platforms/frameworks such as World Labs, JEPA, and NVIDIA Cosmos are positioned on the world model spectrum.
  * Whether it is fair: Since this is a tutorial-style article rather than a paper proposing a new method or new experimental results, its "results" lean toward conceptual organization and do not involve quantitative experimental comparisons; whether its comparison of the three platforms is comprehensive and objective needs to be verified against other papers or the technical documentation of these platforms themselves.
  * It is worth noting that the paper has undergone multiple revisions (v1 through v7, spanning July to August 2026), showing that the authors continue to refine the content based on feedback, and also reflecting that concepts in this field are still evolving rapidly.



### Limitation

  * An inherent limitation of tutorial-style articles is that their definitions and classifications are a teaching framework subjectively proposed by the authors, which may not necessarily be equivalent to standard definitions recognized by academia. Readers still need to cross-reference other more rigorous surveys (such as the three surveys in this list) to gain a more comprehensive, peer-reviewed understanding.
  * The paper states itself that it "does not aim to provide an exhaustive survey," so it deliberately makes trade-offs in the breadth of literature coverage; readers who need a complete literature review still need to read other surveys alongside it.
  * The abstract does not provide specific conclusions on the comparison details between World Labs, JEPA, and NVIDIA Cosmos (e.g., which one is more suitable for which task); the full text needs to be checked further to understand the actual judgment results of its comparative framework.



### Related work

  * Directly related to JEPA (the Joint Embedding Predictive Architecture proposed by Yann LeCun), NVIDIA Cosmos (NVIDIA's world foundation model platform), and World Labs' spatial intelligence model — all three are representative world model frameworks currently receiving extremely high attention from industry and academia, worth reading their original technical reports for a deeper understanding.
  * Assessment of the degree to which the related work is worth surveying: medium-high. As a conceptual introductory tutorial, its comparative framework helps quickly build an understanding of mainstream industry world model platforms, but if rigorous technical details and quantitative comparisons are needed, it still needs to be paired with the original papers or other surveys in this list.



### Conclusion

  * This paper, as a "conceptual tutorial" rather than a technical survey, is suitable as introductory reading for quickly building a foundational understanding of world models / world action models, especially for readers who want to quickly understand the differences among the three representative frameworks of World Labs, JEPA, and NVIDIA Cosmos; however, if in-depth technical details or quantitative comparisons are needed, it should still be paired with other more detailed surveys (such as the three surveys in the list) and the original papers of each platform.
  * Relationship with other important articles: The "world model → world action model" evolution proposed in this paper echoes conceptually with other surveys in this list (such as the definition of "action-conditioned prediction systems" in 2606.00113), both emphasizing how "action" is integrated into world models; NVIDIA Cosmos, as one of its comparison objects, is also worth understanding together with NVIDIA's MimicGen (data generation) within the same ecosystem context, as part of NVIDIA's overall layout in the embodied AI world model field.
  * ROCm/AMD relevance: The NVIDIA Cosmos platform mentioned in the paper is clearly built on NVIDIA's software/hardware ecosystem (CUDA, Isaac, etc.), which highlights the current situation in which mainstream world model platforms in the industry are highly tied to the NVIDIA ecosystem; this is a gap worth AMD/ROCm's attention — if a corresponding world foundation model platform is to be developed on ROCm, or at least to ensure that existing open-source world models (such as the open-source parts of Cosmos, the JEPA series) can be trained and inferred on ROCm, resources need to be invested in building corresponding framework compatibility and ecosystem integration. This is a clearly identifiable area for ROCm to strengthen in the embodied AI / world model field.
