---
layout: post
title: pytorch and c++ woes in nix-shell on ubuntu
date: 2023-05-13 12:12:12 -0400
categories: development
---

I've got a complicated (but hopefully pretty portable) cross-platform development environment that uses [nix-shell](https://nixos.org/manual/nix/stable/command-ref/nix-shell.html). [nixos](https://nixos.org/) is a linux distribution, but `nix-shell` and `nix-env` can both be installed on other platforms (linux and MacOS).

One downside of this complex setup is that stuff breaks in weird ways sometimes.

## The problem

### pip vs conda

Instead of `conda`, I prefer to use `pip` and the ecosystem of tooling built around it (poetry, pdm, pipenv etc.) rather than picking up anaconda. This is largely due to development experience / aesthetics -- I like being able to structure my projects as packages, and that at least _used_ to be difficult / less well-supported with `conda`.

However, whatever its faults, `conda` exists for a reason -- c++ issues crop up pretty often when `pip install`ing numerical computing libraries, and in my setup, things were no different.

### the error message (for SEO optimization)

I'm feeling a bit too lazy right now to reproduce the issue to get an exact quote, but the error message included something like "libstdc++.so.6 not found". This would happen with a simple `python3 -c "import torch"`, but _not_ with `/usr/bin/python3 -c "import torch"`.

## The solution

I haven't been able to figure out a coherent debugging story / explanation as to why my solution worked,, so here it is:

Add `python311Packages.torch-bin` / `python310Packages.torch-bin` to your nixpkgs (e.g. in `shell.nix` / `default.nix`).

> **Note**
> You may need to also add `python311Packages.matplotlib` (among others) if you run into similar issues when importing `matplotlib.pyplot`. It's not an ideal state of affairs, but it's what we deal with when we're stubborn.

### Possible explanation

Even though I **have** `libstdc++.so.6` on my system from `apt install`ing the right dependencies, I think the python interpreters installed by `nix-shell` were unable to link to it? I don't understand how dynamic linking or OS package managers work, but hopefully this helps someone.
