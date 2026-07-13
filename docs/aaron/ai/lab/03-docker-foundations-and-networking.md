# 03 -- Docker Foundations and Networking

## Purpose

Docker provides the infrastructure layer for the AI Server Lab.

Instead of manually installing and configuring every service, Docker allows applications to run as isolated containers with defined:

- Software environments
- Network connections
- Storage locations
- Configuration settings

This makes the AI system easier to:

- Rebuild
- Backup
- Update
- Expand
- Troubleshoot

At the end of this stage, Docker will be configured and ready to run AI services.

---

# Docker Architecture

The AI Server Lab uses Docker Desktop with WSL2 integration.

The architecture:

```text
Windows 11

      |

      |

Docker Desktop

      |

      |

Docker Engine

      |

      |

WSL2 Ubuntu

      |

      |

Docker CLI

      |

      |

Containers
```

The Docker command inside WSL communicates with the Docker engine managed by Docker Desktop.

---

# What is Docker?

Docker is a platform for running applications inside containers.

A container packages:

- Application software
- Required dependencies
- Configuration
- Runtime environment

This allows the application to run consistently across different machines.

---

# Important Docker Concepts

## Images

An image is a template used to create containers.

Example:

```text
Ubuntu Image

        ↓

Ubuntu Container
```

Images are downloaded from container registries.

Example:

```bash
docker pull nginx
```

---

## Containers

A container is a running instance of an image.

Example:

```text
Image

nginx

   |

   ↓

Container

Running Web Server
```

Containers can be:

- Started
- Stopped
- Restarted
- Removed

without affecting the original image.

---

## Volumes

Containers are temporary by default.

If a container is deleted, its internal data is lost.

Volumes provide persistent storage.

Example:

```text
Container

     |

     |

Volume

     |

     |

Permanent Data
```

The AI Server Lab uses persistent storage for:

- AI models
- Documents
- Databases
- Configuration files

---

## Networks

Containers communicate through Docker networks.

Example:

```text
Odysseus Container

        |

        |

Docker Network

        |

        |

Ollama Service
```

Networks allow services to communicate without exposing everything to the internet.

---

# Verify Docker Installation

Before continuing, verify Docker is available.

Open WSL Ubuntu:

```bash
docker --version
```

Expected:

```text
Docker version x.x.x
```

---

Verify Docker can communicate with the engine:

```bash
docker info
```

A successful response shows:

- Docker server information
- Storage driver
- Runtime information

---

# First Docker Container

Before deploying AI services, test Docker with a simple container.

This confirms:

- Docker is working
- Images can download
- Containers can start
- Networking is functional

Run:

```bash
docker run hello-world
```

Expected output:

```text
Hello from Docker!

This message shows that your installation appears to be working correctly.
```

---

# Understanding the Test

The command:

```bash
docker run hello-world
```

performs several actions:

```text
docker run

      |

      |

Check for image

      |

      |

Download image if missing

      |

      |

Create container

      |

      |

Run container

      |

      |

Display output
```

---

# Docker Container Management

View running containers:

```bash
docker ps
```

View all containers:

```bash
docker ps -a
```

Example:

```text
CONTAINER ID

IMAGE

STATUS
```

---

Remove a container:

```bash
docker rm <container-id>
```

---

# Docker Images

View downloaded images:

```bash
docker images
```

Example:

```text
IMAGE

hello-world
```

Remove unused images:

```bash
docker image prune
```

---

# Docker Compose

## Purpose

Docker Compose allows multiple containers to be managed together.

Instead of manually running:

```text
Container A

Container B

Container C

Network

Storage
```

Compose defines the entire system in a YAML file.

Example:

```yaml
services:

  application:
    image: example
```

---

# Compose Architecture

The AI Server Lab will eventually use:

```text
docker-compose.yml

        |

        |

----------------------------

|            |             |

Ollama     Odysseus    ChromaDB

|            |             |

AI        Interface    Memory

----------------------------
```

---

# Create First Compose Test

Navigate to:

```bash
cd AI-Server-Lab
```

Create:

```text
docker-compose.yml
```

Add:

```yaml
services:

  hello:
    image: hello-world
```

---

# Start Compose Service

Run:

```bash
docker compose up
```

Docker will:

1. Read the YAML file
2. Download required images
3. Create containers
4. Start services

---

# Stop Compose Service

Stop and remove containers:

```bash
docker compose down
```

---

# Docker Networking

Docker automatically creates isolated networks.

Example:

```text
Container A

      |

      |

Docker Network

      |

      |

Container B
```

Services can communicate internally without being exposed externally.

---

# Port Mapping

Containers can expose services through ports.

Example:

```yaml
ports:

  - "3000:3000"
```

Meaning:

```text
Computer Port 3000

        |

        |

Container Port 3000
```

Example future services:

| Service | Port |
|---|---|
| Odysseus | 3000 |
| Ollama API | 11434 |
| ChromaDB | 8000 |

---

# Environment Variables

Services often require configuration values.

Example:

```yaml
environment:

  MODEL_NAME: gemma3:4b
```

Environment variables allow configuration without changing application files.

The AI Server Lab uses:

```text
.env
```

for storing configuration values.

---

# Persistent Storage Design

The AI Server Lab uses the following data structure:

```text
AI-Server-Lab

├── data
│
├── chromadb
│
├── documents
│
└── odysseus
```

Purpose:

| Folder | Function |
|---|---|
| chromadb | AI memory database |
| documents | Uploaded files |
| odysseus | Application data |

---

# Future AI Server Architecture

After completing this stage, Docker will support:

```text
                 User

                  |

                  |

              Odysseus

                  |

        --------------------

        |                  |

     Ollama             ChromaDB

        |                  |

    AI Models          Memory

                  |

             Documents
```

---

# Security Considerations

Docker services should not automatically be exposed to the internet.

Bad:

```text
Internet

    |

Open Docker Ports

    |

Services
```

Good:

```text
Private Network

      |

Docker Network

      |

Services
```

Remote access will later be handled through:

```text
iPad

 |

 |

Tailscale

 |

 |

AI Server
```

---

# Troubleshooting

## Docker Command Not Found

Check:

```bash
docker --version
```

If missing:

1. Open Docker Desktop.
2. Verify WSL Integration is enabled.
3. Restart WSL.

---

## Docker Daemon Not Running

Error:

```text
Cannot connect to Docker daemon
```

Solution:

Start Docker Desktop.

---

## Container Will Not Start

Check logs:

```bash
docker logs <container-name>
```

---

# Docker Validation Complete

At this stage:

| Component | Status |
|---|---|
| Docker Installed | ✅ Ready |
| Docker Engine Accessible | ✅ Ready |
| Containers Tested | ✅ Ready |
| Docker Compose Tested | ✅ Ready |
| Networking Concepts Understood | ✅ Ready |
| Persistent Storage Planned | ✅ Ready |

The workstation is now prepared for deploying AI services.

---

# Next Step

Continue to:

```text
04 -- Odysseus Deployment
```

The next stage will deploy the AI interface layer and connect it to Ollama.