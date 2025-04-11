```markdown
# SafeRM - Protective Wrapper for `rm` Command

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A safety-enhanced replacement for the `rm` command that prevents accidental recursive deletion of root directory (`/`) or its immediate subdirectories.

## Features

- 🛡️ **Critical Path Protection**  
  Blocks recursive deletion of:
  - Root directory (`/`)
  - Any first-level subdirectories under root (e.g., `/etc`, `/home`)
  - Equivalent paths using relative/alternative notations

- 🔍 **Smart Argument Parsing**  
  Recognizes all common recursive flags:
  - `-r`, `-R`, `--recursive`
  - Mixed options like `-rf` or `-fr`

- 🚦 **Transparent Operation**  
  - Non-recursive deletions work normally
  - Seamless passthrough to native `rm` for safe operations

## Installation

1. Add to your `.bashrc` or `.zshrc`:
```bash
# SafeRM configuration
saferm() {
    [function body from provided code]
}
alias rm='saferm'
```

2. Reload shell configuration:
```bash
source ~/.bashrc  # or source ~/.zshrc
```

## Usage Examples

### Blocked Operations
```bash
rm -rf /                  # Block root deletion
rm -r /var ../usr         # Block first-level directories
rm -R "$PWD"              # Block if current dir is under /
```

### Allowed Operations
```bash
rm file.txt               # Regular file deletion
rm -r ~/downloads         # Safe recursive deletion
rm -f *.log               # Force-delete files
```

## Requirements

- `realpath` utility (usually preinstalled on Linux systems)
- Bash 5.x+ or Zsh 5.8+ (tested environments)

## Notes

- ⚠️ **Not a Full Protection Solution**  
  This is designed as a last-line defense against catastrophic mistakes. Maintain proper backups and consider additional safeguards like:
  - `--preserve-root` in GNU rm
  - Filesystem snapshots
  - Privilege separation

- For systems without `realpath`, replace with `readlink -f` (may require existing paths)