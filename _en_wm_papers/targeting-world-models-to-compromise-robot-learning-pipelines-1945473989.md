---
layout: paper
title: "Targeting World Models to Compromise Robot Learning Pipelines"
section: wm
page_id: "1945473989"
permalink: /en/wm/targeting-world-models-to-compromise-robot-learning-pipelines-1945473989/
---

**Paper** : [Targeting World Models to Compromise Robot Learning Pipelines](https://arxiv.org/abs/2606.09499)  
**Source** : arXiv (cs.RO, cs.AI, cs.CR), CoRL Preprint  
**arXiv ID** : 2606.09499

### Abstract

World models have grown rapidly in recent years and are viewed as a more data-efficient tool for generating robot training data or simulating real-world environments, with many studies proposing to integrate them into robot learning pipelines. However, this paper demonstrates that world models introduce a particularly stealthy and effective data poisoning entry point into the robot learning supply chain — even when the training data itself appears safe, it can still lead to the deployment of unsafe or poisoned robot policies. Unlike traditional data poisoning techniques (directly embedding dangerous trajectories into datasets that are sold or uploaded), this paper proposes new attack methods that inject malicious prompts or compromising transition dynamics into "seemingly safe" teleoperated datasets. This malicious content is only "activated" after the data is fed into a world model, generating synthetic, dangerous robot training trajectories, ultimately leading to unsafe or poisoned robot policies. The authors demonstrate the effectiveness of the attack against both action-conditioned and text-conditioned state-of-the-art world models, and show a complete end-to-end backdoor attack on downstream deep reinforcement learning (DRL) policies, while also providing a proof-of-concept for VLA scenarios. These findings suggest the need to research safer world models and to re-evaluate their position within the robot learning supply chain.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945473989_wmattack_fig1.png) 

_Figure 1: Diagram of the "Visual Prompt Hijacking" attack, targeting text-conditioned world models, using a malicious prompt to overwrite the user's original prompt, causing the generation of dangerous learning trajectories that propagate to downstream robot policies._

![Figure]({{ site.baseurl }}/assets/images/1945473989_wmattack_fig2.png) 

_Figure 2: Visualization of the threat model. A malicious data provider targets the world model within the robot learning pipeline, embedding dangerous behavior or altered transition dynamics into otherwise safe teleoperated data, thereby poisoning the downstream robot policy while bypassing dataset-level safety checks._

  * **Problem addressed**: World models are widely used to generate robot training data, but this stage itself may become a new entry point for supply chain attacks — even if the original teleoperated dataset "looks" clean and safe, attackers can still covertly produce dangerous synthetic training data through this intermediary stage of the world model.
  * **Main method**: Two new types of attack techniques are proposed:
    * Injecting compromising transition dynamics into "action-conditioned world models," causing them to generate dangerous trajectories under specific trigger conditions.
    * Injecting malicious prompts into "text-conditioned world models," similarly producing problematic output only when activated under specific conditions.
    * The key characteristic of the attack is its "stealthiness": the original dataset itself appears safe under manual or standard inspection, and the malicious behavior only manifests during the stage when the data flows through the world model to generate synthetic data, making traditional dataset-level safety checks difficult to detect.
    * The authors further demonstrate a complete end-to-end backdoor attack: from a poisoned world model → generating synthetic training data containing backdoor trigger patterns → training a downstream DRL policy → the policy exhibiting attacker-implanted unsafe behavior under specific trigger conditions. A proof-of-concept is also provided for VLA (Vision-Language-Action) settings.
  * **Difference from prior approaches**: Traditional data poisoning directly places dangerous trajectories into the dataset itself, which can potentially be detected by inspecting the dataset (e.g., anomaly detection). This paper's attack hides the "poison" within the world model's generation logic or trigger mechanism, rather than in the surface content of the dataset, meaning the dataset itself passing a safety review cannot guarantee the safety of downstream training data — a completely new attack surface tailored to the emerging robot learning paradigm of "model as data generator."
  * **Key design details**: The attack process can be understood as follows: an attacker gains access to or influences the world model's training/fine-tuning process → implants a trigger (which may be a specific action sequence pattern or a specific text prompt fragment) → the world model appears normal externally, and only generates dangerous/shifted synthetic trajectories when it encounters the trigger condition → downstream developers use this synthetic data to train DRL or VLA policies → the policy executes unsafe behavior when the trigger condition appears, forming an end-to-end backdoor.

### Result

  * The attack is demonstrated to be effective against both action-conditioned and text-conditioned state-of-the-art world models.
  * A complete end-to-end backdoor attack on downstream DRL policies is fully demonstrated (successfully propagating the backdoor from the world model all the way through to the final policy behavior).
  * A proof-of-concept for VLA settings is provided, indicating that the attack surface is not limited to traditional RL policies but may also extend to currently mainstream VLA models.
  * The abstract does not provide specific attack success rates or quantitative data; verification of the experimental section of the full paper is needed to understand the strength of the attack's effect under different trigger rates/poisoning ratios.
  * **Fairness**: This is a security/attack research paper, and its threat model assumptions (that the attacker can influence world model training or fine-tuning) are not detailed in the abstract; verification of the full paper's threat model section is needed to understand the access requirements and real-world feasibility of the attack, to avoid overestimating or underestimating its threat level.

### Limitation

  * The abstract does not mention specific limitations stated by the authors, but based on the nature of attack research, it can be inferred that its threat model may assume the attacker has a certain degree of access to model training/the supply chain — the real-world feasibility of this needs to be verified against the full paper's threat model section.
  * The VLA scenario is only a "proof-of-concept" rather than a fully demonstrated end-to-end case, meaning its attack effectiveness and generalizability on more complex, real-world deployment-oriented VLA systems still need further verification.

### Related work

  * This is a relatively novel topic focused on "world model security." No clear newer follow-up research proposing defenses against this attack or expanding the attack surface has been found so far, but this topic (world model supply chain security) forms an interesting contrast with other contemporaneous papers emphasizing world model capabilities (such as WoVR, Interactive World Simulator) — the latter assume world models are a trustworthy data source, while this paper directly challenges that assumption.
  * **How worth surveying this related work is**: Medium-high, especially for researchers in robot learning security or AI supply chain security, this is a newly emerging threat category worth attention; for engineers purely focused on world model capability research, this paper provides an important risk-awareness perspective.

### Conclusion

  * **Overall assessment**: This is a security research paper proposing an entirely new attack surface, carrying important cautionary significance — it reminds the industry that when world models are widely integrated into robot learning pipelines (as advocated by papers such as WoVR, Interactive World Simulator, and Cosmos), the world model itself can also become a covert entry point for supply chain attacks. This is a risk aspect easily overlooked in the current enthusiasm for "using world models to accelerate robot data generation," and is worth reference for all engineers working in this field.
  * **Relationship to other important papers**: This paper can be seen as a challenge and complementary perspective to positive-application papers such as WoVR and Interactive World Simulator that treat world models as robot training data/simulators — those papers assume the data generated by world models is trustworthy, while this paper proves that this assumption itself can be exploited by attackers.
  * **ROCm/AMD gaps**: The paper focuses on algorithmic-level attack/security research and does not involve any specific hardware platform or ROCm-related content, so no clear connection to ROCm can be identified. However, if AMD is promoting world model/robot learning solutions on its own hardware, this paper is a reminder that when building a complete robot learning supply chain (including the world model stage), security review and model provenance trustworthiness verification should also be included as platform-level considerations.
