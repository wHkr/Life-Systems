# MkDocs -- Starting/Stopping/Adjusting

This document explains how to modify, test, and deploy the **Life Systems MkDocs website** using:

- **WSL Ubuntu** for the Linux development environment
- **Python virtual environment** stored in the Linux filesystem
- **VS Code Remote WSL** for editing
- **GitHub Pages** for deployment

> **Important:** The project files are stored on the Windows filesystem, but Python and MkDocs run from the WSL Linux environment.

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

The Python environment is stored in the Linux filesystem:

```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

Verify that Python and MkDocs are using the Linux virtual environment:

```bash
which python

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
```

```bash
which mkdocs

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

---

# 3. Open Project in VS Code

Navigate to the project stored on the Windows filesystem:

```bash
cd /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems
```

Open VS Code:

```bash
code .
```

VS Code should automatically open using the **WSL Remote environment**.

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

## Verify Python

```bash
which python

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
```

Check version:

```bash
python --version

# Expected:
# Python 3.12.3
```

---

## Verify MkDocs

```bash
which mkdocs

# Expected:
# /home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

Check version:

```bash
mkdocs --version

# Expected:
# mkdocs, version 1.6.1 from /home/aaron/venvs/StaticWebpage_Life-Systems/lib/python3.12/site-packages/mkdocs (Python 3.12)
```

---

# 5. Run Local Development Server

Start the MkDocs development server:

```bash
mkdocs serve
```

The website will be available locally at:

```text
http://127.0.0.1:8000
```

Changes made to Markdown files will automatically refresh.

---

# 6. Updating Website Files

After making changes:

## Stage changes

```bash
git add .
```

## Commit changes

```bash
git commit -m "Describe changes made"
```

## Push source files to GitHub

```bash
git push # Updates your code and markdown files on GitHub `main`
```

## Deploy website and start server

```bash
mkdocs gh-deploy # Updates your website

mkdocs serve
```

!!! abstract "`mkdocs gh-deploy` performs three actions"

    **1. Builds the website**

       Converts Markdown source files into a complete static website:

       ```
       Markdown → HTML/CSS/JavaScript
       ```

    **2. Creates or updates the `gh-pages` branch**

       Pushes the generated website files to the branch used by GitHub Pages.

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

       GitHub Pages detects the updated `gh-pages` branch and serves the generated website at your public URL.

---

# 7. Exit Workflow

## Kill MkDocs Server

From whichever terminal the `mkdocs serve` command was run from.
```bash
ctrl + c
```

## Close remote connection & VS Code

`File > Close remote connection`<br>
`File > Close Folder`<br>
`File > Close Window`<br>

## Kill Python Virtual Environment

Using same wsl terminal that you started VS Code from:
```bash
deactivate
```

# 8. Common Workflow

Normal editing cycle:

```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate

cd /mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems

code .

mkdocs serve
```

After completing changes:

```bash
git add .
git commit -m "Update documentation"
git push

mkdocs gh-deploy
```

---

# Troubleshooting

## MkDocs command not found

Check the virtual environment:

```bash
which mkdocs
```

If it does not point to:

```text
/home/aaron/venvs/StaticWebpage_Life-Systems/bin/mkdocs
```

reactivate the environment:

```bash
source ~/venvs/StaticWebpage_Life-Systems/bin/activate
```

---

## VS Code using Windows Python

Confirm VS Code is connected to WSL.

The bottom-left corner should show:

```text
WSL: Ubuntu
```

The Python interpreter should be:

```text
/home/aaron/venvs/StaticWebpage_Life-Systems/bin/python
```