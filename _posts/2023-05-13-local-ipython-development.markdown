---
layout: post
title: plotting in ipython in wezterm (or iterm2)
date: 2023-05-13 12:12:12 -0400
categories: development
---

## Motivation

I don't like working with notebooks. However, until recently, it wasn't possible to replicate a lot of their benefits in a traditional repl -- i.e. inline plots.

However, now that more and more terminals are adopting [one](https://iterm2.com/documentation-images.html) or [another](https://sw.kovidgoyal.net/kitty/graphics-protocol/) protocol for inline display of images, terminal addicts like myself might be able to do exploratory data analysis without having to give up the benefits of a terminal.

In my particular case, upon starting the fast.ai course, I immediately ran into a wall when trying to run code from [the first notebook](https://course.fast.ai/Lessons/lesson1.html) in ipython. Namely, displaying `PIL.Image`s.

## Alternatives

Here are some of the alternative solutions I know about

- [firenvim](https://github.com/glacambre/firenvim) (neovim-specific)
  - Why not just bring your terminal-based editor to the browwser?
  - I love the idea of this extension, and it's implemented remarkably well. Unfortunately, there's [a blocker](https://github.com/glacambre/firenvim/issues/672) with a [pretty popular but deprecated react component](https://github.com/facebookarchive/draft-js). This also is kind of a pain if you don't have a snappy startup time.
- [magma.nvim](https://github.com/dccsillag/magma-nvim) (neovim-specific)
  - Requires a decent amount of diy to get this working, and I wasn't able to work through some issues.
  - I might come back to this
- something that syncs ipynb to py file (Don't remember what this was and i haven't tried this)

## The solution

I use wezterm, which [supports the iterm image protocol](https://wezfurlong.org/wezterm/imgcat.html?h=image).

A bit of googling lead me to ipython's docs about [mime type rendering extensions](https://ipython.readthedocs.io/en/stable/config/shell_mimerenderer.html). Coupled with a helper function from the [itermplot library](https://github.com/daleroberts/itermplot) (which will be helpful in its own right for matplotlib plots), we're able to implement support for rendering images in ipython:

```python
from itermplot import imgcat

def register_mimerenderer(ipython, mime, handler):
    ipython.display_formatter.active_types.append(mime)
    ipython.display_formatter.formatters[mime].enabled = True
    ipython.mime_renderers[mime] = handler


def imgcat_factory(fn):
    def _wrapper(img, _):
        imgcat(img, fn=fn)

    return _wrapper


def load_ipython_extension(ipython):
    register_mimerenderer(ipython, "image/png", imgcat_factory(fn="img.png"))
    register_mimerenderer(ipython, "image/jpeg", imgcat_factory(fn="img.jpg"))
```

I've added this to my fork of itermplot in a [PR branch](https://github.com/daleroberts/itermplot/pull/58/files). At the moment, you'd load this extension with

```ipython
%load_ext itermplot.ipython
```

If the doesn't end up getting merged, you can still use this extension by itermplot from my fork. This isn't a great idea for most usecases (I'm very unlikely to keep that branch up-to-date with the central repo), but it's _probably fine_ for a development tooling situation like this.

Either way, if you want to do that:

```bash
pip install git+https://github.com/znd4/itermplot@add-ipython-extension
```
