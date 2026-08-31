# Shared Conda Environments

This repository provides shared, direction-specific Conda environment baselines for NTU Industrial AI Lab projects.

The goal is not to force every student to install every package. Instead, each student should install the smallest environment that matches their current research direction, while keeping the important shared stacks compatible for future code integration and merging.

## Recommended Environment Choice

| Research direction | Recommended environment | When to use it |
| --- | --- | --- |
| General Python, data processing, notebooks | `environments/core/environment.yml` | Use this for basic scripts, data analysis, and common utilities. |
| Graph neural networks / GNN | `environments/gnn/environment.yml` | Use this when your project needs PyTorch Geometric, DGL, or CUDA-based graph learning. |
| Deep reinforcement learning / DRL | `environments/drl/environment.yml` | Use this for reinforcement learning, scheduling/dispatching agents, simulation-based policy learning, or DRL-based production decisions. |
| LLM-based agents | `environments/llm-agent/environment.yml` | Use this for API-based or Ollama-based agent workflows that do not need local vision-language models. |
| MLLM / multimodal models | `environments/mllm/environment.yml` | Use this for image-text, embedding, retrieval, and multimodal reasoning projects. |
| Production / Supply Chain Network | `environments/production-supply-chain-network/environment.yml` | Use this for global production network, supply chain modeling, optimization, simulation, and related analytics. |
| GNN + MLLM combined work | `environments/combined/gnn-mllm.yml` | Use this only if your project genuinely needs both graph learning and multimodal/LLM packages in one environment. |

## Core Compatibility Policy

The most sensitive dependency group is the GNN stack:

```text
python=3.10
pytorch=2.1.0
pytorch-cuda=12.1
pyg=2.5.2
dgl=2.0.0.cu121
```

DRL and MLLM environments also use the same PyTorch/CUDA base where possible. This reduces conflicts when projects later need shared utilities or partial code integration. For DRL, Stable-Baselines3 is pinned to a version compatible with `torch=2.1.0`; newer Stable-Baselines3 releases may require newer PyTorch.

When combining GNN with MLLM or agent packages, the GNN stack should remain the base. Do not let pip upgrade or replace `torch`, `torchvision`, `torchaudio`, CUDA packages, PyG, or DGL unless the whole group is updated and checked together.

## Installation Examples

Create the core environment:

```bash
conda env create -n uricard-core -f environments/core/environment.yml
conda activate uricard-core
```

Create the GNN environment:

```bash
conda env create -n uricard-gnn -f environments/gnn/environment.yml
conda activate uricard-gnn
```

Create the DRL environment:

```bash
conda env create -n uricard-drl -f environments/drl/environment.yml
conda activate uricard-drl
```

Create the MLLM environment:

```bash
conda env create -n uricard-mllm -f environments/mllm/environment.yml
conda activate uricard-mllm
```

Create the combined GNN + MLLM environment:

```bash
conda env create -n uricard-gnn-mllm -f environments/combined/gnn-mllm.yml
conda activate uricard-gnn-mllm
```

## Adding New Packages

If your project needs an additional package, please report it before adding it to the shared baseline. In general:

- Add common packages to `core` only when many projects need them.
- Add direction-specific packages to the corresponding environment folder.
- Avoid changing the GNN torch/CUDA/DGL/PyG stack casually.
- Avoid upgrading DRL libraries in a way that forces an incompatible PyTorch version.
- For experimental packages, prefer project-level `requirements.txt` first.

This repository should help us reduce environment-related syntax errors, import errors, version conflicts, and integration bugs when different project codes are merged later.
