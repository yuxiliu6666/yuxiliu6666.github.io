---
layout: post
title: "SparkDiffusion: Mitigating the High-Sparsity Trap"
date: 2026-09-19
description: A unified framework for up to 265x single-GPU acceleration of visual generation.
tags: diffusion-transformers video-generation sparse-attention distillation quantization
categories: research
featured: true
---

SparkDiffusion is a unified acceleration framework for visual generation that pushes single-GPU video generation to up to **265x end-to-end speedup** over the dense 50-step CFG baseline, while sustaining **97% attention sparsity** with strong visual quality on long-sequence 720P generation.

## The high-sparsity trap

Video diffusion transformers are expensive because attention dominates long spatiotemporal token sequences. A natural remedy is to sparsify attention — but we identify a failure mode we call the **high-sparsity trap**: at extreme attention sparsity, step-local training losses keep decreasing while terminal generation quality stagnates or even degrades.

The trap is one of *supervision*, not capacity. The dominant terminal errors originate in the **high-noise structure-generation stage**, and terminal-aligned training corrects terminal errors that substantially extended step-local training simply cannot reach. Optimizing the per-step proxy harder only digs the trap deeper.

## A simple staging principle

This diagnosis yields a staging principle: **first adapt the sparse architecture into a coarse prior, then correct the terminal distribution**. SparkDiffusion instantiates the principle with three complementary components:

1. **Short sparse warm-up** — adapts the model to the sparse attention architecture, producing a coarse but structurally sound prior at 97% sparsity.
2. **Few-step trajectory-mixed distillation** — corrects the terminal distribution and collapses sampling to 3 CFG-free steps.
3. **FP8 quantization with fused kernels** — removes the remaining compute and memory bottlenecks at the system level.

## Results

- Sustains **97% attention sparsity** with strong visual quality on long-sequence **720P** generation across **Wan2.1/Wan2.2** backbones and both **T2V/I2V** tasks (90% sparsity on Wan2.1-T2V-1.3B-480P).
- With 3-step CFG-free inference, achieves a **265x end-to-end speedup** over the 50-step CFG dense baseline for Wan2.1-T2V-14B-720P on a single **RTX 5090** (**220x on H100**).
- Denoises a Wan2.1-T2V-1.3B-480P video in just **1.3 seconds**.

## Links

- [arXiv](https://arxiv.org/abs/2609.23153)
- [Project page](https://sparkdiffusion.github.io/)
- [Code](https://github.com/AlibabaResearch/SparkDiffusion)
- [Project](/projects/sparkdiffusion/)
