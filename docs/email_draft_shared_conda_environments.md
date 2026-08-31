Subject: Shared Conda Environments for Upcoming Coding Work

Dear all,

After becoming familiar with Zotero and literature management, we will gradually start moving into programming work and environment setup this week. I believe many of you already have experience with Python, Anaconda, and virtual environment management. For those who are less familiar with these tools, I strongly recommend spending some time learning how to use Anaconda to create isolated Python environments and manage project-specific packages.

To support our upcoming coding, integration, and code merging work, I have prepared a shared repository for Conda environment baselines:

https://github.com/NTU-Industrial-AI-Lab/shared-conda-environments

The purpose is not to require everyone to install all packages. Different projects in our group have different needs, including GNN-based models, LLM-based agents, MLLM/multimodal models, and production/supply chain network modeling. Therefore, the repository provides several environment options. Please choose the smallest environment that matches your own project direction.

Recommended choices:

- For general Python, data analysis, notebooks, and common utilities, please use the `core` environment.
- For graph neural network or graph learning projects, please use the `gnn` environment.
- For LLM-based agent projects, especially API-based or Ollama-based workflows, please use the `llm-agent` environment.
- For multimodal LLM, image-text, embedding, or retrieval-related projects, please use the `mllm` environment.
- For global production network, supply chain modeling, optimization, simulation, and network analysis, please use the `production-supply-chain-network` environment.
- Only if your project really needs both GNN and MLLM packages in the same environment, please use the combined `gnn-mllm` environment.

This structure is intended to reduce future problems when we integrate and merge code from different projects. In particular, GNN-related packages such as PyTorch, CUDA, PyG, and DGL are sensitive to version conflicts. Keeping clear environment boundaries should help us avoid unnecessary syntax errors, import errors, package conflicts, and debugging time later.

If your project requires an additional package, please report it before adding it to the shared baseline. We can then decide together whether it should be added to the common `core` environment, a direction-specific environment, or only your own project-level requirements file.

Please try to create the environment that matches your current project and let me know if you encounter installation issues.

Best regards,
Muyang
