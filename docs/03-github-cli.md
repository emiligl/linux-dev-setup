# GitHub CLI

## Purpose
Install and configure GitHub CLI.

## Installation
```bash
sudo dnf config-manager --add-repo https://cli.github.com/packages/rpm/gh-cli.repo
sudo dnf install -y gh
```

## Configuration
```bash
gh auth login
gh config set git_protocol https
gh config set prompt enabled
```

## Verification
```bash
gh --version
gh auth status
```

## Useful Commands
```bash
gh repo create
gh repo list
gh repo view --web
gh pr list
gh issue list
```

## Best Practices
- Authenticate with browser
- Keep gh updated

## References
https://cli.github.com/

## Last Tested
GitHub CLI 2.96.0

## Last Updated
2026-07-15
