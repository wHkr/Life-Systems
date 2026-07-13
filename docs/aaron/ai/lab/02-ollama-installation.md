# 02 -- Ollama Installation

## Purpose

Ollama provides the local AI runtime used by the AI Server Lab.

This stage installs, verifies, and tests the AI model engine before adding additional services such as:

- Docker containers
- Odysseus interface
- Memory systems
- Document processing
- Remote access

At the end of this stage, the workstation will be capable of running local AI models and responding through the Ollama API.

---

# Ollama Architecture

Ollama acts as the intelligence layer of the system.

The basic architecture:

```text
User Interface

      |
      |

Application Layer

(Odysseus / Future Interfaces)

      |
      |

Ollama API

      |
      |

Ollama Runtime

      |
      |

AI Model

(Gemma, Qwen, Phi, etc.)
```

---

# What is Ollama?

Ollama is a local AI model runtime.

It manages:

| Component | Purpose |
|---|---|
| Runtime | Executes AI models |
| Models | Downloaded AI weights |
| API | Allows applications to communicate with models |
| Storage | Maintains local model files |

Unlike cloud-based AI services, Ollama runs models locally on the user's hardware.

---

# System Considerations

This lab is being tested on:

| Component | Specification |
|---|---|
| CPU | Intel i7-9750H |
| RAM | 8GB |
| GPU | NVIDIA GTX 1650 4GB VRAM |
| OS | Windows 11 + WSL2 |

Because of hardware limitations, this system is designed for smaller optimized models.

Recommended models:

| Model | Purpose |
|---|---|
| Gemma 3 1B | Lightweight testing |
| Gemma 3 4B | General assistant |
| Phi-3 Mini | Writing and reasoning |
| Qwen 2.5 3B | Notes and organization |

---

# Verify Ollama Installation

Before continuing, verify Ollama is installed.

Open PowerShell:

```powershell
ollama --version
```

Expected result:

```text
ollama version x.x.x
```

If a version number appears, Ollama is installed correctly.

---

# Check Installed Models

View available models:

```powershell
ollama list
```

Example output:

```text
NAME          SIZE

gemma3:4b     3.3 GB
```

If no models are installed, continue to the next section.

---

# Download AI Model

For this lab, install:

```powershell
ollama pull gemma3:4b
```

This downloads the Gemma 3 4B model locally.

The model is stored on the computer and does not require cloud access.

---

# Test Local AI Generation

Start the model:

```powershell
ollama run gemma3:4b
```

Test prompt:

```text
Explain what you are in one sentence.
```

Expected result:

The model generates a response locally.

At this point:

✅ AI model downloaded  
✅ AI model running locally  
✅ No external AI service required  

---

# Understanding Model Storage

Ollama stores models locally.

Default Windows location:

```text
C:\Users\<username>\.ollama
```

Example:

```text
Ollama Models

├── gemma3:4b
├── qwen2.5:3b
├── phi3
└── future models
```

Each additional model requires additional storage.

Before downloading large models, verify available disk space.

---

# Understanding the Ollama API

Applications do not communicate with Ollama through the terminal.

Instead, they use the Ollama API.

Architecture:

```text
Application

      |

      |

Ollama API

      |

      |

AI Model
```

The default API address is:

```text
http://localhost:11434
```

---

# Test Ollama API

Verify the API is running:

```powershell
curl http://localhost:11434/api/tags
```

Expected result:

A JSON response containing installed models.

Example:

```json
{
  "models": [
    {
      "name": "gemma3:4b"
    }
  ]
}
```

This confirms:

- Ollama service is running
- Models are available
- Applications can communicate with Ollama

---

# Test AI Generation Through API

Test a request directly through the API:

```powershell
curl http://localhost:11434/api/generate `
-d '{"model":"gemma3:4b","prompt":"Explain Docker in one sentence.","stream":false}'
```

Expected result:

The API returns an AI-generated response.

The communication path is:

```text
Application

      |

      |

Ollama API

      |

      |

Gemma 3 Model

      |

      |

Response
```

---

# Security Considerations

By default, Ollama only listens locally.

Current configuration:

```text
Computer

localhost:11434

Only this machine can access Ollama
```

This is intentional.

Do not expose Ollama directly to the internet.

Future remote access will use:

```text
iPad

     |

     |

Tailscale Private Network

     |

     |

AI Server

     |

     |

Ollama
```

---

# Troubleshooting

## Ollama Command Not Found

Symptom:

```text
ollama is not recognized
```

Solution:

- Confirm Ollama is installed.
- Restart PowerShell.
- Verify the installation path.

---

## Model Runs Slowly

Possible causes:

- Limited RAM
- Large model size
- CPU-only inference

Solutions:

- Use a smaller model.
- Close unnecessary applications.
- Monitor memory usage.

---

## API Does Not Respond

Test:

```powershell
curl http://localhost:11434/api/tags
```

If unsuccessful:

1. Verify Ollama is running.
2. Restart Ollama.
3. Confirm port `11434` is available.

---

# Ollama Validation Complete

At this point the AI runtime should have:

| Component | Status |
|---|---|
| Ollama Installed | ✅ Ready |
| Model Downloaded | ✅ Ready |
| Local AI Generation | ✅ Ready |
| Ollama API | ✅ Ready |

The local AI engine is now operational.

---

# Next Step

Continue to:

```text
03 -- Docker Foundations and Networking
```

The next stage will introduce:

- Docker images
- Containers
- Compose files
- Networks
- Volumes
- Service management

Docker will become the management layer that organizes the AI services running around Ollama.