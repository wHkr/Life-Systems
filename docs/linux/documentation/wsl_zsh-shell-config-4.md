# WSL -- Zsh shell customization

Current system is compatable with ***3 different*** environments.

Windows
│
├── Docker Desktop
│
├── VS Code
│
└── WSL Ubuntu
      │
      ├── Zsh
      ├── Starship
      ├── Docker CLI
      ├── GitHub CLI
      ├── uv
      └── Git

## Goal -- WSL becomes the primary development environment

That means:

    - VS Code connects to WSL
    - Git runs in WSL
    - Python runs in WSL
    - MkDocs runs in WSL
    - Docker commands run in WSL
    - GitHub CLI runs in WSL
It's a cleaner separation, and it's the workflow many linux-focused developers use even on windows


## Phase 1 -- Finish Starship

## Step 1

Open:
`~/.config/starship/starship.toml`

Replace its contents with:
```toml
add_newline = false
command_timeout = 1000

format = """
$os\
$username\
$hostname\
$python\
$docker_context\
$kubernetes\
$directory\
$git_branch\
$git_status\
$cmd_duration
"""

[character]
success_symbol = ""
error_symbol = ""

[os]
disabled = false
format = "[$symbol](bold white) "

[os.symbols]
Ubuntu = " "
Windows = " "
Arch = " "
Macos = " "

[username]
show_always = true
format = "[$user](bold white) "

[hostname]
ssh_only = false
format = "on [$hostname](bold yellow) "

[directory]
truncation_length = 2
home_symbol = "~"
format = "at [$path]($style) "

[git_branch]
symbol = " "
format = "via [$symbol$branch]($style) "

[git_status]
format = "[$all_status$ahead_behind]($style)"

[python]
disabled = false
symbol = "🐍 "
format = "via [$symbol$virtualenv]($style) "

[docker_context]
disabled = false
symbol = "🐳 "
format = "via [$symbol$context]($style) "

[kubernetes]
disabled = false
symbol = "☸ "
format = "on [$symbol$context($namespace)]($style) "

[cmd_duration]
min_time = 500
format = "took [$duration](bold yellow) "
```
This preserves my personal Starship prompt while also adding effects for Python, Docker, Kubernetes, & command timing.


## Step 2 -- Reload Zsh

Close & Reopen
or
```bash
source ~/.zshrc
```

## Step 3 -- Let's build aliases

Open:
`~/.config/zsh/10-aliases.zsh`

Start with:
```bash
# ==========================================
# Navigation
# ==========================================

alias ..="cd .."
alias ...="cd ../.."
alias ....="cd ../../.."

alias home="cd ~"

# ==========================================
# Listing
# ==========================================

alias ls="eza --icons"
alias ll="eza -lah --icons"
alias lt="eza --tree --level=2 --icons"

# ==========================================
# Files
# ==========================================

alias c="clear"

# ==========================================
# Git
# ==========================================

alias gs="git status"
alias ga="git add"
alias gc="git commit"
alias gp="git push"
alias gl="git log --graph --oneline --decorate"

# ==========================================
# Docker
# ==========================================

alias dps="docker ps"
alias di="docker images"
alias dc="docker compose"
alias dcup="docker compose up"
alias dcupd="docker compose up -d"
alias dcdown="docker compose down"
alias dclogs="docker compose logs -f"

# ==========================================
# Python
# ==========================================

alias py="python3"
alias pip="python3 -m pip"

alias py="uv run python"
alias pip="uv pip"

# ==========================================
# MkDocs
# ==========================================

alias serve="uv run mkdocs serve"
alias builddocs="uv run mkdocs build"
```
These are everyday commands, don't go to crazy adding weird ones.


## Step 4 -- Install eza

Because we're using it for `ls`
```bash
sudo apt update
sudo apt install eza
```


## Step 5 -- Verify

Run:
```bash
ll

gs

serve
```


## NEW RULE

### RULE #1
> Windows uses Windows virtual environments

### RULE #2
> WSL uses Linux virtual environments

Never the same `.venv`


## Python issue

Normal issue, Python always has some issue on linux

3 Choices:
    1. Keep using `python3`
    2. Install compatability package `python-is-python3`
    3. Build everything around `uv` - Doesn't replace a working python command

❯ uv python install cpython-3.12.3-linux-x86_64-gnu
Installed Python 3.12.3 in 6.57s
 + cpython-3.12.3-linux-x86_64-gnu (python3.12)

## We need to repair the Windows virtual environment

### First - Verify you are using some sort of python3

```bash
# alias py="python3"
py --version
Python 3.12.3
```

or download one
```bash
sudo apt update
sudo apt install python-is-python3
```

Verify:
```bash
python --version
```

Should see
```bash
Python 3.12.3 ish
```

### Second -- Windows virtual environment

The issue with my `wsl` is that using the Windows virtual environment and executable, it could damage my processes.

The purpose of `wsl` is so i can work on windows projects in a linux terminal. Windows is not supposed to be using scripts when it's trying to share those files with me

Windows virtual environments contain:
```bash
.venv/
└── Scripts/
```

Linux virtual environments contain:
```bash
.venv/
└── bin/
```
They are not interchangeable.


### Then fix the virtual environment

This is the important part.

I don't want your Linux tools using a Windows `.venv`.

Instead, inside WSL we'll recreate it:
```bash
rm -rf .venv
python -m venv .venv
source .venv/bin/activate

ls
```
Permissions Size User  Date Modified Name
drwxrwxrwx     - aaron 30 Jun 15:19   .git
.rwxrwxrwx   474 aaron 20 Jun 20:32   .gitignore
drwxrwxrwx     - aaron 30 Jun 16:43   .venv
drwxrwxrwx     - aaron 30 Jun 16:08   dist
drwxrwxrwx     - aaron 30 Jun 11:06   docs
.rwxrwxrwx  6.1k aaron 30 Jun 12:33   mkdocs.yml
.rwxrwxrwx   506 aaron 30 Jun 06:26   notes.txt
.rwxrwxrwx   717 aaron 29 Jun 21:47   requirements.txt
drwxrwxrwx     - aaron 30 Jun 09:10   site
```

That ls command solved my workflow;

I am working in
```bash
/mnt/c/users/aaron/engineering/projects/staticwebpage_Life-Systems
```

That means:

✅ WSL is running Linux.
❌ Your project lives on the Windows filesystem (NTFS).
❌ Your .venv is the Windows virtual environment (Scripts/, Lib/).

That explains all of the odd behavior.


//============================================================

## My recommendation

From now on, I'd separate your workflows like this:


### Windows

`C:\Users\aaron\Engineering\`
    - Notepad++
    - Windows PowerShell
    - Windows Python (if needed)
    - Windows-only tools


### WSL

`~/Projects/`
    - Git
    - Python
    - MkDocs
    - Docker
    - Node
    - Development

This becomes your primary development environment.

//============================================================


### Why?

When you work under `/mnt/c/`..., WSL has to translate Linux file operations into Windows file operations.

That causes issues with:
    - File permissions
    - Symlinks
    - File watchers
    - Performance
    - Virtual environments
    - Git line endings
    - Python tooling

Microsoft actually recommends storing Linux development projects inside the Linux filesystem (~) for these reasons.


powershell > wsl/
```bash
> pwd
`/mnt/c/Users/aaron/engineering/projects/StaticWebpage_Life-Systems`
```

Terminal > Open `Ubuntu` App
```bash
❯ pwd
/mnt/c/users/aaron/engineering/projects/StaticWebpage_Life-Systems
```

//============================================================


## What would I do -- Option A

Instead of continuing to work here:

`/mnt/c/users/aaron/engineering/projects/staticwebpage_Life-Systems`

I'd create:

`~/Projects/Documentation/Life-Systems`

Then copy the project:

```bash
cp -r /mnt/c/Users/aaron/Engineering/Projects/StaticWebpage_Life-Systems \ ~/Projects/Documentation/Life-Systems
```bash
```

(We'll actually use `rsync` later because it's better, but this illustrates the idea)


//============================================================

### Then

Delete the Windows `.venv` inside the Linux copy only

The Windows copy remains untouched

Inside the WSL copy:
```bash
rm -rf .venv
```

Then create a proper linux virtual environment
```bash
python -m venv .venv
```

Now we will get it
```
.venv/
├── bin/
├── include/
├── lib/
└── pyvenv.cfg
```
Instead of:
```bash
Scripts/
lib/
```

//============================================================

## Then

Install your dependencies
```bash
pip install -r requirements.txt
```

Then
```bash
python -m mkdocs serve
```
Everyone will be running natively in Linux

//==============================================================

## VS Code

This is the part most people miss

Instead of opening:
`C:\Users\aaron\Engineering\Projects\...`

You'll open:
`~/Projects/Documentation/Life-Systems`


//============================================================

## Here's my proposal

I'd like to make this your first "real" WSL project migration.

We'll:

1. Copy `Life-Systems` into `~/Projects/Documentation/`.
2. Recreate the virtual environment as a Linux .venv.
3. Reinstall the dependencies.
4. Open the project in VS Code using the WSL extension.
5. Verify that MkDocs, Mermaid, Git, and Starship all work from the Linux environment.

Once that succeeds, we'll use the same workflow for every future project. It gives you one consistent development environment instead of having to think about whether a project belongs to Windows or Linux. I think that's the cleanest path forward for the engineering workstation you're building.