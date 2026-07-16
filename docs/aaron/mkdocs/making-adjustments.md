# Making Adjustments

## WSL Terminal
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
which python # /home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
which mkdocs # /home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

Using same python virtual environment, `wsl` prompt, navigate to your windows file system and open the folder
```bash
cd /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems
code .
```

## VS Code Terminal -- Will open as `WSL` terminal automatically
verify location and software, then start server
```bash
pwd # /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems

which python # /home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
python --version # Python 3.12.3

which mkdocs # /home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
mkdocs --version # mkdocs, version 1.6.1 from /home/aaron/venvs/StaticWebpage_Life-Systems/lib/python3.12/site-packages/mkdocs (Python 3.12)

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