# WSL -- ZSH Shell tools & keys configuration

Current Workstation Status

| Component        | Status |
| ---------------- | :----: |
| Ubuntu WSL       |    ✅   |
| Zsh              |    ✅   |
| Starship         |    ✅   |
| Docker CLI       |    ✅   |
| Docker Compose   |    ✅   |
| GitHub CLI       |    ✅   |
| uv               |    ✅   |
| Git              |    ✅   |
| Modular Zsh      |    ✅   |
| `.config` layout |    ✅   |


## Step 1 -- Finish Zsh

For now, leave the modular files in place, but don't obsess over moving every last setting. We can migrate the remaining completion styles later.

Your goal is simply:

Zsh starts correctly.
    - zsh --version
    - which zsh
    - ps aux | grep zsh
Starship loads.
    - starship explain
Your history works.
    - echo $HISTFILE
Tab completion works.
    - print - `tab`
If all four are true, move on.
    - All 4 = Correct


## Step 2 -- Install the core tools

Run:
```bash
sudo apt update

sudo apt install \
git \
curl \
wget \
tree \
htop \
btop \
tmux \
fzf \
ripgrep \
fd-find \
bat \
eza \
zoxide \
unzip \
zip
```
These are the tools you'll use constantly


## Step 3 -- Install GitHub CLI

```bash
type -p curl >/dev/null || sudo apt install curl -y

curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg \
| sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg

sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" \
| sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

sudo apt update

sudo apt install gh
```

Then
```bash
gh auth login
```

## Step 4 -- Install modern Python

I recommend ***uv***
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Then
```bash
uv --version
```


## Step 5 -- Install Node

Use nvm
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Restart Zsh

Then:
```bash
nvm install --lts
```


## Step 6 -- Install Docker CLI

Since you're already using Docker Desktop on Windows, inside WSL just verify:
```bash
docker version # Server & Client full-info
docker --version # Docker Ver; build #
docker compose version # Docker compose Ver
```


## Step 7 -- Verify everything

Run:
```bash
git --version

gh --version

docker --version

docker compose version

python3 --version

uv --version

node --version

npm --version

zsh --version

starship --version
```
Everything should report a version



## Step 8 -- Build your Starship prompt

Ideal workflow:
    - Docker
    - Python virtual environments
    - Git
    - WSL
    - Node
    - Kubernetes (later)
    - AI projects


## Step 9 -- Build aliases

Again, later.

We already have the structure. Once you're using the workstation daily, you'll naturally discover the commands you repeat, and those are the ones worth turning into aliases.

Here's what I want you to do right now

Let's finish the installation phase before we customize.

Run these four commands and tell me the output if anything fails:
```bash
docker version
docker compose version
gh --version
uv --version
```



