# cc-account

Switch between multiple Claude Code subscription accounts.

Claude Code stores OAuth credentials in `~/.claude/.credentials.json`. This script manages named profiles by copying credential files in and out.

## Install

```bash
cp cc-account ~/.local/bin/
chmod +x ~/.local/bin/cc-account
```

Requires `jq`.

## Usage

```bash
# Save current credentials as a named profile
cc-account save max20x

# Login to another account, then save it
claude logout && claude login
cc-account save max5x

# Switch between profiles
cc-account use max20x
cc-account use max5x

# List all saved profiles (shows tier + expiry)
cc-account list
#   max5x        max_5x   (expires 2026-04-06)
#   max20x       max_20x  (expires 2026-04-05)

# Show current account details
cc-account current

# Remove a profile
cc-account rm old-account
```

Restart your Claude Code session after switching for the new credentials to take effect.

## How it works

Profiles are stored as JSON files in `~/.claude/profiles/`. Switching simply copies the selected profile over `~/.claude/.credentials.json`.

## License

MIT
