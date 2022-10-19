---
title: "Jax, Flax, & Macs"
date: 2022-10-19T12:00:00+01:00
draft: false
weight: 60
---

[JAX](jax.readthedocs.io) is a powerful tensor manipulation and autograd library that has seen a surge in popularity recently. It's also one of the key dependencies in Google's neural network library [Flax](flax.readthedocs.io). However, trying to install it on an M1 Mac can be a bit tricky. Today I managed to get it running on a 2021 Macbook Pro M1 without too many problems, so I've shared the Python environment [here](https://gist.github.com/JHart96/8fdca120f40b985440bb03f6a033ab26) to help others facing the same problem. Once downloaded, and in a virtual environment, the key dependencies can be installed by running:

```
pip install --upgrade pip
pip -r install flax-requirements.txt
```

And that should (hopefully) do it.

Out of curiosity I ran a quick test using a [CNN on MNIST](https://flax.readthedocs.io/en/latest/getting_started.html) to see how well the M1 chip does against a Colab GPU. I ran the example code and recorded how long 10 training and evaluation epochs took with a fixed batch size of 32.

| Device      | Running Time |
| ----------- | ------------ |
| M1 Pro (10 Core) | 3m 3s |
| Colab GPU | 1m 7s |
| Colab CPU | ~ 20m |

My 10 core M1 Pro ran 10 epochs in *3 minutes and 3 seconds*, where the Colab GPU took only *1 minute and 7 seconds*. Though nearly 3x slower, I don't think this is too bad for a CPU, and will be great for development environments. This story might change a lot depending on batch sizes and workloads, so take this with a pinch of salt. For reference though, a Colab CPU took around 20 minutes to run the same code, so the M1 CPU is certainly doing something right.