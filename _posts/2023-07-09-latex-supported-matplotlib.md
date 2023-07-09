---
layout: post
title: Use latex with matplotlib on HPCs
date: 2023-07-09 17:00:00-0800
description: 
tags: latex matplotlib
categories: hack
giscus_comments: true
---

Have you ever wanted to use LaTeX with matplotlib? You are definitely not alone and there are many tutorials out there that can guide you through the installation process and follow the [official documentation](https://matplotlib.org/stable/tutorials/text/usetex.html).

What we need to do is just installing typical `latex` by 

```bash
sudo apt update
sudo apt install texlive # for minimum latex build
sudo apt install dvipng texlive-latex-extra texlive-fonts-recommended # required by matplotlib
```

Then we are good to go! The lightest `texlive` installation is not enough, and if you try to use `plt.rcParams['text.usetex'] = True` you will find there are packages missing like `type1cm.sty`, `dvipng`, *etc*. 

**What if we cannot `sudo` on the specific computer?** Then this post is what you are looking for! 

# I can't sudo!

Things get tricky when we want to install latex on computers where we don't have administrative privileges (such as HPCs). We cannot use `sudo install latex-*` anymore and need to download and install `texlive` manually.

1. Follow the instruction on [official texlive website](https://www.latex-project.org/get/) to build from scratch 
    ```bash
    wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz # or curl instead of wget
    zcat < install-tl-unx.tar.gz | tar xf -
    cd install-tl-*
    perl ./install-tl --no-interaction # as root or with writable destination
    ```
2.  Prepend `<installed texlive path>/bin/PLATFORM` to your `PATH`, *e.g.*, `~/texlive/YYYY/bin/x86_64-linux`
3.  Download and extract the missing package to latex library folder (*e.g.* `<path to texlive>/texmf-dist/tex/latex/type1cm`)
    ```bash
    wget https://mirrors.ctan.org/macros/latex/contrib/type1cm.zip
    unzip type1cm.zip
    ```
4. Run `latex` to generate `.sty` file
    ```bash
    latex type1cm.ins
    ```
5. Update and link the file by executing `mktexlsr`
    ```bash
    ./<path to extracted folder>/install-tl-<date>/texmf-dist/scripts/texlive/mktexlsr
    ```

Then voilà! Happy plotting matplotlib supported with latex on any system! Leave comment or buy me a coffee if you like this post! 🙂