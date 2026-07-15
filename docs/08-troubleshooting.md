# Troubleshooting

This document collects common issues encountered while configuring the development environment and their corresponding solutions.

---

# GitHub CLI cannot open the browser

## Problem

Opening a repository from GitHub CLI fails.

```bash
gh repo view --web
```

Error:

```text
exec: "xdg-open,x-www-browser,www-browser,wslview": executable file not found in $PATH
```

## Cause

GitHub CLI attempts to launch the default browser using Linux utilities such as:

- xdg-open
- x-www-browser
- www-browser
- wslview

These utilities are not installed by default in CentOS Stream running under WSL.

## Solution

Create a lightweight `xdg-open` wrapper that delegates the request to Windows Explorer.

```bash
sudo tee /usr/local/bin/xdg-open >/dev/null <<'EOF'
#!/bin/bash
explorer.exe "$@"
EOF

sudo chmod +x /usr/local/bin/xdg-open
```

Verify the wrapper.

```bash
xdg-open https://github.com
```

Then verify GitHub CLI.

```bash
gh repo view --web
```

The default browser should open the repository page.

---

# VS Code launches the Linux version instead of Windows

## Problem

Running:

```bash
code .
```

opens the Linux installation of Visual Studio Code or displays an error similar to:

```text
To use Visual Studio Code with the Windows Subsystem for Linux...
```

## Cause

A Linux version of VS Code is installed and appears before the Windows launcher in the system PATH.

## Solution

Remove the Linux package.

```bash
sudo dnf remove code
```

Clear Bash command cache.

```bash
hash -r
```

Verify the executable.

```bash
which code
```

Expected output:

```text
/mnt/c/Users/<username>/AppData/Local/Programs/Microsoft VS Code/bin/code
```

Verify.

```bash
code .
```

Visual Studio Code should open using the Windows installation and automatically connect to WSL.

---

# GitHub CLI completion is not working

## Problem

GitHub CLI completion does not work.

Example:

```bash
gh repo <TAB>
```

or

```text
bash: _get_comp_words_by_ref: command not found
```

## Cause

Bash Completion is not loaded.

## Solution

Install Bash Completion.

```bash
sudo dnf install -y bash-completion
```

Load Bash Completion from `~/.bashrc`.

```bash
if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
fi
```

Enable GitHub CLI completion.

```bash
eval "$(gh completion -s bash)"
```

Reload Bash.

```bash
source ~/.bashrc
```

Verify.

```bash
type _get_comp_words_by_ref
```

Expected output:

```text
_get_comp_words_by_ref is a function
```

---

# Git Prompt is not displayed

## Problem

The current Git branch does not appear in the shell prompt.

## Cause

The Git Prompt script is not loaded.

## Solution

Load the Git Prompt script.

```bash
if [ -f /usr/share/git-core/contrib/completion/git-prompt.sh ]; then
    source /usr/share/git-core/contrib/completion/git-prompt.sh
fi
```

Reload Bash.

```bash
source ~/.bashrc
```

Verify.

```bash
git status
```

Expected prompt:

```text
root@hostname:~/projects/linux-dev-setup [main =]#
```

---

# VS Code Server installation

## Problem

The first execution of:

```bash
code .
```

downloads Visual Studio Code Server.

Example:

```text
Installing VS Code Server...
Downloading...
```

## Cause

This is the expected behaviour when connecting to a WSL distribution for the first time.

## Solution

No action is required.

Wait until the installation completes.

Subsequent executions of `code .` will reuse the installed server.

---

# Best Practices

- Document every issue immediately after solving it.
- Prefer official tools over third-party workarounds.
- Test every fix before documenting it.
- Keep this document updated as the environment evolves.

---

# References

- https://cli.github.com/
- https://code.visualstudio.com/docs/remote/wsl
- https://www.gnu.org/software/bash/

---

## Last Tested

- Windows 11
- WSL2
- CentOS Stream 9
- GitHub CLI 2.96.0
- Visual Studio Code 1.127

---

## Last Updated

2026-07-16