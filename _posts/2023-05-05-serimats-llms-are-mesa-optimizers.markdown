---
layout: post
title: SERI MATS Summer 2023 Problem 2
date: 2023-05-05 12:12:12 -0400
categories:
---

## Prompt

> Please pick one of the following three essay prompts to respond to:
>
> - What argument in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" do you think is most likely to be wrong? Explain why.
> - Do you think the majority of the existential risk from AI comes from inner alignment concerns, outer alignment concerns, or neither? Explain why.
> - Discuss one way that you might structure an AI training process to mitigate inner alignment issues.

## We're not in the best of all possible worlds


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
