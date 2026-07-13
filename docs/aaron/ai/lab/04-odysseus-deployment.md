# 04 -- Odysseus Deployment

**READ**
```MARKDOWN
One important note before you actually deploy this: when we get to the hands-on portion, we should not blindly use image: odysseus because your original Odysseus setup had specific containers (odysseus, chromadb, ntfy, searxng) and a real image name.
```

## Purpose

Odysseus provides the user interface and orchestration layer for the AI Server Lab.

While Ollama is responsible for running AI models, Odysseus provides the environment where users interact with those models.

Odysseus allows the system to become more than a simple chatbot by providing:

- User interface
- Model connections
- Conversation management
- File interaction
- Tool integration
- Future memory integration

At the end of this stage, Odysseus will be running as a Docker service and communicating with Ollama.

---

# AI Server Architecture

The completed architecture:

```text
                    User

                      |

                      |

                 Odysseus

                      |

              -----------------

              |               |

           Ollama          Memory

              |               |

         AI Models       ChromaDB

              |

              |

        Business Documents
```

---

# Understanding Odysseus

Odysseus is not the AI model.

The responsibilities are separated:

| Component | Responsibility |
|---|---|
| Ollama | Runs AI models |
| Odysseus | User interface and management |
| ChromaDB | Stores AI memory |
| Docker | Runs and manages services |
| Tailscale | Provides secure remote access |

This separation allows each component to be upgraded independently.

---

# Deployment Strategy

Odysseus will run inside Docker.

The deployment uses:

```text
Docker Compose

        |

        |

Odysseus Container

        |

        |

Docker Network

        |

        |

Ollama Service
```

---

# Directory Preparation

The AI Server Lab uses:

```text
AI-Server-Lab

├── compose
│
│   ├── odysseus.yml
│   ├── chromadb.yml
│   └── future-services.yml
│
├── data
│
│   └── odysseus
│
└── logs
```

---

# Environment Configuration

Odysseus uses environment variables for configuration.

The main configuration file:

```text
.env
```

Example:

```env
ODYSSEUS_ADMIN_USER=admin

OLLAMA_HOST=http://host.docker.internal:11434
```

Purpose:

| Variable | Function |
|---|---|
| ODYSSEUS_ADMIN_USER | Creates administrator account |
| OLLAMA_HOST | Connects Odysseus to Ollama |

---

# Connecting Odysseus to Ollama

The communication path:

```text
Odysseus Container

        |

        |

Docker Network

        |

        |

Ollama API

        |

        |

AI Model
```

Ollama provides the intelligence.

Odysseus provides the interface.

---

# Docker Compose Configuration

Create:

```text
compose/odysseus.yml
```

Example structure:

```yaml
services:

  odysseus:

    image: odysseus

    container_name: odysseus

    restart: unless-stopped

    ports:

      - "3000:3000"

    environment:

      OLLAMA_HOST: http://host.docker.internal:11434

    volumes:

      - ../data/odysseus:/app/data
```

---

# Start Odysseus

From:

```bash
AI-Server-Lab
```

Run:

```bash
docker compose -f compose/odysseus.yml up -d
```

The `-d` option runs the container in the background.

---

# Verify Container Status

Check running containers:

```bash
docker ps
```

Expected:

```text
odysseus

STATUS

Up
```

---

# View Logs

If there are problems:

```bash
docker logs odysseus
```

Follow live logs:

```bash
docker logs -f odysseus
```

---

# Access Odysseus

Open a browser:

```text
http://localhost:3000
```

The Odysseus interface should load.

---

# First Connection Test

Verify the complete chain:

```text
Browser

    |

    |

Odysseus

    |

    |

Ollama API

    |

    |

Gemma 3 Model
```

Test:

Ask:

```text
Explain what model you are running.
```

A successful response confirms:

✅ Odysseus is running  
✅ Ollama is reachable  
✅ AI model is responding  

---

# Data Persistence

Odysseus stores important information.

Persistent storage:

```text
AI-Server-Lab

data/

└── odysseus
```

This protects:

- Settings
- User data
- Configuration

from container removal.

---

# Updating Odysseus

Containers should be replaceable.

Update process:

```bash
docker compose pull

docker compose up -d
```

Docker will:

1. Download updated image.
2. Replace old container.
3. Maintain stored data.

---

# Stopping Odysseus

Stop the service:

```bash
docker compose -f compose/odysseus.yml down
```

The container stops, but persistent data remains.

---

# Troubleshooting

## Odysseus Cannot Connect to Ollama

Check Ollama:

```bash
curl http://localhost:11434/api/tags
```

If unavailable:

- Start Ollama.
- Verify the model exists.

---

## Port Already In Use

Error:

```text
port 3000 already allocated
```

Find the service:

```bash
docker ps
```

Change the port mapping if needed.

Example:

```yaml
ports:

 - "8080:3000"
```

---

## Container Keeps Restarting

Check logs:

```bash
docker logs odysseus
```

Common causes:

- Incorrect environment variables
- Missing storage permissions
- Ollama unavailable

---

# Odysseus Validation Complete

At this stage:

| Component | Status |
|---|---|
| Docker Deployment | ✅ Ready |
| Odysseus Container | ✅ Ready |
| Web Interface | ✅ Ready |
| Ollama Connection | ✅ Ready |
| Persistent Storage | ✅ Ready |

The AI interface layer is now operational.

---

# Current Architecture

```text
                         User

                          |

                          |

                      Odysseus

                          |

              ---------------------

              |                   |

           Ollama              Future

              |              Services

              |

          AI Models
```

---

# Next Step

Continue to:

```text
05 -- Tailscale Remote Access
```

The next stage will allow secure access from devices such as an iPad without exposing AI services directly to the internet.