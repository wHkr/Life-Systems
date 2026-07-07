# Environment Descriptions

Explination of folders, files, software, etc... that you find in your environment.

## Folder PATH

~/.config/git/
├── config - Replaces a huge `.gitconfig`
       - user name, aliases, editor, merge settings
├── ignore - Global ignores
        - .DS_Store, Thumbs.db, *.swp, .vscode/
└── attributes
        - Line endings, Diff behavior, Bin file handling


~/.ssh/
├── config - Configuration file
        - No extension
├── known_hosts - Auto maintained
        - Don't edit
├── id_ed25519 - PRIVATE key
        - Never commit it
├── id_ed25519.pub - Public key
        - Safe to share
└── authorized_keys