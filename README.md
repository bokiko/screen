# Screen Cheat Sheet for Ubuntu

A quick reference guide for using GNU Screen on Ubuntu systems.

> **Note:** This is my preferred terminal multiplexer for running persistent sessions on servers.

## Installation

```bash
sudo apt update
sudo apt install screen
```

## Basic Commands

| Command | Description |
|---------|-------------|
| `screen` | Start a new screen session |
| `screen -S name` | Start a new named session |
| `screen -ls` | List all sessions |
| `screen -r` | Reattach to last session |
| `screen -r name` | Reattach to specific session |
| `screen -d -r name` | Detach elsewhere and reattach here |
| `screen -X -S name quit` | Kill a specific session |

## Key Bindings (prefix is Ctrl+a)

### Session Management

| Shortcut | Description |
|----------|-------------|
| `Ctrl+a d` | Detach from session |
| `Ctrl+a A` | Rename current window |
| `Ctrl+a "` | List windows for selection |
| `Ctrl+a k` | Kill current window |

### Window Management

| Shortcut | Description |
|----------|-------------|
| `Ctrl+a c` | Create new window |
| `Ctrl+a n` | Next window |
| `Ctrl+a p` | Previous window |
| `Ctrl+a 0-9` | Switch to window by number |

### Split Screen

| Shortcut | Description |
|----------|-------------|
| `Ctrl+a S` | Split horizontally |
| `Ctrl+a |` | Split vertically |
| `Ctrl+a Tab` | Switch between splits |
| `Ctrl+a X` | Close current split |
| `Ctrl+a Q` | Close all splits except current |

### Scrollback / Copy Mode

| Shortcut | Description |
|----------|-------------|
| `Ctrl+a [` | Enter copy/scrollback mode |
| `Ctrl+a ]` | Paste |
| `Space` | Start selection (in copy mode) |
| `Enter` | Copy selection (in copy mode) |
| `Esc` | Exit copy mode |

## Common Configuration

Create `~/.screenrc`:

```bash
# Enable scrollback buffer (10000 lines)
defscrollback 10000

# Disable startup message
startup_message off

# Show status bar
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{B} %m-%d %{W}%c %{g}]'

# Auto-detach on hangup
autodetach on

# UTF-8 support
defutf8 on
```

## Auto-start Screen on SSH Login

Add to `~/.bashrc`:

```bash
# Auto-start screen on SSH login
if [[ -n "$SSH_CONNECTION" ]] && [[ -z "$STY" ]]; then
    screen -xRR ssh_session
fi
```

## Auto-start Application in Screen

```bash
#!/bin/bash
# Save as ~/start_app.sh and make executable with: chmod +x ~/start_app.sh

# Start a detached named session running a command
screen -dmS myapp bash -c 'cd /path/to/app && ./start_script.sh'

# To run at boot, add to crontab with: crontab -e
# @reboot /home/username/start_app.sh
```

## Running Node Applications

```bash
# Start a node in a detached screen session
screen -dmS my-node ./start-node.sh

# Check if it's running
screen -ls

# Reattach to monitor
screen -r my-node

# Detach again: Ctrl+a d
```

## Quick Comparison: Screen vs Tmux

| Feature | Screen | Tmux |
|---------|--------|------|
| Prefix key | `Ctrl+a` | `Ctrl+b` |
| Detach | `Ctrl+a d` | `Ctrl+b d` |
| Simpler config | ✅ | |
| More features | | ✅ |

I prefer **screen** for its simplicity on server nodes.

---

For more detailed information, see `man screen`.
