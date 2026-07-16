# Making Adjustments

Use a `WSL` prompt and go to your linux file system
```powershell
wsl
cd ~
```

Activate your python environment from your linux file system
```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

Ensure your python and mkdocs are being used from the linux environment
```bash
which python
which mkdocs
```

Using same python virtual environment, `wsl` prompt, navigate to your windows file system and open the folder
```bash
cd /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems
code .
```

Start the server from a terminal within VS Code
```bash
mkdocs serve
```

## Making changes to files and folders

Upon making any changes, push changes to GitHub then re-deploy them
```bash
git add .
git commit -m "..."
git push
mkdocs gh-deploy
mkdocs serve
```