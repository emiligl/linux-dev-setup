# Troubleshooting

## VS Code opens Linux version

Remove Linux package:

```bash
sudo dnf remove code
hash -r
```

## GitHub CLI completion fails

Verify:

```bash
type _get_comp_words_by_ref
```

## Prompt not updated

```bash
source ~/.bashrc
```

## References
https://code.visualstudio.com/docs/remote/troubleshooting

## Last Updated
2026-07-15
