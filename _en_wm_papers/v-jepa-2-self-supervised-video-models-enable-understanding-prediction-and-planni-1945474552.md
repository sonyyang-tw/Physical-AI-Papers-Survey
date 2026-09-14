---
layout: paper
title: "V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning"
section: wm
page_id: "1945474552"
permalink: /en/wm/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planni-1945474552/
---

**Paper** : [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning](https://arxiv.org/abs/2506.09985)  
**Source** : arXiv (Meta FAIR / Mila)  
**arXiv ID** : 2506.09985

### Abstract

V-JEPA 2 is a self-supervised video model proposed by Meta FAIR that combines web-scale video data with a small amount of robot interaction data to understand, predict, and plan behavior in the physical world. The research team first pretrained an action-label-free joint-embedding-predictive architecture (JEPA) on over 1 million hours of web video and image data, achieving performance that surpasses previous task-specific models on action understanding (top-1 accuracy of 77.3 on Something-Something v2) and human action anticipation (recall-at-5 of 39.7 on Epic-Kitchens-100); after aligning with a large language model, it also achieved then-state-of-the-art performance at the 8-billion-parameter scale on multiple video question-answering tasks. Next, using fewer than 62 hours of unlabeled robot video (from the Droid dataset), the team post-trained an action-conditioned latent world model, V-JEPA 2-AC, achieving zero-shot pick-and-place task planning on Franka robotic arms in two different labs, without collecting any data in the deployment environment or performing task-specific training or reward design.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474552_vjepa2_fig1.png) 

_Figure: V-JEPA 2 abstract overview diagram — self-supervised pretraining on video and image data, combined with a small amount of robot data to train an action-conditioned world model._

![Figure]({{ site.baseurl }}/assets/images/1945474552_vjepa2_fig2.png) 

_Figure 1: V-JEPA 2 Overview — a visual mask denoising video model architecture pretrained on 1M hours of web video and 1M images._

  * **Problem addressed**: A major challenge for modern AI is how to understand the world and learn to act primarily through observation, rather than relying on large amounts of labeled action-supervised data or large-scale real robot interaction data (the latter being costly and difficult to scale).
  * **Main method**: Two stages — (1) self-supervised pretraining with an action-label-free JEPA architecture on over 1 million hours of web video and images to obtain the V-JEPA 2 encoder, learning to represent predictable scene content while ignoring unpredictable pixel-level details that generative models tend to emphasize; (2) after freezing the V-JEPA 2 encoder, training a new action-conditioned predictor, V-JEPA 2-AC, using fewer than 62 hours of unlabeled robot video, allowing the model to predict the representation of the next frame based on robot proprioception and actions.
  * **Difference from prior approaches**: Unlike generative video models that target pixel-level reconstruction (such as diffusion models), the JEPA architecture makes predictions in a learned representation space, focusing only on the predictable parts of the scene while ignoring unpredictable visual noise details, allowing it to more effectively leverage web-scale, action-label-free video data; moreover, the amount of robot data needed to train V-JEPA 2-AC (less than 62 hours) is far less than what is typically required for imitation learning or reinforcement learning.
  * **Key design details**: V-JEPA 2-AC's training combines a standard single-step teacher-forcing loss with a multi-step rollout loss, to reduce error accumulation during multi-step planning; at deployment, the model can use image goals as the basis for planning, directly completing pick-and-place tasks through model inference without task-specific training or reward function design.

### Result

  * **Results**: V-JEPA 2 surpasses previous task-specific models on action understanding and human action anticipation tasks (Something-Something v2 top-1 of 77.3; Epic-Kitchens-100 recall-at-5 of 39.7); after aligning with a language model, it achieves then-state-of-the-art performance at the 8-billion-parameter scale on video question-answering tasks such as PerceptionTest (84.0) and TempCompass (76.9). V-JEPA 2-AC achieves zero-shot pick-and-place on Franka robotic arms in two different labs; in tests using uncalibrated, low-resolution RGB cameras and restricting sampled actions to a specific radius, V-JEPA 2-AC achieves an average 80% success rate for cup pick-up and relocation tasks, compared to 15% for the video-language-action baseline model Octo; planning speed is also significantly faster, requiring only 16 seconds per action, compared to 4 minutes for the video-generation-based Cosmos model.
  * **Main contributions**: Data efficiency (a world model capable of planning can be obtained with only a small amount of robot data), zero-shot cross-environment generalization, and planning speed (significantly faster than generative video world models) are the paper's main contributions.
  * **Fairness / points requiring verification**: The comparison data with Octo and Cosmos comes from the paper's own experimental design (specific tasks, specific test environments); whether it generalizes to a broader range of robot manipulation tasks and more complex scenarios still needs verification through subsequent independent reproduction or third-party evaluation studies; the "4 minutes vs. 16 seconds" planning time comparison also needs to be confirmed as being conducted under the same hardware and same task settings for both methods, to ensure fairness of the comparison.

### Limitation

  * Although the paper's abstract does not list a detailed limitations section, the method design suggests that V-JEPA 2-AC's currently validated tasks are concentrated on relatively simple manipulation tasks such as pick-and-place, and the sampled actions are restricted to a specific radius, suggesting that the model's capability on more complex, larger action spaces or fine manipulation tasks remains to be validated.
  * The approach relies on post-training with a frozen V-JEPA 2 encoder, meaning the quality of the model's representations depends heavily on whether the visual representations learned during pretraining cover the visual and physical concepts needed for the target robot task. If the target task involves objects or interaction types rare in the pretraining data, this may affect zero-shot generalization performance — this point needs further verification against the full paper and whether subsequent research has discussed it.

### Related work

  * V-JEPA 2 continues the JEPA (joint-embedding predictive architecture) concept proposed by Yann LeCun, and is an extended version of the V-JEPA series; Meta has mentioned that a subsequent V-JEPA 2.1 was released in 2026, improving dense feature learning, and it is worth further tracking and verifying the technical details.
  * Compared with Cosmos (NVIDIA) and other video-generation-based world models, V-JEPA 2 represents an important example of the "non-generative, representation-predictive" world model route. The comparative advantages and disadvantages of the two routes (generative vs. representation-predictive) in physical world modeling and robot planning is a direction worth deep surveying.
  * **Assessment of how worth surveying this related work is**: High. V-JEPA 2-AC's planning efficiency and zero-shot generalization ability have high practical reference value for embodied AI/robot policy learning applications, and it forms a meaningful three-way comparison methodologically with DreamerV3 (RL-style imagination planning) and Cosmos (generative world model planning).

### Conclusion

  * **Overall assessment**: V-JEPA 2 and its V-JEPA 2-AC world model demonstrate that "self-supervised representation learning + a small amount of robot data" can produce a world model with zero-shot planning capability, which is significant for data-scarce robot application scenarios and is worth serious reference, especially its notable efficiency advantage in planning speed compared to generative world models (such as Cosmos).
  * **Relationship to other work**: V-JEPA 2-AC forms a methodological three-way comparison with Octo (an imitation-learning-based VLA model) and Cosmos (a generative world model), both directly compared in the paper; compared with DreamerV3, both pursue "using a world model to support planning/control," but V-JEPA 2 adopts non-reconstructive joint-embedding prediction, while DreamerV3 adopts categorical representation-based reconstruction modeling — two representative endpoints on the methodological spectrum of world models.
  * **ROCm/AMD relevance**: The body of the paper (only the abstract and some technical details were read this time) does not mention the specific training hardware platform, but it does mention that "compared to the Cosmos model requiring 4 minutes to generate a plan, V-JEPA 2-AC only needs 16 seconds," implying the importance of planning efficiency for real-time robot control applications. If AMD/ROCm wants to find an entry point in embodied AI planning inference, lightweight, non-generative representation-predictive models like V-JEPA 2 (compared to large generative world models) may be more suitable for small-to-medium-scale deployment in terms of inference latency and hardware resource requirements, but this is only speculation, as the paper itself does not discuss support for any specific hardware platform.
