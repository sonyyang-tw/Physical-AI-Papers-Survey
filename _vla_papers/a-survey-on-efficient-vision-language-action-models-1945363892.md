---
layout: paper
title: "A Survey on Efficient Vision-Language-Action Models"
section: vla
page_id: "1945363892"
permalink: /vla/a-survey-on-efficient-vision-language-action-models-1945363892/
---

**Paper** : [A Survey on Efficient Vision-Language-Action Models](https://arxiv.org/abs/2510.24795)  
**Source** : arXiv (cs.CV / cs.AI / cs.LG / cs.RO)  
**arXiv ID** : 2510.24795

### Abstract

This is a comprehensive survey on "Efficient VLAs" (efficient Vision-Language-Action models). The authors point out that although VLA models have shown impressive performance in embodied intelligence, foundational VLA models are often constrained by the heavy computational and data demands of their large-scale architectures. While a large body of research has already focused on improving VLA efficiency, there is no unified framework integrating these scattered efforts. This survey provides the first systematic review across the entire "model-training-data" pipeline, proposing a unified taxonomy that organizes existing techniques into three pillars: (1) efficient model design (architecture and compression), (2) efficient training (reducing the computational burden of training), and (3) efficient data collection (addressing the bottleneck of acquiring and utilizing robot data). The paper also compiles representative applications and key challenges, and lays out future research directions.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945363892_survey_fig1.png) 

_Fig. 1: The transition from Foundational VLA to Efficient VLA. Foundational VLAs are constrained by fundamental challenges such as insufficient real-time performance, excessive computational cost, and low data-collection efficiency; through the three core approaches of efficient model design, efficient training, and efficient data collection, Efficient VLA achieves high-performance deployment on edge devices._

![Figure]({{ site.baseurl }}/assets/images/1945363892_survey_fig2.png) 

_Fig. 3: Overview of VLA models. A VLA integrates a vision encoder to extract visual features, an LLM backbone to fuse multimodal inputs, and an action decoder (MLP-based, autoregressive, or generative) to produce robot control signals, achieving end-to-end vision-language-action reasoning to complete embodied manipulation tasks._

  * Problem addressed: Efficiency-related research in the VLA field is scattered and lacks a unified classification and comparison framework, making it difficult for researchers to grasp overall trends and the trade-offs among different methods.
  * Main method: The paper proposes a unified taxonomy spanning the entire "model-training-data" pipeline, dividing existing Efficient VLA techniques into three broad categories:
    * Efficient Model Design: covers efficient architecture design (e.g., leaner vision-language-action backbones) and model compression techniques (e.g., quantization, distillation, pruning, etc.).
    * Efficient Training: covers techniques that reduce the computational resources required for training (e.g., parameter-efficient fine-tuning, mixed-precision training, etc.).
    * Efficient Data Collection: covers techniques addressing the scarcity and high cost of robot demonstration data (e.g., data augmentation, sim-to-real transfer, automated data generation, etc.).
  * Difference from prior approaches: No previous survey has systematically organized VLA efficiency techniques from a "full-pipeline" perspective (rather than focusing solely on model architecture); this is the first paper to integrate model design, training, and data into a single classification framework for critical review.
  * Description of the key methodological design: This is a survey paper rather than one proposing a new architecture. It uses text and figures to classify, compare, and summarize efficiency techniques scattered across many original papers along the three axes above, supplemented with application case studies (e.g., deployment results on specific robot platforms).

### Result

  * Since this is a survey rather than an original experimental paper, it does not present its own quantitative experimental results; its contribution lies in the systematic organization, classification, and critical comparison of existing literature, and in summarizing representative methods and application scenarios in the Efficient VLA field.
  * Fairness: As a survey, its content depends on the authors' selection and interpretation of the literature. This abstract does not provide specific evaluation data, so it is difficult to judge whether there is selective bias; it would be necessary to verify in the full text whether the comparisons across categories are fair and whether important work has been omitted.

### Limitation

  * The abstract does not explicitly state self-identified limitations, but as a survey-type article, its inherent limitations typically include: coverage limited to literature available as of the writing deadline (this paper's v2 was updated in February 2026, but the technology is evolving quickly, so newer methods may not be included), and the classification system being a subjective construction by the authors that may not cover all edge cases.
  * Further verification of the full text is needed to understand the specific challenges and future research roadmap it lists.

### Related work

  * The paper itself is a synthesis of a large body of existing VLA efficiency work; the specific related work it lists would need to be checked in the full text.
  * The paper provides a continuously updated project page (https://evla-survey.github.io/), indicating the authors intend to keep tracking the latest developments in this field. This type of "living document" survey is quite valuable for the rapidly evolving VLA field.
  * This survey is judged to be a valuable starting point for gaining an overview of and tracking the full landscape of VLA efficiency techniques, suitable as a map before diving into individual method papers.

### Conclusion

  * Overall assessment: As the first systematic survey on "efficient VLA" in 2025-2026, this paper is a very valuable reference for readers who want to quickly grasp the overall landscape of the field, especially those concerned with computational and data efficiency (rather than purely pursuing accuracy), and is suitable as a starting point for literature review.
  * Relationship to other important papers: This paper essentially plays the role of an "aggregator," covering and comparing a large number of original VLA method papers (e.g., representative VLA models such as CogACT and pi-0, as well as various compression/distillation/efficient-training technique papers), but the abstract does not specifically name the papers compared; the full text would need to be checked to confirm.
  * Assessment of gaps regarding ROCm/AMD: The abstract does not mention any specific hardware platform (e.g., GPU vendor, ROCm, CUDA), so it cannot be determined from the abstract whether this survey touches on efficiency issues at the inference/training hardware level (e.g., whether optimizations across different accelerators are discussed). If a company is focused on VLA inference efficiency on ROCm, it would be necessary to verify whether the full text addresses hardware-level considerations; no clear connection is apparent at this time.
