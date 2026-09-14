---
layout: paper
title: "How Fast Can I Run My VLA? Demystifying VLA Inference Performance with VLA-Perf"
section: vla
page_id: "1945391760"
permalink: /en/vla/how-fast-can-i-run-my-vla-demystifying-vla-inference-performance-with-vla-perf-1945391760/
---

**Paper** : [A Survey on Efficient Vision-Language-Action Models](https://arxiv.org/abs/2510.24795)  
**Source** : arXiv (cs.CV / cs.AI / cs.LG / cs.RO)  
**arXiv ID** : 2510.24795

### Abstract

This is a comprehensive survey on "Efficient VLA Models." The authors note that while VLA models perform impressively in the field of embodied intelligence, foundational VLA models are often constrained by the high computational and data requirements imposed by their massive architectures. Although a large body of research has focused on improving VLA efficiency, there is a lack of a unified framework to integrate these scattered results. This survey is the first to systematically review the entire "model-training-data" pipeline, proposing a unified taxonomy that organizes existing techniques into three main pillars: (1) efficient model design (architecture and compression), (2) efficient training (reducing training computational burden), and (3) efficient data collection (addressing bottlenecks in acquiring and utilizing robot data). The paper also compiles representative applications, key challenges, and future research directions.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391760_vlaperf_fig1.png) 

_Fig. 1: The transition from Foundational VLA to Efficient VLA. Foundational VLA is constrained by fundamental challenges such as insufficient real-time responsiveness, excessive computational cost, and inefficient data collection; through the three core approaches of efficient model design, efficient training, and efficient data collection, Efficient VLA achieves high-performance deployment on edge devices._

![Figure]({{ site.baseurl }}/assets/images/1945391760_vlaperf_fig2.png) 

_Fig. 3: Overview of VLA models. A VLA integrates a vision encoder to extract visual features, an LLM backbone to fuse multimodal inputs, and an action decoder (MLP-based, autoregressive, or generative) to produce robot control signals, enabling end-to-end vision-language-action reasoning to accomplish embodied manipulation tasks._

  * Problem to be solved: Efficiency-related research in the VLA field is scattered and lacks a unified classification and comparison framework, making it difficult for researchers to grasp overall trends and the trade-offs between different methods.
  * Main method: Proposes a unified taxonomy spanning the entire "model-training-data" pipeline, classifying existing Efficient VLA techniques into three major categories:
    * Efficient Model Design: covers efficient architecture design (such as more streamlined vision-language-action backbones) and model compression techniques (such as quantization, distillation, and pruning).
    * Efficient Training: covers techniques for reducing the computational resources required for training (such as parameter-efficient fine-tuning and mixed-precision training).
    * Efficient Data Collection: covers techniques for addressing the scarcity and high cost of collecting robot demonstration data (such as data augmentation, sim-to-real transfer, and automated data generation).
  * Difference from prior approaches: No previous survey has systematically organized VLA efficiency techniques from a "full-pipeline" perspective (rather than focusing only on model architecture); this paper is the first to integrate the three stages of model design, training, and data into a single classification framework for critical review.
  * Key method design description: This is a survey-type paper rather than one proposing a new architecture; instead, it uses text and diagrams to classify, compare, and summarize efficiency techniques scattered across individual original papers along the three axes above, supplemented with application case studies (such as deployment results on specific robot platforms).

### Result

  * Since this is a survey rather than an original experimental paper, it does not present its own quantitative experimental results; its contribution lies in the systematic organization, classification, and critical comparison of existing literature, summarizing the representative methods and application scenarios currently found in the Efficient VLA field.
  * Whether the results are fair: Since this is a survey, the content depends on the authors' selection and interpretation of the literature; the abstract does not provide specific evaluation data, so it is difficult to judge whether there is selective bias. It needs to be verified against the full text whether the comparisons of various classified methods are fair and whether any important work has been omitted.

### Limitation

  * The abstract does not explicitly state self-identified limitations, but as a survey-type article, its inherent limitations typically include: coverage limited to literature available at the time of writing (this paper's v2 version was updated in February 2026, but technical evolution is rapid and newer methods may not have been included); and the classification scheme is a subjective construction by the authors that may not cover all edge cases.
  * Further verification of the full text is needed to understand the specific challenges and future research roadmap it lists.

### Related work

  * The paper itself is a synthesis of a large body of existing VLA efficiency work; the specific related work it lists requires consulting the full text to determine.
  * The paper provides a continuously updated project page (https://evla-survey.github.io/), indicating that the authors intend to keep tracking the latest developments in this field. This kind of "living document" survey is quite valuable for the rapidly evolving VLA field.
  * This survey is judged to be a worthwhile starting point for both entering and tracking the overall landscape of VLA efficiency techniques, suitable as a map before diving into individual method papers.

### Conclusion

  * Overall assessment: As the first systematic survey on the theme of "Efficient VLA" for 2025-2026, this paper is highly valuable for readers who want to quickly grasp the overall landscape of this field, especially those who care about computational and data efficiency (rather than purely pursuing accuracy), and is well suited as a starting point for literature review.
  * Relationship with other important papers: This paper essentially plays the role of an "aggregator," covering and comparing a large number of original VLA method papers (such as representative VLA models like CogACT and pi-0, as well as various compression/distillation/efficient training technique papers), but the abstract does not specifically name the comparison targets—the full text needs to be consulted to confirm.
  * Assessment of ROCm/AMD gaps: The abstract does not mention discussion of any specific hardware platform (such as GPU vendor, ROCm, or CUDA), so it cannot be determined from the abstract whether this survey touches on efficiency issues at the inference/training hardware level (such as discussing optimizations across different accelerators). If a company is focused on VLA inference efficiency on ROCm, the full text needs to be checked for hardware-level discussion; currently no clear connection is apparent.
