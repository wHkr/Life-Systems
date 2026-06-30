# WSL -- Configuring the `.zsh` files

## Phase 1 - Prepare the Shell

## Step 1 -- Create the folders and modules

Go to config folder:
```bash
cd ~/.config
```

Create the zsh folder:
```bash
mkdir -p zsh
```

Create every module:
```bash
touch zsh/00-environment.zsh
touch zsh/10-aliases.zsh
touch zsh/20-functions.zsh
touch zsh/30-git.zsh
touch zsh/40-docker.zsh
touch zsh/50-python.zsh
touch zsh/60-node.zsh
touch zsh/70-completion.zsh
touch zsh/80-prompt.zsh
touch zsh/99-local.zsh
```

Verify.
```bash
tree ~/.config/zsh
```

Should look like
```bash
~/.config/zsh

00-environment.zsh
10-aliases.zsh
20-functions.zsh
30-git.zsh
40-docker.zsh
50-python.zsh
60-node.zsh
70-completion.zsh
80-prompt.zsh
99-local.zsh
```

## Step 2 -- Open 00-environment.zsh

Open:
    `~/.config/zsh/00-environment.zsh`

Paste only this:
```bash
# ==========================================
# Environment Variables
# ==========================================

export XDG_CONFIG_HOME="$HOME/.config"

# History
HISTSIZE=1000
SAVEHIST=1000
HISTFILE="$HOME/.zsh_history"

# History behavior
setopt histignorealldups
setopt sharehistory
```

## Step 3 -- Open 80-prompt.zsh

Open
    `~/.config/zsh/80-prompt.zsh`

Paste:
```bash
# ==========================================
# Prompt
# ==========================================

eval "$(starship init zsh)"
```

## Step 4 -- Open 70-completion.zsh

Open:
    `~/.config/zsh/70-completion.zsh`

Paste
```bash
# ==========================================
# Completion
# ==========================================

autoload -Uz compinit
compinit
```

## Step 5 -- 10-aliases.zsh

Open `10-aliases.zsh`

Leave empty


## Step 6 -- 20-functions.zsh

Open `20-functions.zsh`

Leave empty


## Step 7 -- Open `.zshrc`

Open
    `.zshrc`
DO NOT DELETE IT

Comment everything out
```zsh
# old configuration
# autoload promptinit
# promptinit
```
Then replace the top with
```zsh
# ==========================================
# Aaron's Engineering Workstation
# Bootstrap Loader
# ==========================================

for file in "$HOME/.config/zsh/"*.zsh; do
    source "$file"
done
```

## Step 8 -- Restart WSL

Run
```bash
echo $XDG_CONFIG_HOME
```

Should print
```bash
/home/aaron/.config
```

Then
```bash
starship explain
```
should work

Then
```bash
echo $HISTFILE
```

should print
```bash
/home/aaron/.zsh_history
```

Then
```bash
setopt | grep history
```

you should get
```bash
histignorealldups

sharehistory
```

//===========================================================

## Phase 2 -- Build the Shell

## 10-aliases.zsh

This is your toolbox
Organize it:
```bash
# ==========================================
# Navigation
# ==========================================

alias ..="cd .."
alias ...="cd ../.."
alias ....="cd ../../.."

# ==========================================
# Listing
# ==========================================

alias ll="ls -lah"
alias la="ls -A"

# ==========================================
# Files
# ==========================================

alias c="clear"

# ==========================================
# Tree
# ==========================================

alias tree="tree -C"
```

## 20-functions.zsh

Functions are your little programs

Example:
```bash
# mkdir && cd/_dir
mkcd () {
    mkdir -p "$1"
    cd "$1"
}

# extract archive.tar.gz
extract () {

    if [[ -f "$1" ]]; then
        case "$1" in

            *.zip) unzip "$1" ;;
            *.tar.gz) tar -xzf "$1" ;;
            *.tar.xz) tar -xJf "$1" ;;
            *.tar) tar -xf "$1" ;;

            *) echo "Unknown archive"

        esac
    fi
}
```


## 30-git.zsh

Git deserves its own file
```zsh
alias gs="git status"

alias ga="git add"

alias gc="git commit"

alias gp="git push"

alias gl="git log --oneline --graph --decorate"

alias gco="git checkout"

alias gb="git branch"
```


## 40-docker.zsh

```bash
alias dps="docker ps"

alias di="docker images"

alias dcu="docker compose up"

alias dcud="docker compose up -d"

alias dcd="docker compose down"

alias dcl="docker compose logs"

alias dexec="docker exec -it"
```


## 50-python.zsh

```bash
alias py="python3"

alias pip="python3 -m pip"

alias venv="python3 -m venv .venv"

alias activate="source .venv/bin/activate"
```


## 60-node.zsh

```bash
alias ni="npm install"

alias ns="npm start"

alias nd="npm run dev"

alias nb="npm run build"
```


## 70-completion.zsh

```bash
autoload -Uz compinit

compinit
```


## 80-prompt.zsh

```zsh
eval "$(starship init zsh)"
```

## 99-local.zsh

This **NEVER** get commited
```zsh
API Keys

Passwords

Experimental aliases

Machine-specific settings
```
Git ignores it


### Why 99?

Because it loads LAST
it overrides everything else

### The next folder

Now we build
`~/.config/git`
This get the same `.zshrc` treatment

Instead of `.gitconfig` being 500 lines

We'll have
```zsh
~/.config/git/

config

aliases

ignore

attributes
```

and your `.gitconfig` becomes about *5* lines


### Goal with this

To use this one command to build your entire environment from scratch from any location onto any computer

One command:
```bash
git clone your/dotfiles
```

One script
```bash
./bootstrap.sh
```
//=========================================================

## Phase 3 -- Git Configuration

Going to modularize Git just like we did Zsh

## Step 1 -- Create the structure

```bash
cd ~/.config/git
```

if it doesn't exist:
```bash
mkdir -p ~/.config/git
cd ~/.config/git
```

Create the files:
```bash
touch config
touch aliases
touch ignore
touch attributes
```

Verify:
```bash
tree ~/.config/git
```

You should see
```
~/.config/git
├── aliases
├── attributes
├── config
└── ignore
```


## Step 2 - Create your global ignore

open:
```bash
~/.config/git/ignore
```

Paste:
```bash
# Windows
Thumbs.db
Desktop.ini

# macOS
.DS_Store

# Python
__pycache__/
*.py[cod]
.venv/

# Node
node_modules/

# Editors
.vscode/
.idea/

# Vim
*.swp
*.swo

# Logs
*.log
```
Applies to every repo on your machine


## Step 3 -- Create Git aliases

Open
```bash
~/.config/git/aliases
```

Paste:
```bash
[alias]
    st = status
    br = branch
    co = checkout
    sw = switch
    ci = commit
    ca = commit --amend
    lg = log --graph --decorate --oneline --all
    last = log -1 HEAD
```


## Step 4 -- Building the main config

Open
```bash
~/.config/git/config
```

Start with:
```ini
[user]
    name = Your Name
    email = your@email.com

[init]
    defaultBranch = main

[pull]
    rebase = false

[core]
    editor = nano

[color]
    ui = auto

[include]
    path = ~/.config/git/aliases
```


## Step 5 -- Shrink `.gitconfig`

Open
```bash
~/.gitconfig
```

Replace it with:
```ini
[include]
    path = ~/.config/git/config

[core]
    excludesfile = ~/.config/git/ignore

[core]
    attributesfile = ~/.config/git/attributes
```

Notice what happened?

Your actual configuration is now inside .config.

.gitconfig is just the bootstrap.

Exactly like .zshrc.


## Step 6 -- Test

Run:
```bash
git config --list --show-origin
```

**Great Git Command**
Tells you:
    - which file each setting came from,
    - what Git is actually loading
you'll see entries from:
`~/.gitconfig`
and
`~/.config/git/config`
That's how you know the modular setup is working


//=============================================================

## After Git...

