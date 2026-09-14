---
layout: paper
title: "Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)"
section: wm
page_id: "1945392511"
permalink: /en/wm/other-vehicle-trajectories-are-also-needed-a-driving-world-model-unifies-ego-oth-1945392511/
---

**Paper** : [Other Vehicle Trajectories Are Also Needed: A Driving World Model Unifies Ego-Other Vehicle Trajectories in Video Latent Space (EOT-WM)](https://arxiv.org/abs/2503.09215)  
**Source** : arXiv (cs.CV / cs.AI)  
**arXiv ID** : 2503.09215

### Abstract

EOT-WM is a world model for autonomous driving that focuses on simultaneously controlling the trajectories of both the "ego vehicle" and "other vehicles," in order to generate more realistic driving simulation videos. The authors point out that advanced end-to-end autonomous driving systems predict the motion of other vehicles while planning the ego vehicle's trajectory, but existing world models mostly only emphasize controllability of the ego vehicle's trajectory, leaving the motion of other vehicles uncontrollable, which makes it difficult to realistically simulate interactions between the ego vehicle and its surrounding environment. EOT-WM first projects the trajectories of the ego vehicle and other vehicles from BEV (bird's-eye-view) space into image coordinates, matching trajectories to the corresponding vehicles in the video via pixel positions; it then uses a Spatial-Temporal VAE to encode the trajectory videos, aligning them spatially and temporally with the latent representation of the driving video; and it designs a trajectory-injected diffusion Transformer to denoise the noisy latent video and generate the output video. The authors also propose a new metric based on controlled latent similarity to evaluate trajectory controllability. Experiments on the nuScenes dataset show that this method improves FID by 30% and FVD by 55% relative to SOTA methods, and can use its own generated trajectories to predict previously unseen driving scenarios.

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392511_eotwm_fig1.jpg) 

_Figure 1: EOT-WM can generate more realistic videos, and can simultaneously control the trajectories of the ego vehicle and other vehicles, with these trajectories represented in video space._

![Figure]({{ site.baseurl }}/assets/images/1945392511_eotwm_fig2.jpg) 

_Figure 2: Schematic diagram of the EOT-WM architecture._

  * **Problem addressed**: Existing driving world models can only controllably generate the ego vehicle's trajectory, while the motion of other vehicles is uncontrollable (random or data-distribution-dependent), making it impossible to realistically simulate interaction scenarios between the ego vehicle and other traffic participants, which limits the credibility of world models as simulators for evaluating autonomous driving systems.
  * **Main method**: EOT-WM (Ego-Other vehicle Trajectories World Model) unifies control of ego and other vehicle trajectories within the same video latent space. The core consists of three parts:
    * Video-based Trajectory Representation (VTR): projects each vehicle's (ego and other) trajectory from BEV space into the image coordinate system, matching trajectories to the corresponding vehicles in the video frames via pixel positions.
    * Aligned Motion Guidance Generation (AMGG): uses a Spatial-Temporal VAE to encode these "trajectory videos" so they align spatially and temporally with the latent representation of the driving video itself.
    * Trajectory-injected Diffusion Transformer (TiDiT): uses a diffusion Transformer to denoise the noisy video latent, injecting trajectory guidance signals during the denoising process to generate a controlled driving video.
  * **Difference from prior approaches**: Previous methods (e.g., using only ego trajectories or waypoints as conditioning) neglect the controllability of other vehicles, causing the behavior of other vehicles in the simulation to become disconnected from real interactions. EOT-WM converts the trajectories of multiple vehicles into a unified visual latent space, allowing the generative model to simultaneously "understand" the motion intentions of both the ego vehicle and other vehicles.
  * **Key design details**: The model is built on top of CogVideoX (a text/image-to-video diffusion model). In addition to the original driving video, the input includes a set of trajectory videos (visualizing the future trajectory of each vehicle as a trajectory layer positioned according to the image coordinate system). These trajectory videos are aligned with vehicle identities via VTR, encoded into latent tensors of the same dimensionality as the driving video via AMGG, and TiDiT jointly feeds the trajectory latents and video latents into the Transformer at each step of the diffusion denoising process, progressively denoising to generate the final driving video — so the trajectory conditioning can simultaneously influence the motion trajectories of the ego vehicle and every other vehicle in the frame.

### Result

  * **Main results**: On the nuScenes dataset, compared to the SOTA method at the time, FID improved by 30% and FVD improved by 55%. A new metric (based on controlled latent similarity) was proposed to evaluate trajectory controllability, showing high fidelity of trajectory control. In addition, the model can use its own generated trajectories to predict previously unseen driving scenarios, demonstrating a certain degree of generalization ability.
  * **Contributions**: The main contributions are enhanced "video generation quality" (large improvements in FID/FVD) and "multi-vehicle trajectory controllability," which is the core differentiating advantage over previous methods that only controlled ego vehicle trajectories.
  * **Fairness**: The FID/FVD improvement percentages provided in the abstract are results of the authors' own comparisons; the specific baseline(s) being compared against are not stated, and no third-party or subsequent paper has independently verified these numbers. It is necessary to check whether other papers (e.g., subsequent driving world model benchmark papers) have cross-validated or presented differing views on EOT-WM's results.

### Limitation

  * **Limitations stated by the authors**: Based only on the arXiv abstract page, the abstract itself does not list an explicit limitations section.
  * **Weaknesses inferred from the results**:
    * The method relies on BEV-to-image projection and pixel-position matching, which may become unstable in heavily occluded or densely overlapping vehicle scenes, though the abstract does not discuss this situation.
    * The method is only validated on nuScenes (a single dataset with specific sensor configurations and region), so its generalization across datasets or sensor configurations is unknown.
    * The paper has undergone multiple revisions (v1 to v4, spanning March to November 2025), which may reflect adjustments to the method or evaluation during the review process, though the specific changes cannot be determined from the abstract alone.

### Related work

  * According to web searches, this research direction already has follow-up work, such as "EgoExo-WM: Unlocking Exo Video for Ego World Models" (2026) and "Ego-Dynamics-Augmented World Model for Autonomous Driving with Zero-Shot Cross-Chassis Adaptation," showing that the driving world model field continues to move toward richer viewpoint fusion and cross-vehicle generalization. In addition, a survey published in October 2025, "A Comprehensive Survey on World Models for Embodied AI" (arXiv:2510.16732), cites this paper and can serve as a quick entry point for understanding the overall landscape of this field.
  * **How worth surveying this related work is**: High. This field (controllability and multi-agent interaction simulation in driving world models) continues to see new work published, and the above survey is recommended for quickly locating other related methods for comparison.

### Conclusion

  * **Overall assessment**: EOT-WM proposes a clear architectural solution (VTR + AMGG + TiDiT) to the specific and practical problem of "uncontrollable other-vehicle trajectories," with a significant improvement in FID/FVD. It is a worthwhile reference in research on driving world model controllability, especially for its engineering-reproducible technique of projecting trajectories into image coordinates.
  * **Relationship to other important papers**: This work builds on the line of driving world model research based on video diffusion models such as CogVideoX, and challenges the limitation of previous methods that could "only control ego vehicle trajectories." It continues to evolve in the same context as subsequent works such as EgoExo-WM and Ego-Dynamics-Augmented World Model.
  * **ROCm/AMD gaps**: The abstract does not mention the hardware platform or framework details used for training/inference, so no clear connection to ROCm/AMD can be identified, and it would not be appropriate to speculate. If a team wants to reproduce this type of CogVideoX-based diffusion Transformer training pipeline on AMD hardware, they would need to separately verify the ROCm support status of the CogVideoX series of models.
