---
name: towards-monosemanticity-decomposing-language-models-with-dictionary-learning
description: "Use this skill to Trains a wide sparse autoencoder on the residual stream of a one-layer transformer and finds that the resulting features are substantially more interpretable than the model s native neurons.. Triggers when working on Towards Monosemanticity, code implementation, auditing, or refactoring."
---

# Towards Monosemanticity

## TL;DR
Trains a wide sparse autoencoder on the residual stream of a one-layer transformer and finds that the resulting features are substantially more interpretable than the model's native neurons.

## Key claims
1. SAE features are more monosemantic than neurons
2. Features come in interpretable families (tokens, contexts, syntactic roles)
3. The approach is complementary to, not a replacement for, mechanistic circuits work

## Methods
- One-layer transformer target
- Wide sparse autoencoder on residual stream
- L1 sparsity regularization
- Feature dictionary size >> model width

## Evidence cited
- Qualitative inspection of top activating examples per feature
- Comparison with probing
- Feature family analysis

## Connections
- Extends [[concepts/sparse-autoencoder]]
- Builds on [[entities/anthropic]]'s prior Transformer Circuits work

## Where it's cited
- [[concepts/sparse-autoencoder]]
- [[entities/anthropic]]
- [[synthesis/interpretability-overview]]
