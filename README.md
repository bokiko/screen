<div align="center">

# Screen Cheat Sheet

<h3>Quick reference for GNU Screen terminal multiplexer on Ubuntu.</h3>

<p>
  <img src="https://img.shields.io/badge/Platform-Ubuntu-E95420" alt="Ubuntu" />
  <img src="https://img.shields.io/badge/Tool-GNU%20Screen-green" alt="GNU Screen" />
  <img src="https://img.shields.io/badge/Type-Cheat%20Sheet-blue" alt="Cheat Sheet" />
</p>

</div>

---

## What is Screen?

**GNU Screen** is a terminal multiplexer that lets you run multiple terminal sessions inside a single window. My preferred tool for running persistent sessions on servers.

**Simple. Reliable. Lightweight.**

---

## Installation

```bash
sudo apt update && sudo apt install screen
```

---

## Quick Reference

### Basic Commands

| Command | Description |
|---------|-------------|
| `screen` | Start a new session |
| `screen -S name` | Start a new named session |
| `screen -ls` | List all sessions |
| `screen -r` | Reattach to last session |
| `screen -r name` | Reattach to specific session |
| `screen -d -r name` | Detach elsewhere and reattach here |
| `screen -X -S name quit` | Kill a specific session |

### Key Bindings (prefix: `Ctrl+a`)

#### Session Management
| Shortcut | Description |
|----------|-------------|
| `Ctrl+a d` | Detach from session |
| `Ctrl+a A` | Rename current window |
| `Ctrl+a "` | List windows for selection |
| `Ctrl+a k` | Kill current window |

#### Window Management
| Shortcut | Description |
|----------|-------------|
| `Ctrl+a c` | Create new window |
| `Ctrl+a n` | Next window |
| `Ctrl+a p` | Previous window |
| `Ctrl+a 0-9` | Switch to window by number |

#### Split Screen
| Shortcut | Description |
|----------|-------------|
| `Ctrl+a S` | Split horizontally |
| `Ctrl+a \|` | Split vertically |
| `Ctrl+a Tab` | Switch between splits |
| `Ctrl+a X` | Close current split |
| `Ctrl+a Q` | Close all splits except current |

#### Scrollback / Copy Mode
| Shortcut | Description |
|----------|-------------|
| `Ctrl+a [` | Enter copy/scrollback mode |
| `Ctrl+a ]` | Paste |
| `Space` | Start selection (in copy mode) |
| `Enter` | Copy selection (in copy mode) |
| `Esc` | Exit copy mode |

---

## Configuration

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

---

## Auto-Start on SSH Login

Add to `~/.bashrc`:

```bash
if [[ -n "$SSH_CONNECTION" ]] && [[ -z "$STY" ]]; then
    screen -xRR ssh_session
fi
```

---

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

---

## Screen vs Tmux

| Feature | Screen | Tmux |
|---------|:------:|:----:|
| Prefix key | `Ctrl+a` | `Ctrl+b` |
| Simpler config | Yes | No |
| More features | No | Yes |
| My preference | Yes | - |

I prefer **screen** for its simplicity on server nodes.

---

## More Information

Official docs: `man screen`

---

<div align="center">

Built by [@bokiko](https://github.com/bokiko)

</div>
