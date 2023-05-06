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

The core concepts considered in the paper will likely be looked upon favorably by future AI researchers, but the _future work_ recommendations in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" seem, in the present moment, to be too narrowly focused on theoretical research into the emergence of mesa-optimizers & pseudo-alignment and improvements in interpretability. Those lines of work will likely form the core of the effort to reduce risk from catastrophically misaligned mesa-optimizers, but I will argue that, partially due to "grey swan" events that occurred shortly after the publication of the article, Hulbinger et al missed the potential for experimental research into then-near-future deep learning systems. Such experimental research into mesa-optimizers, especially lower-effort behavioral studies, might significantly reduce AI existential risk, both by

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
