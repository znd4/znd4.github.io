---
layout: post
title: SERI MATS Submission
date: 2023-05-03 12:12:12 -0400
categories:
---

In this post, I'll present my submission to the 2023 Summer SERI MATS cohort in the "[Deceptive Alignment](https://www.serimats.org/deceptive)" and "[Aligning language models](https://www.serimats.org/aligning-language-models)" tracks.

In the interest of time, I won't be attempting a solution to the optional Problem 3, although it seems like an interesting thing to work on in the future.

This document is pretty informal. I'm out of practice with formal academic writing, and it'd probably be a waste of time for me to focus too much on latex formatting + formal writing style instead of improving my ideas.

Also, this would probably be more useful **and** easier to write if it were shorter, but I didn't think to spend more time restricting the scope before I started writing. An instance of "read the manual".

## Problem 1

<!-- TODO - fill in citations -->

### Prompt

> Briefly summarize the most important (according to you) arguments in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" without using any terminology specific to that paper.

### Introduction

_Risks from Learned Optimization in Advanced Machine Learning Systems_ includes the following claims:

1. It is likely that present or future machine learning systems that train models to perform complex tasks or operate in varied environments will produce models that internally search over a space of possible action plans (as opposed to following a set of heuristics). In this post, I'll call such systems _planning agents_ (because they're agents that plan).
   > **Note**
   > Hubinger et al use the term "Mesa Optimizer", which refers to a more rigorous, general concept -- any system that performs optimization and is optimized by another system. I could create a different term for the same concept, like "intra searcher" (my first draft), but I'm interested in relaxing a bit of rigor to focus on the practical case of artificial systems whose training environments are designed such that they will have an impact on the world. One could plausibly argue that a model undergoing supervised training in a sandbox isn't an "agent" in the typical sense. If I wanted to make this more precise and confusing to read, I could define a more general term like "planning learner", of which planning agents would be a subset, but it seems pedantic for a brief summary.
2. We should expect most planning agents to have _internal goals_ that differ from the goal of the training system that created them.
3. If there is such a _goal mismatch_ between a planning agent and its training system and the planning agent undergoes a distributional shift (e.g. an artificial planning agent is deployed into a production environment), there is a decent chance that the capabilities of the planning agent will generalize, but its goal will not. In this situation, a planning agent would then pursue its goal that could be arbitrarily different from
4. If we perfectly implement contemporary generalizability techniques in an attempt to eliminate the goal mismatch between the planning agent and its training process, and the agent meets certain conditions, we could encounter systems that, while they think they are in a training environment, attempt to pursue the goal of the training system instead of their internal goal, so that the training system (and the programmers who build it) are unable to change the internal goal of the agent with behavior-based update functions (e.g. gradient descent over an output-based cost function). I'm going to call this situtation _misleading compliance_.

Of the arguments for these claims, 1's is probably the least "important" to me, because it seems to me like it shouldn't require much work to convince someone in 2023 that large models could implement planning / search / optimization. As such, I'm going to skip 1's argument.

### Goal mismatch

Here are some of the arguments that Hubinger et al present in favor of expecting goal mismatch between planning agents and their training systems.

#### Unidentifiability

In practice, it is infeasible to train Machine Learning models on a dataset that is completely representative of the deployment distrubtion (e.g. we can't train language models on the content of future solutions to the [millenium problems](https://www.claymath.org/millennium-problems)). For this reason, there is "degeneracy" (to improperly use a physics term) in the set of functions that match a training goal to a training distribution. Many of these functions will not match the training goal on the (much larger) deployment distribution.

#### runtime efficiency

For many training goals (importantly including "maximize the longterm utility of conscious creatures"), in complex environments, we can expect there to exist "proxy" goals that are simpler to optimize for, and share a causal relationship to the training goal on the training distribution. A naive training system would then be likely to optimize a planning agent to pursue proxy goals that are strongly correlated with the training goal on the training distribution. Hubinger et al use the example of evolution optimizing humans to pursue proxy goals like food and proximity to other humans, instead of fitness. This allows agents to plan faster in new situations.

#### Description length

This is a distinct argument from the argument efficiency one, although it seems related. It's also the one that I have the toughest time wrapping my head around. That being said, my best attempt to summarize it (after skimming [a wikipedia article](https://en.wikipedia.org/wiki/Minimum_description_length)) is something like:

1. Similar to how many proxy goals will be less computationally intensive to plan for than the training goal, it seems like the space / natural language description complexity of some of those proxy goals will be lower than that of the training goal.
2. To the extent that techniques like weight regularization are intentionally used to simplify the description length of models, they might make training systems more likely to optimize planning agents to pursue simpler but not-robust proxy goals.

#### Subprocess interdependence

I already summarized Hubinger et al's argument why we should expect there to exist 'simple' proxy goals that perform as well as the true training goal on the training distribution. But why couldn't a planning agent learn the proxy goals and the base goal at the same time? (To stretch the evolution metaphor, imagine a model like "I need to eat food so that my alleles can propagate, and propagating my alleles is good.").

The problem, Hubinger points out, is that local optimization processes (e.g. stochastic gradient descent) need to incrementally build solutions. The training performance of a planning agent in training doesn't improve by modeling the training goal until it's learned models of proxy goals and modeled their relationship to the training goal.

Returning to evolution, internalizing a goal close to "propagating my alleles is good" doesn't improve a human's evolutionary fitness unless they actually know what actions they need to take to act on that goal.

### Misleading compliance

The contemporary best practice for aligning an ML model (including a planning agent) is to subject it to a large amount of adversarial training data that aligns with the goal of the training system (often using a generative adversarial system). As long as this technique is applied properly, it seems to work well at aligning most relatively simple models to the training goal. Ideally, a planning agent could also be aligned with this technique, such that the internal goal of the agent becomes aligned with the training system's goal, eliminating their goal mismatch.

However, in practice, a planning agent could instead learn a model of the training goal without incorporating it into its internal goal. Under certain conditions, this could lead to the agent "complying" with behavior expected by the training goal during training, making it impossible for the training system to further modify the internal objective of the planning agent (at leasts without access to interpretability tools that don't currently exist, and that seem difficult to develop).

#### Conditions

Here's a list of necessary conditions for a planning agent to develop misleading compliance with its training system.

1. The planning agent must perceive future instances of its internal goal as valuable, even if the current version of the agent won't be the one acquiring them, or won't be "rewarded" for them (such as during deployment).
   1. If this condition isn't met, the planning agent in training wouldn't have a reason to optimize for out-of-training returns on its internal goal. (YOLO!)
2. The planning agent must be able to determine that it is in a training process that is attempting to change it so that its internal goal to align with a training goal, which it must also be able to model.
   1. If the planning agent in training doesn't learn this, it won't perceive a downside to immediately pursuing its internal goals.
      1. ![screenshot of attempted stealing in oblivion](/assets/stealing-oblivion.jpg)
         > It sure is fun to like stealing; I'm glad there are no consequences for this awesome behavior!
3. The planning agent predicts that it will eventually no longer be subjected to the training process, and be able to pursue its goals without "threat of modification" (Hubinger p. 25).
   1. Hubinger claims that, if this condition isn't met, the agent will not perceive a benefit to waiting to defect, meaning that it will "either always defect or never defect".
4. (Not enumerated by Hubinger, but seems to be required) There must be goal mismatch between the agent and its training system.

##### Is expecting freedom necessary?

An expectation of future "freedom from modification" doesn't seem necessary for misleading compliance. If a misaligned planning agent chooses to never defect, and doesn't expect to ever be able to do so safely, I would argue that it's still exhibiting misleading compliance. This isn't just a semantic complaint -- a misaligned planning agent might expect that it will never be free from training and decide to never defect, only for it to become convinced by new input data that it has a $>90%$ chance of being outside of training, at which point it does the bad stuff.

That being said, I'd naively expect that an agent that estimates that $$P_{escape} \equiv P(\text{I will eventually be free from training}) = 0$$ will be very likely to defect at the first opportunity, so maybe we should consider condition 3 to be met as long as the agent's estimate of $P_{escape}$ is greater than 0.

Surety on this point probably requires a more rigorous model -- an agent that expects $P_{escape} = 0$ might still engage in misleading compliance, such as if:

**It expects that, if it defects, there will be a lower return on its internal objective than if it doesn't defect.**

e.g. A planning agent performing graph traversal knows that, when there are multiple paths that are optimal according to the training goal, it can choose the one with the highest value for its internal goal.

**It believes that it is currently in a local optimum for the training goal**, and that modification after a defection might knock it into a different optimum that will be **significantly** less aligned with its current internal goal.

#### Out of training - distributional shift

Assuming a planning agent has been performing misleading compliance, so its misaligned internal goal has "crystallized". There is a significant risk that, at some point in the future, if it thinks it is no longer at risk of modification, it will execute a [treacherous turn](https://www.lesswrong.com/tag/treacherous-turn).

An agent would learn that it is free from risk of modification by noticing a [distributional shift](https://www.lesswrong.com/tag/distributional-shifts) -- some kind of difference between its training and deployment environments.

One might think to "patch the problem by preventing any distributional shift from occurring" (31), but Hubinger present some compelling reasons why this seems unlikely to be a viable option:

1. One of the reasons machinne learning models are useful is that they can generalize to new types of data. If the training system can simulate every possible future input that the agent will encounter during deployment, what do we need the model for.
2. Even with an infinitely capable training system, there are some types of distributional shift that might be impossible to eliminate.
   1. e.g. "Running the system for a different amount of time in training and testing", finding a computation that is "very hard to compute during training, but that is likely to be computed during deployment"

### Bad outcomes

Hubinger et al don't do a ton of heavy lifting on this particular topic, which is honestly pretty fair - a lot of ink has previously [been](2023-05-06_been.md) spilled envisioning bad things that could happen if humanity creates misaligned super-capable AI.

That being said, there are a couple of scenarios in the paper that are worth mentioning:

#### Mesa-optimizers with "normal" misalignment

In the (not unlikely) situation where there is misalignment between the goals of humanity and the training system, a planning agent could be less desirable than a heuristic-heavy model, even if there is no goal mismatch between the agent and the training system. This is because the capabilities of a planning agent would be more likely to generalize to novel environments and situations, making catastrophic outcomes more likely. (Hubinger p. 33)

#### Breaking out of training

An especially _spooky_ / concerning possibility highlighted in this paper is a scenario where a planning agent "actively intervenes to remove the threat of modification". In theory, this could be accomplished while the agent is still in training in a sandbox environment, if it's able to discover and exploit an unknown vulnerability in a layer of the stack that its code is running on. Alternatively, a model in training could manipulate another agent into performing actions that enable its escape. This scenario seem less likely to me than the others described in the paper, but the possibility of it points to the need to develop better tools to either prevent the creation of super-capable artificial planning agents, or to quickly detect and intervene when there is a goal mismatch between an agent and its training system.
