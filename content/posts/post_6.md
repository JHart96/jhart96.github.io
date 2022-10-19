---
title: "Jax, Flax, & Macs"
date: 2022-10-03T12:00:00+01:00
draft: false
---
{{< katex >}}

JAX is a powerful tensor manipulation and autograd library that has seen a surge in popularity recently. However, trying to install it on an M1 Mac has been a bit tricky until recently. Today I managed to get it running on a 2021 Macbook Pro M1 without too many problems, so I've shared the Python environment here to help others facing the same problem.

Out of curiosity I ran a quick test using a CNN on MNIST to see how well the M1 chip does against a Colab GPU. My 10 core M1 Pro ran 10 epochs in 3 minutes and 2.8 seconds, where the Colab GPU took only 1 minute and 7 seconds. Though nearly 3x slower, I don't think this is too bad for a CPU, and will be great for development environments. This story might change a lot depending on batch sizes and workloads, so take this with a pinch of salt. For reference though, a Colab CPU took around 20 minutes to run the same code, so the M1 CPU is certainly doing something right.