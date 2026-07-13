# 01 -- Environment Setup

## Verify your Environment

Before touching the AI server, make sure your development environment is healthy.

### ***Windows***

Verify:

    - Docker Desktop starts normally
    - Ollama is installed
    - NVIDIA drivers are working (If using GPU acceleration)
    - Git is installed

Commands:
```PowerShell
docker --version

ollama --version

git --version
```

---

### ***WSL***

Start `Ubuntu`

Verify:
```bash
python3 --version

pip --version

docker --version
```

---

### ***Virtual Environment***

Activate the MkDocs virtual Environment:
```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

Verify:
```bash
mkdocs serve
```

