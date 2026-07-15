# Git

## Purpose
Install and configure Git.

## Installation
```bash
sudo dnf install -y git
```

## Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global color.ui auto
git config --global fetch.prune true
git config --global push.autoSetupRemote true
git config --global rerere.enabled true
git config --global core.editor "code --wait"
```

## Verification
```bash
git --version
git config --global --list
```

## Useful Commands
```bash
git status
git add .
git commit -m "message"
git push
git pull
```

## Best Practices
- Small commits
- Feature branches
- Meaningful commit messages

## References
https://git-scm.com/

## Last Tested
Git 2.43.x

## Last Updated
2026-07-15
