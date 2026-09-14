---
layout: paper
title: "Robots Need More than VLA and World Models"
section: vla
page_id: "1945392804"
permalink: /en/vla/robots-need-more-than-vla-and-world-models-1945392804/
---

**Paper** : [Robots Need More than VLA and World Models](https://arxiv.org/abs/2606.06556)  
**Source** : arXiv (cs.RO), a position paper  
**arXiv ID** : 2606.06556

### Abstract

This is a position paper arguing that "general-purpose robot intelligence" is currently over-simplified into a "policy-scaling" problem — that is, collecting more robot demonstration data, training larger VLA models, and hoping for broader generalization. The authors argue that this framing is incomplete: the real core bottleneck is not merely policy learning itself, but the lack of mechanisms to convert the vast amount of unstructured behavioral data in the world into usable robot supervision signals. Human actions, internet videos, simulated rollouts, and interactive demonstrations contain rich information about tasks, goals, contacts, failures, and physical constraints, but most of this information cannot be directly used by robot policies because it lacks "embodiment-specific action labels," "task semantics," and "reward structure." The authors propose four missing components for next-generation robot systems: a data interface (for automatically labeling unstructured behavior), an embodiment interface (for retargeting human actions into robot actions), a world-model interface (for physically grounded 3D reasoning), and a reward interface (for inferring task progress and success from video and language).

### Method

![Figure]({{ site.baseurl }}/assets/images/1945392804_robots_need_more_fig1.png) 

_Figure 1: The next generation of robotics will come from progress that goes far beyond simply scaling up vision-language-action (VLA) models._

  * **Problem addressed**: the current mainstream industry narrative on "general-purpose robot intelligence" simplifies the problem into a scaling issue of "more data + bigger VLA models = better generalization," but the authors argue that the real bottleneck lies in the lack of "interface" mechanisms for converting the world's abundant unstructured behavioral data (human actions, internet videos, simulated rollouts, interactive demonstrations) into supervision signals usable by robots.
  * **Main method (essentially a position argument plus a research agenda proposal, rather than a new model)**: the authors identify four "missing components" and review existing progress for each:
    * **Data interfaces**: for autolabelling unstructured behavioral data so it can be used by robot policies.
    * **Embodiment interfaces**: for retargeting human actions into the action space of a specific robot.
    * **World-model interfaces**: providing physically grounded 3D reasoning capability.
    * **Reward interfaces**: inferring task progress and success from video and language, establishing reward/evaluation signals.  
The authors survey recent progress in robot foundation models, cross-embodiment datasets, learning from video, world models, reward modeling, and related areas for each component, and propose a research agenda arguing that robot systems should learn not only from robot demonstrations, but from the broader physical-world data.
  * **Difference from prior approaches**: unlike technical routes that simply "scale up VLA" or "add a world model," this paper points out from a systemic perspective that even with better policy models or world models, if there is no interface mechanism to convert "unstructured world data" into "structured robot supervision signals," such data still cannot be effectively used; the paper therefore argues that priority should be given to building these four types of interfaces.

### Result

  * As a position paper, there are no experimental results or benchmark data; its "output" is a four-component research agenda framework, along with a survey of existing progress in each related area (robot foundation models, cross-embodiment datasets, video learning, world models, reward modeling).
  * Fairness assessment: since this is a position paper rather than an empirical study, the question of whether specific experimental results agree with other papers does not apply; however, whether its argument is comprehensive and fair depends on whether its survey of related work has notable bias or omissions, which needs to be checked against the full paper's scope of citations.

### Limitation

  * Limitations stated by the authors: as a position paper, its nature is to propose a research agenda that still needs to be validated, rather than to provide solutions to already-solved problems; the four "interfaces" themselves remain open problems yet to be built, and the paper does not claim to have already solved them.
  * Weaknesses inferred from the content: the persuasiveness of a position paper depends on the quality of its argument rather than empirical data; readers need to judge for themselves whether the proposed four-component taxonomy is complete, or whether it omits other important bottlenecks (such as safety, long-horizon planning, multi-robot collaboration, etc.), which the abstract does not cover.

### Related work

  * The core argument of this paper directly challenges the object explicitly targeted by "Robots Need More than VLA and World Models" in this list, including research that relies on the VLA scaling narrative (implicitly challenging the existing VLA route of simply stacking more data and larger models); it also overlaps with the "World Action Models" related survey (2605.12090) on the viewpoint that "world models are part of robot intelligence," but this paper argues that world models alone are still insufficient, and that additional data/embodiment/reward interfaces are needed.
  * No newer related research directly extending this position paper has been found within the scope of this search.
  * Survey value: medium-high. As a critical reflection on the popular narrative that "VLA + world models alone can solve general-purpose robot intelligence," it is suitable reading material for establishing a macro research perspective before diving into technical details.

### Conclusion

  * Overall assessment: worth referencing, especially as a high-level perspective supplement for understanding the limitations of the VLA/WAM technical route. It offers no concrete technical solution, but points out a systemic bottleneck (the data-conversion interface) that the industry may be overlooking, providing reference value for planning long-term research directions.
  * Relationship to other papers: this paper offers a critical supplementary perspective — "even if these technologies are all perfected, it still won't be enough" — to papers in this list that emphasize scaling and architectural innovation (such as LeVERB, ChainFlow-VLA, and WAM-related papers), arguing that data, embodiment, world-model, and reward interfaces must also work together; it can be viewed as a "meta-reflection" on the entire VLA/WAM technical route.
  * ROCm/AMD relevance: no clear connection to ROCm/AMD can be seen from the abstract; the paper makes no mention whatsoever of specific hardware or frameworks, being purely a research-direction argument, so it would be inappropriate to force such a connection.
