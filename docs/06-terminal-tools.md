# Terminal Tools

## Purpose
Install useful command-line utilities.

## Installation
```bash
sudo dnf install -y jq curl wget unzip zip
```

### Optional packages

Some utilities require additional repositories.

Example:

```bash
sudo dnf install epel-release
sudo dnf install htop
```

## Verification
```bash
jq --version
curl --version
wget --version
unzip -v
zip -v
htop --version
```

## Best Practices
Install only tools you use.

## References
https://jqlang.org/

## Last Updated
2026-07-15
