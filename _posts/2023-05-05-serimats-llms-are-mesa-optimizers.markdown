---
layout: post
title: SERI MATS Summer 2023 Problem 2
date: 2023-05-05 12:12:12 -0400
categories:
---

In this post, I'll present part of my submissions to the "[Deceptive Alignment](https://www.serimats.org/deceptive)" and "[Aligning language models](https://www.serimats.org/aligning-language-models)" tracks of summer 2023 SERI MATS.

## Prompt

> What argument in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" do you think is most likely to be wrong? Explain why.

## We're not in the best of all possible worlds

The core concepts considered in the paper will likely be looked upon favorably by future AI researchers, but I will argue that, partially due to "grey swan" events that occurred shortly after the publication of the article, "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)"'s discussions of future research agendas underestimate the possibility for behavioral research into then-near-future deep learninng models to _lead the way_, generating valuable insights prior to (and possibly contributing to) significant advances in model interpretability.
Similarly, although Hubinger et al highlight uncertainties about the occurrence of mesa-optimizers and our ability to prevent them, due to both the previously mentioned surprises and their paper's lack of consideration AI governance concerns, Hubinger et al provide an overly certain conditional endorsement of research into preventing mesa-optimization.
That being said, the lines of work endorsed in the paper -- building a "formal specification of optimization", developing interpretability techniques for understanding when an ML system is performing optimization, and considering the applicability of techniques from inverse reinforcement learning, among others -- will likely form the core of any solution to the problem of pseudo-alignment in mesa-optimizers.

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
  - depth
  - diverse environments
- behavioral vs mechanistic study
  - I don't have a strong academic background in the theoretical underpinnings of optimization (some from an ML fundamentals course, some from numerical analysis).
  - It's true that we can't _know_ whether a system is internally running an optimization algorithm without understanding its internals -- Hulbinger et al are right to draw a distinction between the behavioral objective and mesa objective. After all, many of the claims in the paper about risks from internal alignment depend on the assumption that
  - Bootstrapping deceptive alignment
- Conclusion

## Resources

[Robert Miles: We Were Right! Real Inner Misalignment](https://www.youtube.com/watch?v=zkbPdEHEyEI)
