# Personal Linux Workstation Setup - Ansible Automation

## Overview

This Ansible project provides a robust and opinionated solution for automating the setup and configuration of a personal Linux workstation (primarily Debian-based systems like Ubuntu). It streamlines the installation of essential software, development tools, cloud CLIs, and specialized environments for various domains, ensuring consistency and efficiency across your machines.

The project is designed with modularity, idempotency, and maintainability in mind, allowing users to select only the components they need during the setup process.

## Features

* **Modular Design**: Structured into distinct Ansible roles for clear separation of concerns (e.g., `base_system`, `programming_languages`, `devops_tools`, `cloud-cli`, etc.).
* **User-Driven Customization**: Utilizes a pre-playbook prompt (via a `prompt_user` role, not directly provided but implied) to select specific tools and environments for installation.
* **Comprehensive Tooling**: Covers a wide array of software, including:
    * **Base System Enhancements**: Essential utilities, Zsh with Oh My Zsh.
    * **Programming Languages**: Python, Java, Go, Rust, Node.js (via NVM).
    * **DevOps & Orchestration**: Docker, Kubernetes CLI (kubectl), Helm, Terraform, Ansible, Git, ArgoCD CLI, Jenkins CLI, MinIO Client, Ollama.
    * **AI/ML & Data Science**: JupyterLab, PyTorch, TensorFlow, Hugging Face CLI (with conditional GPU setup).
    * **Databases**: PostgreSQL (client & server), MySQL client, Redis client.
    * **Cloud CLIs**: AWS CLI, Google Cloud SDK (gcloud).
    * **IDEs & Editors**: Visual Studio Code.
    * **CLI Utilities**: `jq`, `yq`.
* **Idempotent Execution**: Ensures that running the playbook multiple times will achieve the desired state without re-installing or re-configuring unnecessarily.
* **"Latest by Default" or Version Pinning**: Allows flexible installation of the latest stable versions of tools or specific pinned versions as required.
* **GPU Support**: Intelligently installs NVIDIA drivers and CUDA toolkit only when a GPU is detected and a GPU-dependent AI/ML library is selected.
* **PATH Management**: Centralized and idempotent management of environment `PATH` variables for installed tools.
* **Zsh Integration**: Dynamically configures `~/.zshrc` with aliases, environment variables, and plugins based on installed components.

## Project Structure (Key Roles & Templates)
```bash
.
├── playbook.yml                 # Main playbook to orchestrate roles (To be created/reviewed)
├── inventory.ini                # Ansible inventory file (Example)
├── group_vars/
│   └── all.yml                  # Global variables for default tool versions etc. (To be created/reviewed)
└── roles/
├── base_system/             # Core OS setup, Zsh, common utilities
│   ├── tasks/main.yml
│   └── templates/.zshrc.j2  # Zsh configuration template
├── programming_languages/   # Python, Java, Go, Rust, Node.js
│   └── tasks/main.yml
├── devops_tools/            # Kubernetes, Docker, Terraform, Ansible, etc.
│   └── tasks/main.yml
├── ai-ml-dataScience/       # Jupyter, PyTorch, TensorFlow, HuggingFace
│   ├── tasks/main.yml
│   └── tasks/gpu_setup.yml  # Dedicated for NVIDIA/CUDA setup
├── databases/               # PostgreSQL, MySQL, Redis clients/servers
│   ├── tasks/main.yml
│   ├── tasks/db_clients.yml
│   └── tasks/postgresql_server.yml
├── cli_tools/               # jq, yq
│   └── tasks/main.yml
├── containerization/        # Docker Engine
│   ├── tasks/main.yml
│   └── handlers/main.yml
├── version_control/         # Git
│   └── tasks/main.yml
├── cloud-cli/               # AWS CLI, Google Cloud SDK
│   ├── tasks/main.yml
│   ├── tasks/aws_cli.yml
│   └── tasks/gcloud_cli.yml
└── ide_editors/             # VS Code
└── tasks/main.yml
```