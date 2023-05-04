---
layout: post
title: SERI MATS Submission
subtitle: Are contemporary LLMs capable of deceptive alignment?
gh-repo: znd4/znd4.github.io
comments: true
---

In this post, I'll be writing my submission to the 2023 Summer SERI MATS cohort in the "[Deceptive Alignment](https://www.serimats.org/deceptive)" and "[Evaluating dangerous capabilities](https://www.serimats.org/evals)" and "[Aligning language models](https://www.serimats.org/aligning-language-models)" tracks.

In the interest of time, I won't be attempting a solution to the optional Problem 3, although it seems like an interesting thing to work on in the future.

## Problem 1

> Briefly summarize the most important (according to you) arguments in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" without using any terminology specific to that paper.

Broadly speaking, _Risks from Learned Optimization in Advanced Machine Learning Systems_ argues for the following:

1. That Machine Learning systems training for complex tasks / environments will be / are likely to produce models that actively perform search over a space of possible actions.
   1. E.g. evolution -> humans
2. That we should expect most such "searching" models to have goals that do not _generally_ align with the goal of the original training system (unless significant advancements are made in the ML community's understanding of the inner mechanisms of large models). That is, the _outputs_ of the model might appear to align with the training goal over the training distribution, but
   1. It's important to note that this isn't necessarily a prediction that most of the "searching" models we create will exhibit this sort of misalignment -- rather, that we should expect most models sampled from the distribution of models produced by current training processes to exhibit these properties. Future developments (including some proposed in this paper) could (and hopefully will!) prevent the creation of a powerful artificial agent with a goal that doesn't align with the goal of the training process that created it.
3. That, if we work through most of the causes of misalignment between the model and the training process, if the model meets three criteria, we could find that the

## Problem 2

> Please pick one of the following three essay prompts to respond to:
>
> - What argument in "[Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB)" do you think is most likely to be wrong? Explain why.
> - Do you think the majority of the existential risk from AI comes from inner alignment concerns, outer alignment concerns, or neither? Explain why.
> - Discuss one way that you might structure an AI training process to mitigate inner alignment issues.

## Resources

[Robert Miles: We Were Right! Real Inner Misalignment](https://www.youtube.com/watch?v=zkbPdEHEyEI)
