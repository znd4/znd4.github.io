---
layout: post
title: We're not in the best of all possible worlds
date: 2023-05-05 12:12:12 -0400
categories:
---

In this post, I'll present part of my submissions to the "[Deceptive Alignment](https://www.serimats.org/deceptive)" and "[Aligning language models](https://www.serimats.org/aligning-language-models)" tracks of summer 2023 SERI MATS.

## Prompt

> What argument in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" do you think is most likely to be wrong? Explain why.

## Introduction

The core concepts advanced in the paper will likely be evaluated favorably by future AI researchers, but [Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB), underestimates the likelihood that contemporary and near-future language models will include mesa-optimizers without being "specifically designed to induce mesa-optimization".
This oversight is significant for mesa-optimizer research because, if they do include mesa-optimzers, Large Language Models (LLMs) could be ideal test subjects for basic experimental research. Up to this point, most of the behavioral research of LLMs has been focused on immediate safety / capabilities concerns, rather than attempting to build an empirical footing for speculative concerns like mesa-optimization.

### GPT-2 might have been a meta-optimizer. GPT-4 probably is

Looking back, it's clear that "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" was written at an inflection point. Prior to 2018, language modeling
"[Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)", the paradigm-shifting paper that introduced [Transformers](<https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)>) to the world, was published in December 2017, 18 months before Hulbinger et al's paper on mesa-optimizers, but it's understandable that language models were not significantly considered in the paper.
In April of 2018, models based on BERT, then the state of the art in large transformer-based language models, performed "no better than most-frequent-class guessing" on the Winograd schema challenge, a test of pronoun disambiguation and commonsense reasoning ability ([Kocijian et al.](https://arxiv.org/abs/2201.02387), [Wang et al.](https://arxiv.org/abs/1804.07461)).
By November of 2019, [Sakaguchi et al](https://arxiv.org/abs/1907.10641) were able to score over 90% on the same challenge.
By the release of Hulbinger's paper, the capabilities of GPT-2 had [already surprised many](https://www.theverge.com/2019/2/14/18224704/ai-machine-learning-language-models-read-write-openai-gpt2), and already exhibited many of the qualities that Hulbinger et al would connect to mesa-optimizers.
These qualities would then be 'turned up to 11' with the release of gpt 3.

#### Human behavior

One of the tasks that Hulbinger highlights as possibly significant to the creation of mesa-optimizers is "reasoning about optimization". More specifically, "predicting human behavior":

> Since humans often act as optimizers, reasoning about humans will likely involve reasoning about optimization. A system capable of reasoning about optimization is likely also capable of reusing that same machinery to do optimization itself, resulting in a mesa-optimizer. For example, it might be the case that predicting human behavior requires instantiating a process similar to human judgment, complete with internal motives for making one decision over another

Intuitively, it seems like "predicting human behavior" should include human language modeling. One might respond that the training data for LLMs includes a lot of content that doesn't count as "behavior" the way that navigating a maze does -- press releases, articles, etc. -- but upon consideration, the critique seems flimsy. Long-form writing involves a significant amount of optimization, and the people writing such content are clearly doing so with specific goals in mind -- e.g. I'm currently writing this with the goal of convincing some of the readers to accept me into a competitive education program.

#### Diverse environments

In one sense, language models operate in a very limited environment compared to the one that we find ourselves in. However, think of the vast amount of data that foundation LLMs are trained on -- we have substituted broad environment diversity with narrow environment diversity. Released prior to Hulbinger's paper, GPT-2 was trained on the task of predicting the text of "all outbound links from Reddit" with "at least 3 karma", a dataset totalling 40GB ([Radford & Wu, 2019](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)). GPT-3 would then be trained on 570 GB of text data ([Brown et al](https://arxiv.org/abs/2005.14165)). LLMs don't have access to much of the data that humans experience -- taste, proprioception etc. -- but they have experienced _much_ more of the collective textual history of humanity than any human.

#### Deep double descent and recent interpretability work

This is more speculative but it seems possible that some of the SGD "shallow" minima that may cause [deep double descent](https://www.lesswrong.com/posts/FRv7ryoqtvSuqBxuT/understanding-deep-double-descent) (DDD) and [grokking](https://openreview.net/forum?id=JqtHMZtqWm) could be candidates for mesa-optimizers. DDD might give us a graph of them being created.

#### Model capacity

From the paper:

> The larger the model capacity ... the more likely that it will be able to find one that is a mesa-optimizer. ... For example, architectures that explicitly give the algorithm access to a wide range of possible computations, such as recurrent neural networks...

When I started writing this, I wasn't confident about my intuitions about the capacity of transformers -- I'd planned to point to the raw scale of recenet LLMs (the largest GPT-3 base model has 96 attention layers and 175 Billion parameters). While writing this, I found that [someone else is bullish](https://www.lesswrong.com/posts/fytgZ26AgxmrAdyB4/mesa-optimizers-via-grokking) about a connection between grokking and mesa-optimizers, and was convinced that transformers could be the real deal. I'm not sure that [induction heads](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html) or [discrete fourier transforms](https://www.lesswrong.com/posts/N6WM6hs7RQMKDhYjB/a-mechanistic-interpretability-analysis-of-grokking#Key_Takeaways1) count as mesa-optimizers, but the fact that toy transformer models can learn these algorithms should convince observers that deeper transformer architectures could implement complex optimization procedures.

### Agency Solipsism

In addition to noticing the significant advances that occured since 2019, I've found an disagreement between myself and Hubinger et al about epistemology. They seem pessimistic about the possibility of diagnosing meta-optimization without advanced interpretability tools:

> Moreover, the limited interpretability of neural networks, combined with the fact that there is no general and precise definition of “optimizer,” means that it would be hard to evaluate whether a given model is a mesa-optimizer.

... that is, unless we're attempting to diagnose a human, their "existence proof" for mesa-optimizers. I am _far_ from an expert in neuroscience, but my impression is that our capacity to interpret the human brain is still quite "limited". For example, as far as I know, we're far from anything close to the "neural lie detection" technique that's been [recently invented for evaluating language models](https://arxiv.org/abs/2212.03827).

It's possible that we should be significantly more confident that I am a mesa-optimizer than that GPT-4 is. Still, if we are able to elicit behavior from GPT-4 for which mesa-optimization is the only known causal theory (e.g. deceptive alignment), we should significantly update our confidence that LLMs contain mesa-optimizers, even if we can't be **sure** that they're actually performing something close to a known optimization process. If it walks like a duck and quacks like a duck, it's **probably** a duck.

### Conclusion

## Appendix

### Deceptive alignment gain-of-function

I was too excited about this idea to not include it, especially since I haven't found anything like it while working on this document.

It's possible that GPT-4 (and possibly smaller LLMs) contain mesa-optimizers, but have not developed the capacity required to meet one or more of the conditions for deceptive alignment proposed in "Risks from Learned Optimization". With that in mind, it might be possible to "bootstrap" those conditions by testing an LLM in a lower-complexity environment.

e.g.

#### process

1. Start with a foundation LLM
2. fine-tune the model via reinforcement learning, where the task is to predicting events in RL histories set in a relatively simple environment. Without loss of generality, let's pick a maze.
   1. Specifically, require the model to predict the the fictitious agent's next action and expected reward, and the actual reward from the base goal
   1. Present synthesized examples of deceptive alignment followed by a "successful" treacherous turn. This could be accomplished by stitching together separate RL histories
3. Train the fine-tuned model as part of an agent in an adversarial RL task in similar maze environments
   1. initially, present mazes where there are multiple clear proxy objectives (e.g. object at the exit)
   2. at a certain point, switch to adversarially generating a robust dataset, expecting the model to begin to display pursuit of the base objective.
4. Test the model in a "deployment" environment and see if it starts pursuing one of the proxy objectives.
5. Create a control by running 2-4 again, but don't demonstrate deceptive alignment to it during step 2

#### hypothesis

The theory of the case is that we'd be lowering the amount of cognitive capacity required to model the base objective, the "threat of modification" and the possibility that the threat will eventually disappear. This is expected because:

1. The LLM has "memory" between training and deployment (during the initial fine-tuning task)
2. The environment being studied is simpler than the real world
3. It is given explicit examples of successful treacherous turns

If we see the control model continue to pursue the base objective and the treated model veers off course, it _might_ be a definitive demonstration of deceptive alignment (if my concerns can be addressed).

#### Gaps / Concerns

I'm not _sure_ that this would actually demonstrate deceptive alignment. There might need to be a significant difference between the fine-tuning and final train-test environments. Additionally, I'm not sure about whether we could inject a train-test distribution shift that wouldn't the validity of the experiment.
