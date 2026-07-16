# MkDocs Development Workflow

This document explains the complete development workflow for the **Life Systems MkDocs website**, including:

- Starting the WSL development environment
- Activating the Python/MkDocs toolchain
- Editing with VS Code Remote WSL
- Testing changes locally
- Publishing updates through GitHub Pages

> **Important:** The project files are stored on the Windows filesystem, but Python, MkDocs, and the virtual environment run from the WSL Linux environment.

---

# 1. Open WSL Environment

Open a **WSL terminal**.

Navigate to your Linux home directory:

```bash
wsl
cd ~
```

---

# 2. Activate Python Virtual Environment

The Python environment is stored in the WSL Linux filesystem:

```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

Verify Python is using the Linux virtual environment:

```bash
which python

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
```

Verify MkDocs is using the Linux virtual environment:

```bash
which mkdocs

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

---

# 3. Open Project in VS Code

The website source files are stored on the Windows filesystem.

Navigate to the project:

```bash
cd /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems
```

Open VS Code:

```bash
code .
```

VS Code should automatically open using the **Remote WSL environment**.

Verify the bottom-left corner of VS Code shows:

```text
WSL: Ubuntu
```

---

# 4. Verify VS Code Environment

Open the VS Code terminal.

The terminal should automatically open as a WSL terminal.

Verify the project location:

```bash
pwd

# Expected:
# /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems
```

---

## Verify Python Interpreter

```bash
which python

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
```

Check Python version:

```bash
python --version

# Expected:
# Python 3.12.3
```

---

## Verify MkDocs Installation

```bash
which mkdocs

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

Check MkDocs version:

```bash
mkdocs --version

# Expected:
# mkdocs, version 1.6.1 from /home/aaron/venvs/StaticWebpage_Life-Systems/lib/python3.12/site-packages/mkdocs (Python 3.12)
```

---

# 5. Local Development Server

Before publishing changes, test the website locally.

Start the MkDocs development server:

```bash
mkdocs serve
```

The website will be available at:

```text
http://127.0.0.1:8000
```

Changes made to Markdown files will automatically refresh the website.

Stop the server with:

```text
CTRL + C
```

---

# 6. Updating Website Files

After making and testing changes:

## Stage Changes

```bash
git add .
```

---

## Commit Changes

```bash
git commit -m "Describe changes made"
```

Example:

```bash
git commit -m "Updated pool maintenance documentation"
```

---

## Push Source Files to GitHub

```bash
git push
```

This updates the source repository:

```
main branch

├── docs/
├── mkdocs.yml
└── source files
```

---

## Deploy Website

Run:

```bash
mkdocs gh-deploy
```

This updates the public website.

!!! abstract "`mkdocs gh-deploy` performs three actions"

    **1. Builds the website**

    Converts Markdown source files into a complete static website:

    ```
    Markdown → HTML/CSS/JavaScript
    ```

    **2. Creates or updates the `gh-pages` branch**

    Pushes the generated website files to the branch used by GitHub Pages:

    ```
    main branch

    ├── docs/
    ├── mkdocs.yml
    └── source files


    gh-pages branch

    ├── index.html
    ├── assets/
    └── generated website
    ```

    **3. Deploys the website through GitHub Pages**

    GitHub Pages detects the updated `gh-pages` branch and serves the generated website at the public URL.

---

# 7. Exit Development Environment

## Stop MkDocs Server

If the development server is running:

```text
CTRL + C
```

---

## Close VS Code Remote Session

Use:

```
File > Close Remote Connection
```

Then:

```
File > Close Window
```

---

## Deactivate Python Environment

Using the WSL terminal where the environment was activated:

```bash
deactivate
```

---

# 8. Normal Development Workflow

## Start Development

```bash
wsl

source ~/venvs/StaticWebpage_Life-Systems/bin/activate

cd /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems

code .

mkdocs serve
```

---

## Publish Updates

After testing changes:

```bash
git add .

git commit -m "Update documentation"

git push

mkdocs gh-deploy
```

---

# Troubleshooting

## MkDocs Command Not Found

Check the active MkDocs location:

```bash
which mkdocs
```

Expected:

```text
/home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

If incorrect, reactivate the environment:

```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

---

## VS Code Using Windows Python

Confirm VS Code is connected to WSL:

```
WSL: Ubuntu
```

The selected Python interpreter should be:

```text
/home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
```

Do not use:

```text
C:\Python...
```

or:

```text
/usr/bin/python
```

The correct interpreter is the Python installation inside the WSL virtual environment.