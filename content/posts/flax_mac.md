---
title: "Jax, Flax, & Macs"
date: 2022-10-19T12:00:00+01:00
draft: false
weight: 60
---

[JAX](jax.readthedocs.io) is a powerful tensor manipulation and autograd library that has seen a surge in popularity recently. It's also one of the key dependencies in Google's neural network library [Flax](flax.readthedocs.io). However, trying to install it on an M1 Mac can be a bit tricky. Today I managed to get it running on a 2021 Macbook Pro M1 without too many problems, so I've shared the Python environment [here](https://gist.github.com/JHart96/8fdca120f40b985440bb03f6a033ab26) to help others facing the same problem. Once downloaded, and in a virtual environment, the key dependencies can be installed by running:

```
pip install --upgrade pip
pip install -r flax-requirements.txt
```

And that should (hopefully) do it.

Out of curiosity I ran a quick test using a [CNN on MNIST](https://flax.readthedocs.io/en/latest/getting_started.html) to see how well the M1 chip does against a Colab GPU. I ran the example code and recorded how long 10 training and evaluation epochs took with a fixed batch size of 32.

| Device      | Running Time |
| ----------- | ------------ |
| M1 Pro (10 Core) | 3m 3s |
| Colab GPU | 1m 7s |
| Colab CPU | ~ 20m |

My 10 core M1 Pro ran 10 epochs in *3 minutes and 3 seconds*, where the Colab GPU took only *1 minute and 7 seconds*. Though nearly 3x slower, I don't think this is too bad for a CPU, and will be great for development environments. This story might change a lot depending on batch sizes and workloads, so take this with a pinch of salt. For reference though, a Colab CPU took around 20 minutes to run the same code, so the M1 CPU is certainly doing something right.

## PyMC & BlackJAX

Another reason you might want to use JAX is for probabilistic programming in PyMC. Using a JAX-based backend ([BlackJAX](https://blackjax-devs.github.io/blackjax/)) it's possible to speed up model compilation and fitting quite considerably. I also ran a quick comparison using a [simple linear regression](https://www.pymc.io/projects/docs/en/stable/learn/core_notebooks/GLM_linear.html) with 2000 data points to test sampling and compilation times in PyMC and CmdStan. I ran each model 5 times and took the lowest number for both sampling time and end-to-end time, including compilation.

| Sampler      | Sampling Time | End-to-end Time |
| ----------- | ------------ | --- |
| CmdStan 2.30.0 | 1.1s | 6.7s |
| PyMC 4.2.2 | 9.0s | 10.9s |
| PyMC 4.2.2 + BlackJAX | 2.8s | 3.6s |
| PyMC 4.2.2 + NumPyro | 1.8s | 2.8s |

Interestingly, base PyMC was slowest in both cases, but benefitted a lot from using the BlackJAX and NumPyro backends. The CmdStan sampler was fastest, but takes a while longer to compile meaning the end-to-end time was slower. This benchmark is far from exhaustive, and depending on model specification and dataset size, I suspect these results could change a lot.