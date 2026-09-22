---
layout: page
title: SparkDiffusion
description: Unified framework for up to 265x single-GPU acceleration of visual generation.
importance: 1
category: research
github: https://github.com/AlibabaResearch/SparkDiffusion
---

SparkDiffusion identifies the **high-sparsity trap** in video diffusion transformers — at extreme attention sparsity, step-local training losses keep decreasing while terminal generation quality stagnates or degrades — and turns the diagnosis into a staging principle: first adapt the sparse architecture into a coarse prior, then correct the terminal distribution.

The framework combines a short sparse warm-up, few-step trajectory-mixed distillation, and FP8 quantization with fused kernels. It sustains 97% attention sparsity with strong visual quality on long-sequence 720P generation across Wan2.1/Wan2.2 backbones and T2V/I2V tasks, achieves a 265x end-to-end speedup over the 50-step CFG dense baseline on a single RTX 5090 (220x on H100) with 3-step CFG-free inference, and denoises a Wan2.1-T2V-1.3B-480P video in 1.3s.

- [arXiv](https://arxiv.org/abs/2609.23153)
- [Project page](https://sparkdiffusion.github.io/)
- [Code](https://github.com/AlibabaResearch/SparkDiffusion)
- [Research note](/blog/2026/sparkdiffusion/)
