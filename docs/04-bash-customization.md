# Bash Customization

## Purpose
Improve shell productivity.

## Configuration
Enable bash-completion:

```bash
if [ -f /usr/share/bash-completion/bash_completion ]; then
  . /usr/share/bash-completion/bash_completion
fi
```

Enable Git prompt:

```bash
if [ -f /usr/share/git-core/contrib/completion/git-prompt.sh ]; then
  source /usr/share/git-core/contrib/completion/git-prompt.sh
fi

export GIT_PS1_SHOWDIRTYSTATE=1
export GIT_PS1_SHOWUNTRACKEDFILES=1
export GIT_PS1_SHOWUPSTREAM="auto"

PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[33m\]$(__git_ps1 " [%s]")\[\033[00m\]\$ '
```

GitHub CLI completion:

```bash
eval "$(gh completion -s bash)"
```

Reload:

```bash
source ~/.bashrc
```

## Verification
```bash
gh repo <TAB>
git status
```

## Best Practices
- Version your shell config
- Group aliases
- Keep prompt readable

## References
https://www.gnu.org/software/bash/

## Last Tested
Bash 5.1

## Last Updated
2026-07-15
