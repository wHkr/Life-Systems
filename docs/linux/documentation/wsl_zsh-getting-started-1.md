# Linux

## Folder Architecture

```markdown
Ubuntu (WSL)
│
├── Zsh
├── Starship
├── Git
├── GitHub CLI
├── SSH
├── GPG
├── Docker CLI
├── Docker Compose
├── Python
├── uv
├── pipx
├── Node.js
├── npm
├── pnpm
├── MkDocs
├── Neovim (optional)
├── fzf
├── zoxide
├── bat
├── eza
├── ripgrep
├── fd
├── tmux
├── lazygit
└── aliases/functions
```

## Docker Dev Env

```markdown
engineering-dev/
│
├── Dockerfile
├── docker-compose.yml
├── install.sh
├── README.md
├── dotfiles/
├── scripts/
└── bootstrap/
```

## Bootstrap Script

```bash
git clone <your-dotfiles>
cd dotfiles
./bootstrap.sh
```
The script can:

Install packages
Configure Zsh
Install Starship
Restore aliases
Configure Git
Configure SSH
Install Python tooling
Install Node tooling
Set up your MkDocs environment

## Backup Strategy

We'll keep:

    📁 Dotfiles in Git
    📁 Docker image definition in Git
    📁 MkDocs projects in Git
    📁 Documentation templates in Git

---

## Phase 0 -- Philosophy

***XDG Base Directory Specification*** should be followed whenever possible.
    - A standard defined by `freedesktop.org` to organize user data, configuration, cache, state, and runtime files into specific directories, preventing the clutter of dotfiles in the home directory.

## Dotfiles

```markdown
~/
├── .config/
│   ├── starship/
│   ├── git/
│   ├── gh/
│   ├── nvim/
│   └── ...
│
├── .zsh/
│   ├── aliases.zsh
│   ├── docker.zsh
│   ├── git.zsh
│   ├── python.zsh
│   ├── prompt.zsh
│   ├── functions.zsh
│   ├── exports.zsh
│   └── local.zsh
│
├── .zshrc
├── .zprofile
└── .gitconfig
```

## Phase 1 -- Install the foundation

Typical packages you find on any linux machine:
```bash
sudo apt update

sudo apt install -y \  # '-y'; auto-answer Yes to everything
    git \
    curl \
    wget \
    unzip \
    zip \
    build-essential \
    ca-certificates \
    software-properties-common \
    gnupg \
    tree \
    jq \
    ripgrep \
    fd-find \
    fzf \
    bat \
    tmux \
    htop \
    btop \
    zoxide
```

## Phase 2 -- Shell

Install zsh
```bash
sudo apt install zsh
```
Then:
```bash
chsh -s $(which zsh)
```
Close WSL
Reopen WSL
You're now running ZSH

## Phase 3 -- Shell Prompt

Install Starship
```bash
sudo apt update && sudo apt upgrade

curl -sS https://starship.rs/install.sh | sh
```
**Don't config. anything yet**

## Phase 4 -- Build your Config tree

Don't throw everything into `.zshrc`

```bash
mkdir -p ~/.config/zsh
```
Inside;

```bash
~/.config/zsh

aliases.zsh

docker.zsh

exports.zsh

functions.zsh

git.zsh

python.zsh

prompt.zsh

completion.zsh

local.zsh
```

## Phase 5 -- Shrink `.zshrc`

```zsh

# Starship
eval "$(starship init zsh)"

# Load configuration
for file in ~/.config/zsh/*.zsh; do
    source "$file"
done
```
That's it, nothing else

## Phase 6 -- Starship `.toml`

Create:
    `~/.config/starship/starship.toml`

## Phase 7 -- 📁 ~/Projects

```
~/Projects/                  📁
├── Documentation/           📁
├── Development/             📁
├── Docker/                  📁
├── Testing/                 📁
└── Archive/                 📁
```

## Phase 8 -- 📁 ~/Containers

```
~/Containers/                📁
├── Base/                    📁
├── Python/                  📁
├── Node/                    📁
├── AI/                      📁
└── Utilities/               📁
```

## Phase 9 -- 📁 ~/.config/git

```
~/.config/git/               📁
├── config                   📄 # Standard git config files
├── ignore                   📄
└── attributes               📄
```

        ```
        /-- config --/

        This replaces a huge .gitconfig.
        Contains things like:
            user name
            aliases
            editor
            merge settings

        /-- ignore --/

        Global ignores.
        Things like:
            .DS_Store
            Thumbs.db
            *.swp
            .vscode/

        /-- attributes --/

        Line endings.
        Diff behavior.
        Binary file handling.
                ```

## Phase 10 -- 🔐 ~/.ssh

```
~/.ssh/                      📁
├── config                   📄
├── known_hosts              📄
├── id_ed25519               🔑
├── id_ed25519.pub           🔑
└── authorized_keys          📄
```

## Finished Picture

```
~
│
├── Projects
│
├── Containers
│
├── Scripts
│
├── .config
│   ├── git
│   ├── gh
│   ├── zsh
│   ├── starship
│   ├── nvim
│   ├── tmux
│   └── ...
│
├── .cache
│
├── .local
│
├── .ssh
│
├── .zshrc
│
└── .gitconfig
```

## Phase 11 -- Decide what lives where

**Master Blueprint**
Home Directory
```
~
├── Projects/                    # Everything you create
│
├── Containers/                  # Docker projects
│
├── Scripts/                     # Utility scripts
│
├── Downloads/                   # Temporary downloads
│
├── .config/                     # Application configuration
│
├── .local/                      # User-installed programs/data
│
├── .cache/                      # Temporary caches
│
├── .ssh/                        # SSH keys
│
├── .gnupg/                      # GPG keys
│
├── .zshrc                       # Tiny bootstrap file
│
└── .gitconfig                   # Tiny bootstrap file
```

## Phase 12 -- Projects

`~/Projects/
```
├── Documentation/
│   ├── Life-Systems/
│   ├── ReAbility-Lab/
│   ├── Templates/
│   └── Research/
│
├── Software/
│   ├── Python/
│   ├── Web/
│   ├── PowerShell/
│   ├── Bash/
│   └── Arduino/
│
├── Infrastructure/
│   ├── Docker/
│   ├── Networking/
│   ├── Tailscale/
│   ├── Linux/
│   └── Kubernetes/
│
├── Testing/
│
└── Archive/
```

## Phase 13 -- Containers

`~/Containers
```
├── AI/
│   ├── Odysseus/
│   ├── Ollama/
│   ├── Open-WebUI/
│   └── SearXNG/
│
├── Development/
│   ├── Python/
│   ├── Node/
│   └── MkDocs/
│
├── Databases/
│   ├── PostgreSQL/
│   └── Redis/
│
├── Utilities/
│   ├── Nginx/
│   ├── Portainer/
│   └── Watchtower/
│
└── Templates/
```
```
## Phase 14 -- Scripts

This becomes your toolbox
```
~/Scripts/

├── backup.sh
├── bootstrap.sh
├── docker-clean.sh
├── git-update.sh
├── mkdocs-build.sh
├── python-update.sh
└── system-info.sh
```
Anything you run belongs here


## Phase 15 -- `.config`

```
~/.config/

├── bat/
├── btop/
├── fd/
├── fzf/
├── git/
├── gh/
├── starship/
├── tmux/
├── zoxide/
├── zsh/
└── nvim/
```

## Phase 16 -- Your Zsh Modules

Instead of a 700-line `.zshrc`, you have focused files here
```
~/.config/zsh/

├── 00-environment.zsh
├── 10-aliases.zsh
├── 20-functions.zsh
├── 30-git.zsh
├── 40-docker.zsh
├── 50-python.zsh
├── 60-node.zsh
├── 70-completion.zsh
├── 80-prompt.zsh
└── 99-local.zsh
```

Why the numbers?

Because they load in order.

```
00
↓

10
↓

20
↓

30
↓

...

99
```
Giving you predictable initialization

## Phase 17 -- Bootstrap Files

Your `.zshrc` becomes tiny
```zsh
export XDG_CONFIG_HOME="$HOME/.config"

for file in "$XDG_CONFIG_HOME"/zsh/*.zsh; do
    source "$file"
done
```
and your `.gitconfig` can become a bootstrap:
```ini
[include]
    path = ~/.config/git/config
```

## Before installing anything -- Recommended to keep entire WSL in Git

```
dotfiles/

├── README.md
├── bootstrap.sh
├── .config/
│   ├── git/
│   ├── starship/
│   ├── zsh/
│   └── ...
├── .zshrc
└── .gitconfig
```
This allows you to clone your profile to your next environment


## Your next task:

Before installing any tools, create this folder structure only:
```
~
├── Projects/
├── Containers/
├── Scripts/
└── .config/
```

## Phase 18 -- Install Zsh

First verify
```zsh
zsh --version
```
if you get
    `zsh 5.x.x`
you're good

If not:
```bash
sudo apt update && sudo apt install zsh
```

## Phase 19 -- Make Zsh Default shell

Check currrent shell
```bash
echo $SHELL
```

If it says
`/bin/bash`

change it
```bash
chsh -s $(which zsh)
```

Then Close & Open Windows Terminal

```bash
chsh -s $(which zsh)
```

You should now see
`/usr/bin/zsh`


## Phase 20 -- Install Starship

Install:
```bash
curl -sS https://starship.rs/install.sh | sh
```

Verify:
```bash
starship --version
```

## Phase 21 -- Build your config tree

Create directories:
```bash
mkdir -p ~/.config/zsh
mkdir -p ~/.config/starship
mkdir -p ~/.config/git
```

Verity:
```bash
tree ~/.config
```
Should see something like:
```zsh
~/.config
├── git
├── starship
└── zsh
```


## Phase 22 -- Create Zsh Modules

Create empty files:
```bash
touch ~/.config/zsh/00-environment.zsh
touch ~/.config/zsh/10-aliases.zsh
touch ~/.config/zsh/20-functions.zsh
touch ~/.config/zsh/30-git.zsh
touch ~/.config/zsh/40-docker.zsh
touch ~/.config/zsh/50-python.zsh
touch ~/.config/zsh/60-node.zsh
touch ~/.config/zsh/70-completion.zsh
touch ~/.config/zsh/80-prompt.zsh
touch ~/.config/zsh/99-local.zsh
```
Files load numerically, giving you predictability for start-up


## Phase 23 -- Create a minimal `.zshrc`

Your `.zshrc` should have minimal code, mainly bootstrap
```zsh
export XDG_CONFIG_HOME="$HOME/.config"

for file in "$XDG_CONFIG_HOME"/zsh/*.zsh; do
    source "$file"
done
```

## Phase 24 -- Configure Starship

Create:
```
~/.config/starship/starship.toml
```

Keep it simple: we will return to engineer the prompt
```
add_newline = false
```

## Phase 25 -- Wire Starship into Zsh

Don't use `.zshrc`, but instead use:
```
~/.config/zsh/80-prompt.zsh
```

Contents:
```zsh
eval "$(starship init zsh)"
```
Now the prompt configuration is isolated from everything else


## Phase 26 -- Test

Close & Open WSL

Check:
```bash
echo $ZSH_VERSION
```

Then:
```bash
starship explain
```
shows exactly how your prompt is assembled and is very useful when customizing it.


