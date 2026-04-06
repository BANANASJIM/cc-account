# cc-account

Lightweight, secure Claude Code account switcher.

A single zsh script that manages named credential profiles — no dependencies beyond `jq`.

## Install

```bash
cp cc-account ~/.local/bin/
chmod +x ~/.local/bin/cc-account
```

## Usage

```bash
cc-account save <name>      # save current credentials as a profile
cc-account use <name>       # switch to a profile (atomic write)
cc-account list             # list profiles with tier + expiry
cc-account current          # show active account details
cc-account rm <name>        # remove a profile
```

Example workflow:

```bash
cc-account save max20x            # save current account
claude logout && claude login     # login to another account
cc-account save max5x             # save it too

cc-account use max20x             # switch anytime
# Switched to: max20x (max_20x)
#   ↳ restart CC session to apply
```

## Security

- Profile names validated against `[a-zA-Z0-9_-]` to prevent path traversal
- Credential switch uses atomic `mktemp` + `mv` to prevent corruption on interruption
- Profiles stored with original file permissions in `~/.claude/profiles/`

## License

MIT
