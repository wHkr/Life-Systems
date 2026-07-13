# 01 -- Environment Setup

## Purpose

The purpose of this stage is to prepare the workstation for AI server development.

Before installing AI services, containers, or automation systems, the underlying environment must be verified and configured.

This includes:

- Hardware verification
- Windows configuration
- WSL2 configuration
- Python environment setup
- Docker Desktop integration
- Project structure creation

After completing this stage, the workstation will be ready for AI infrastructure development.

---

# System Requirements

This lab is designed around a Windows workstation using:

- Windows 11
- WSL2 Ubuntu
- Docker Desktop
- Local AI models through Ollama

---

## Recommended Minimum Hardware

| Component | Recommendation |
|---|---|
| CPU | 6+ cores |
| RAM | 16GB recommended |
| Storage | 100GB available |
| GPU | Optional |

---

## Current Lab Machine

This environment is being tested on:

| Component | Specification |
|---|---|
| CPU | Intel i7-9750H |
| RAM | 8GB |
| GPU | NVIDIA GTX 1650 4GB VRAM |
| OS | Windows 11 + WSL2 Ubuntu |

> Note: This system is suitable for learning, testing, and smaller AI models. Larger models may require additional RAM or dedicated hardware.

---

# Required Software

The AI Server Lab requires the following software.

---

## Windows Applications

Required:

- Docker Desktop
- Ollama
- Git
- Visual Studio Code

Optional:

- NVIDIA Drivers  
  Required only for GPU acceleration.

---

## WSL Packages

Required:

- Python 3
- pip
- python3-venv
- curl
- git
- unzip
- build-essential

Install:

```bash
sudo apt update

sudo apt install -y \
python3-venv \
python3-pip \
curl \
git \
unzip \
build-essential
```

---

## Package Purpose

| Package | Purpose |
|---|---|
| python3-venv | Creates isolated Python environments |
| pip | Installs Python packages |
| curl | API testing and downloads |
| git | Version control |
| unzip | File management |
| build-essential | Compiling dependencies |

---

# Project Directory

The AI Server Lab uses the following structure:

```text
AI-Server-Lab

├── backups
├── compose
├── data
├── docs
├── logs
├── scripts
│
├── .env
├── docker-compose.yml
├── README.md
└── notes.md
```

---

## Directory Purpose

| Folder | Function |
|---|---|
| compose | Docker service definitions |
| data | Persistent application data |
| docs | Lab documentation |
| logs | Service logs |
| backups | Recovery files |
| scripts | Automation tools |

---

# Verify Windows Environment

Before continuing, verify required Windows applications.

---

## Verify Installed Software

Open PowerShell:

```powershell
docker --version

ollama --version

git --version
```

Expected result:

Each command returns an installed version.

---

# Verify WSL Environment

Open Ubuntu WSL.

Check Python:

```bash
python3 --version
```

Check pip:

```bash
pip3 --version
```

Check Docker:

```bash
docker --version
```

> Docker Desktop must be running for the Docker command to work.

---

# Docker Desktop Integration with WSL

## Overview

Docker is not installed directly inside WSL.

Instead, Docker Desktop runs the Docker engine on Windows and provides access through WSL integration.

Architecture:

```text
Windows

Docker Desktop
      |
      |
 Docker Engine
      |
      |
WSL Integration
      |
      |
Ubuntu Docker CLI
```

The `docker` command inside WSL is only the client.

The actual Docker daemon (`dockerd`) runs inside Docker Desktop.

---

## Enable WSL Integration

1. Open Docker Desktop

2. Navigate to:

```
Settings
    >
Resources
    >
WSL Integration
```

3. Enable:

```
Enable integration with my default WSL distro
```

4. Enable your Ubuntu distribution.

5. Apply and restart Docker Desktop.

---

# Why Does Docker Desktop Need to Run Before WSL Can Use Docker?

Docker Desktop provides the Docker engine.

Without Docker Desktop:

```text
Ubuntu WSL

docker command

       X

No Docker daemon available
```

With Docker Desktop:

```text
Ubuntu WSL

docker command

       |

Docker Desktop Engine

       |

Containers
```

Benefits of this configuration:

- One Docker installation to maintain
- Docker Desktop manages updates
- Windows and WSL share containers and images
- Easier future GPU support

---

# Python Virtual Environment

The Life Systems documentation project uses a Python virtual environment.

Activate:

```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

Verify MkDocs:

```bash
mkdocs serve
```

The documentation website should load successfully.

---

# Final Validation

The environment is complete when all checks pass.

---

## Windows PowerShell

```powershell
docker --version

ollama --version

git --version
```

---

## WSL Ubuntu

```bash
python3 --version

pip3 --version

docker --version
```

---

# Environment Validation Complete

At this point the workstation should have:

| Component | Status |
|---|---|
| Windows Environment | ✅ Ready |
| WSL Ubuntu | ✅ Ready |
| Python 3 | ✅ Ready |
| pip | ✅ Ready |
| Python Virtual Environment | ✅ Ready |
| Docker Desktop | ✅ Ready |
| Docker WSL Integration | ✅ Ready |
| Project Structure | ✅ Ready |

The workstation is now prepared for AI server development.

---

# Next Step

Continue to:

```
02 -- Ollama Installation
```