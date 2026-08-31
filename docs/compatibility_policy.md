# Environment Compatibility Policy

This repository uses direction-specific environments instead of one large environment for everyone.

## Why We Separate Environments

Different projects in the lab have different dependency profiles:

- GNN projects need a sensitive PyTorch/CUDA/PyG/DGL stack.
- DRL projects need reinforcement learning frameworks such as Stable-Baselines3 and Gymnasium, but not necessarily PyG or DGL.
- LLM-based agent projects often need API clients, local Ollama access, tool orchestration, and graph/database utilities, but not necessarily CUDA-based graph learning.
- MLLM projects need multimodal, embedding, retrieval, and image-processing packages.
- Production / Supply Chain Network projects usually need optimization, simulation, network analysis, and data-processing packages.

Installing every package for everyone would make environments larger, slower to solve, harder to debug, and more likely to break during code integration.

## GNN Stack Rule

For GNN and GNN-combined environments, keep this stack together:

```text
python=3.10
pytorch=2.1.0
torchvision=0.16.0
torchaudio=2.1.0
pytorch-cuda=12.1
pyg=2.5.2
dgl=2.0.0+cu121
```

MLLM and agent packages may be added on top, but they should not reinstall or upgrade `torch`, `torchvision`, `torchaudio`, PyG, DGL, or CUDA packages.

## DRL Stack Rule

DRL is not the same as GNN. Do not rename GNN dependencies as DRL dependencies.

The DRL baseline uses the same PyTorch/CUDA base as GNN and MLLM where possible:

```text
python=3.10
pytorch=2.1.0
torchvision=0.16.0
torchaudio=2.1.0
pytorch-cuda=12.1
stable-baselines3=2.3.2
gymnasium>=0.29.1,<1.0
```

Stable-Baselines3 is pinned because newer releases may require newer PyTorch versions. This keeps DRL compatible with the current shared PyTorch baseline while avoiding accidental upgrades of the GNN stack.

## Practical Rule for Students

Start with the smallest environment that matches your project. Add packages only when your project actually needs them. If a new package becomes common across several projects, report it so that we can decide whether it belongs in `core`, a direction-specific environment, or a combined environment.

## Notes

- PyTorch releases `torch`, `torchvision`, `torchaudio`, and CUDA builds as matched installation groups.
- PyG provides wheels/Conda support according to specific PyTorch and CUDA versions.
- DGL CUDA wheels are also versioned by CUDA runtime.
- Stable-Baselines3 dependency requirements can change across versions, so DRL packages should be updated deliberately rather than automatically.

This policy is intended to reduce future import errors, syntax/version mismatch issues, dependency conflicts, and integration bugs when project code is merged.
