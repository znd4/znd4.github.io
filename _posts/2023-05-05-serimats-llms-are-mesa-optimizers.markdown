---
layout: post
title: We're not in the best of all possible worlds
date: 2023-05-05 12:12:12 -0400
categories:
---

In this post, I'll present part of my submissions to the "[Deceptive Alignment](https://www.serimats.org/deceptive)" and "[Aligning language models](https://www.serimats.org/aligning-language-models)" tracks of summer 2023 SERI MATS.

## Prompt

> What argument in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" do you think is most likely to be wrong? Explain why.

The core concepts considered in the paper will likely be looked upon favorably by future AI researchers, but I will argue that, partially due to "grey swan" events that occurred shortly after its publication, [Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB), in its discussions of future research agendas, underestimates the possibility for behavioral research into then contemporary and near-future deep learninng models to lead the way, and generate valuable insights prior to significant advances in interpretability.
Similarly, although Hubinger et al highlight uncertainties about the occurrence of mesa-optimizers and our ability to prevent them, due to both the previously mentioned surprises and their paper's lack of consideration AI governance concerns, Hubinger et al provide an overly certain conditional endorsement of research into preventing mesa-optimization.
That being said, the lines of work endorsed in the paper -- building a "formal specification of optimization", developing interpretability techniques for understanding when an ML system is performing optimization, and considering the applicability of techniques from inverse reinforcement learning, among others -- will likely form the core of any solution to the problem of pseudo-alignment in mesa-optimizers.

### GPT-2 might have been a meta-optimizer. GPT-4 probably is

Looking back, it's clear that "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" was written at an inflection point. "[Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)", the paradigm-shifting paper that introduced [Transformers](<https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)>) to the world, was published in December 2017, 18 months before Hulbinger et al's paper on mesa-optimizers, but it's understandable that language models were not significantly considered in the paper. In April of 2018, models based on BERT, then the state of the art in large transformer-based language models, performed "no better than most-frequent-class guessing" on the Winograd schema challenge, a test of pronoun disambiguation and commonsense reasoning ability ([Kocijian et al.](https://arxiv.org/abs/2201.02387), [Wang et al.](https://arxiv.org/abs/1804.07461)). By November of 2019, [Sakaguchi et al](https://arxiv.org/abs/1907.10641) were able to score over 90% on the same challenge. By the release of Hulbinger's paper, the capabilities of GPT-2 had [already surprised many](https://www.theverge.com/2019/2/14/18224704/ai-machine-learning-language-models-read-write-openai-gpt2), and already exhibited many of the qualities that Hulbinger et al would connect to mesa-optimizers. These qualities would then be 'turned up to 11' with the release of gpt 3.

#### Human behavior

One of the tasks that Hulbinger highlights as potentially significant to the creation of mesa-optimizers is "reasoning about optimization". More specifically, "predicting human behavior":

> Since humans often act as optimizers, reasoning about humans will likely involve reasoning about optimization. A system capable of reasoning about optimization is likely also capable of reusing that same machinery to do optimization itself, resulting in a mesa-optimizer. For example, it might be the case that predicting human behavior requires instantiating a process similar to human judgment, complete with internal motives for making one decision over another

GPT-2 had already been trained on predicting the text of "all outbound links from Reddit" with "at least 3 karma", a total of 40 GB of text ([Radford & Wu, 2019](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)). GPT-3 would then be trained on 570 GB of data ([Brown et al](https://arxiv.org/abs/2005.14165)). The task of language modeling seems to count as "predicting human behavior" -- a task at which GPT-2 and successor LLMs have performed surprisingly well.

#### Model capacity

The rest of the

From the paper:

> The larger the model capacity ... the more likely that it will be able to find one that is a mesa-optimizer. ... For example, architectures that explicitly give the algorithm access to a wide range of possible computations, such as recurrent neural networks...

GPT-2 was already pretty big. GPT-4 is enormous. Transformers are quite expressive.

#### Diverse environments

In one sense, language models operate in a very limited environment -- essentially reading and typing at a terminal. However, considering the enormous variety of

### Deep double descent

This is more speculative -- I'm in way over my head on this one -- but it's possible that some SGD "shallow" minima that may cause [deep double descent](https://www.lesswrong.com/posts/FRv7ryoqtvSuqBxuT/understanding-deep-double-descent) should be candidates for mesa-optimizers, and DDD (what an acronym!) is a graph of them being created.

### Agency Solipsism

One of the central causes of the mistake discussed in this essay was an (understandable, at the time) underestimation of the near-term potential of language models. Another was over-indexing on being _sure_ about whether certain agents are mesa-optimizers -- an assumption that we shouldn't significantly update our expectations based on anything but mechanistic, bottom-up insights:

> Moreover, the limited interpretability of neural networks, combined with the fact that there is no general and precise definition of “optimizer,” means that it would be hard to evaluate whether a given model is a mesa-optimizer.

... that is, unless that agent is a human, the "existence proof" for mesa-optimizers. I am _far_ from an expert in neuroscience, but I don't get the impression that we have an 'unlimited' capacity to interpret the human brain.

It's possible that we should be significantly more confident that I am a mesa-optimizer than that GPT-4 is. Still, if we are able to elicit behavior from GPT-4 for which mesa-optimization is the only known causal theory (e.g. deceptive alignment), we should significantly update our confidence that LLMs contain mesa-optimizers, even if we can't be **sure** that they're actually performing something close to a known optimization process.

And if we do encounter a system that is able to engage in deceptive alignment, maybe it doesn't matter if it's an

### Deceptive alignment gain-of-function

It's possible that GPT-4 (and possibly smaller LLMs) contain mesa-optimizers, but have not developed the capacity required to meet one or more of the conditions for deceptive alignment proposed in "Risks from Learned Optimization". It might be possible to "bootstrap" those conditions by testing an LLM in a lower-dimensional environment.

As an example, starting with a foundation LLM, then fine-tune the model via reinforcement learning, where the task is to predicting events in fictitious RL historys set in a relatively simple environment, (like a maze!). By training the model to predict actions, rewards and the fictitious agents' predicted rewards throughout training and testing, and by presenting clear instances of deceptive alignment followed by "successful" treacherous turns, it's possible that if we then train the fine-tuned model as part of an agent in an actual adversarial RL environment with different features, we might be able to observe deceptive alignment.
The theory of the case is that we'd be lowering the amount of cognitive capacity required:

Because, during fine-tuning, the model has "memory" between updates, and between training and testing

1. It should be easier for it to learn to model the "threat of modification"
2. It should be easier for it to learn that the "threat of modification" will eventually disappear

Additionally, the proposed environment could be significantly simpler than the real world.

### Risks

Proposals like the one above do carry risks (besides the obvious direct risks involved with gain-of-function research). If we put a ton of energy into these sorts of alignment evaluation studies, it's possible that we could become complacent when we get negative results. Tripping an alarm with one of these evaluations could be hugely valuable -- demonstrating deceptive alignment, or catching a model successfully working out the steps to copy itself in a sandbox -- but the spectre of deceptive alignment should always be in the back of our minds when we don't find anything. Absence of evidence is not evidence of abascence.

I've been thinking about an imperfect analogy: We don't want to be like the doctors before [stethoscopes](https://en.wikipedia.org/wiki/Stethoscope). Basically, never forget our ignorance.

## Quotes

> We deliberately choose to present theoretical considerations for why mesa-optimization may or may not occur rather than provide concrete examples. Mesa-optimization is a phenomenon that we believe will occur mainly in machine learning systems that are more advanced than those that exist today. Thus, an attempt to induce mesa-optimization in a current machine learning system would likely require us to use an artificial setup specifically designed to induce mesa-optimization. Moreover, the limited interpretability of neural networks, combined with the fact that there is no general and precise definition of “optimizer,” means that it would be hard to evaluate whether a given model is a mesa-optimizer.

## Outline

- introduction
  1. We're probably already living with mesa-optimizers
  2. we don't need better interpretability tools to check
  3. Even if non-mesa-optimizing TAI are possible, that doesn't mean that that's what we should focus on
- Why we might expect LLMs to be mesa-optimizers
  - [deep double descent](https://www.lesswrong.com/posts/FRv7ryoqtvSuqBxuT/understanding-deep-double-descent)
    - also see [OpenAI Article](https://openai.com/research/deep-double-descent)
    - Subprocess interdependence
    - > This suggests that, at least in a local optimization process, mesa-optimizers might tend to start their development as proxy aligned before becoming robustly aligned.
  - human modeling
  - model capacity / depth
  - diverse environments
  - sidney (look up ezra klein quote with casey newton's cohost "it knew you were a journalist looking for a Black Mirror episode, so that's what it gave you")
- behavioral vs mechanistic study
  - I don't have a strong academic background in the theoretical underpinnings of optimization (some from an ML fundamentals course, some from numerical analysis).
  - It's true that we can't _know_ whether a system is internally running an optimization algorithm without understanding its internals -- Hulbinger et al are right to draw a distinction between the behavioral objective and mesa objective. After all, many of the claims in the paper about risks from internal alignment depend on the assumption that
  - agency solipsism
- Bootstrapping deceptive alignment proposal
- Conclusion

## Resources

[Robert Miles: We Were Right! Real Inner Misalignment](https://www.youtube.com/watch?v=zkbPdEHEyEI)
