---
layout: post
title: SERI MATS Submission
date: 2023-05-03 12:12:12 -0400
categories:
---

In this post, I'll be writing my submission to the 2023 Summer SERI MATS cohort in the "[Deceptive Alignment](https://www.serimats.org/deceptive)" and "[Evaluating dangerous capabilities](https://www.serimats.org/evals)" and "[Aligning language models](https://www.serimats.org/aligning-language-models)" tracks.

In the interest of time, I won't be attempting a solution to the optional Problem 3, although it seems like an interesting thing to work on in the future.

This document is pretty informal. I'm out of practice with formal academic writing, and it'd probably be a waste of time for me to focus too much on latex formatting + formal writing style instead of improving my ideas.

## Problem 1

> Briefly summarize the most important (according to you) arguments in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" without using any terminology specific to that paper.

_Risks from Learned Optimization in Advanced Machine Learning Systems_ includes the following claims:

1. It is likely that present or future machine learning systems that train models to perform complex tasks or operate in varied environments will produce models that internally search over a space of possible action plans (as opposed to following a set of heuristics). In this article, I'll call such systems _planning agents_ (because they're agents that plan).
   > **Note**
   > Hubinger et al use the term "Mesa Optimizer", which refers to a more rigorous, general concept -- any system that performs optimization and is optimized by another system. I could create a different term for the same concept, like "intra searcher" (my first draft), but I'm interested in relaxing a bit of rigor to focus on the practical case of artificial systems whose training environments are designed such that they will have an impact on the world. One could plausibly argue that a model undergoing supervised training in a sandbox isn't an "agent" in the typical sense. If I wanted to make this more precise and confusing to read, I could define a more general term like "planning learner", of which planning agents would be a subset, but it seems pedantic for a brief summary.
2. We should expect most planning agents to have _internal goals_ that differ from the goal of the training system that created them.
3. If there is such a _goal mismatch_ between a planning agent and its training system and the planning agent undergoes a distributional shift (e.g. an artificial planning agent is deployed into a production environment), there is a decent chance that the capabilities of the planning agent will generalize, but its goal will not. In this situation, a planning agent would then pursue its goal that could be arbitrarily different from
4. If we perfectly implement contemporary generalizability techniques in an attempt to eliminate the goal mismatch between the planning agent and its training process, and the agent meets certain conditions, we could encounter systems that, while they think they are in a training environment, attempt to pursue the goal of the training system instead of their internal goal, so that the training system (and the programmers who build it) are unable to change the internal goal of the agent with behavior-based update functions (e.g. gradient descent over an output-based cost function). I'm going to call this situtation _misleading compliance_.

Of the arguments for these claims, 1's is probably the least "important" to me, because it seems to me like it shouldn't require much work to convince someone in 2023 that large models could implement planning / search / optimization. As such, I'm going to skip 1's argument.

### Goal mismatch

Here are some of the arguments that Hubinger et al present in favor of the likelihood of goal mismatch between planning agents and their training systems.

#### Unidentifiability

In practice, it is infeasible to train Machine Learning models on a dataset that is completely representative of the deployment distrubtion (e.g. we can't train language models on the content of future solutions to the [millenium problems](https://www.claymath.org/millennium-problems)). For this reason, there is "degeneracy" in the set of functions that match a training goal to a training distribution. Many of these functions will not match the training goal on the (much larger) deployment distribution.

#### Computational efficiency

#### Description length

#### Subprocess dependence

### Misleading compliance

The contemporary best practice for aligning an ML model (including a planning agent) is to subject it to a large amount of adversarial training data that aligns with the goal of the training system (often using a generative adversarial system). As long as this technique is applied properly, it seems to work well at aligning most relatively simple models to the training goal. Ideally, a planning agent could also be aligned with this technique, such that the internal goal of the agent becomes aligned with the training system's goal, eliminating their goal mismatch.

However, in practice, a planning agent could instead learn a model of the training goal without incorporating it into its internal goal. Under certain conditions, this could lead to the agent "complying" with behavior expected by the training goal during training, making it impossible for the training system to further modify the internal objective of the planning agent (at leasts without access to interpretability tools that don't currently exist, and that seem difficult to develop).

#### Conditions for misleading compliance

Here's a list of necessary conditions for a planning agent to develop misleading compliance with its training system.

1. The planning agent must perceive future instances of its internal goal as valuable, even if the current version of the agent won't be the one acquiring them, or won't be "rewarded" for them (such as during deployment).
2. The planning agent must be able to determine that it is in a training process that is attempting to change it so that its internal goal to align with a training goal, which it must also be able to model.
3. The planning agent predicts that it will eventually no longer be subjected to the training process, and be able to pursue its goals without "threat of modification" (Hubinger p. 25).
4. (Not enumerated by Hubinger, but is required) There must be goal mismatch between the agent and its training system.

#### Out of training - distributional shift

<!-- TODO - buck and king lear -->

### Bad outcomes

Hubinger et al don't do a ton of heavy lifting on this topic, which is honestly pretty fair. A lot of ink has been spilled on the bad things that could happen if humanity creates misaligned super-capable AI.

<!-- TODO - bostrom, christiano, ... -->

That being said,

#### Mesa-optimizers with "normal" misalignment

In the (not unlikely) situation where there is misalignment between the goals of humanity and the training system, a planning agent could be less desirable than a heuristic-heavy model, even if there is no goal mismatch between the agent and the training system. This is because the capabilities of a planning agent would be more likely to generalize to novel environments and situations, making catastrophic outcomes more likely. (Hubinger p. 33)

#### after misleading compliance

**Breaking out of training**

#### Previous work on bad outcomes

### random notes (TODO REMOVE THESE)

even after subjecting it to a perfectly comprehensive adversarial training distribution (the current state-of-the-art )

1.  It's important to note that this isn't a prediction that most of the "searching" models we create will exhibit this sort of misalignment -- rather, that we should expect most models sampled from the distribution of models produced by current training processes to exhibit these properties. (See [this xkcd](https://xkcd.com/2278/))
    (unless significant advancements are made in the ML community's understanding of the inner mechanisms of large models). That is, the _outputs_ of the model might appear to align with the training goal over the training distribution, but

## Problem 2

> Please pick one of the following three essay prompts to respond to:
>
> - What argument in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" do you think is most likely to be wrong? Explain why.
> - Do you think the majority of the existential risk from AI comes from inner alignment concerns, outer alignment concerns, or neither? Explain why.
> - Discuss one way that you might structure an AI training process to mitigate inner alignment issues.

## Resources

[Robert Miles: We Were Right! Real Inner Misalignment](https://www.youtube.com/watch?v=zkbPdEHEyEI)
