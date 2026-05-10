# OlympSSH Commander

**SSH server monitoring, Docker management, terminal access, command templates, and alerts in one native app.**

OlympSSH Commander is a desktop and mobile server administration app for Linux servers reachable through SSH. It helps operators, developers, homelab users, and small teams monitor server health, inspect Docker workloads, run recurring commands, and respond to problems without opening multiple separate tools.

Website: https://olympstack.com  
Contact: contact@olympstack.com  
Support: support@olympstack.com

![OlympSSH Commander Servers](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serversTabDarkMode.png?raw=true)

## Why OlympSSH Commander

Managing Linux servers usually means switching between SSH terminals, Docker commands, monitoring dashboards, shell snippets, and notes. OlympSSH Commander brings those daily workflows into one focused interface:

- Monitor CPU, memory, swap, disk, network, load average, uptime, and per-core CPU activity.
- Manage Docker containers with live stats, logs, inspect views, and guarded container actions.
- Open interactive SSH terminals with tab support, command history, copy/paste, and snippet execution.
- Store reusable commands and use built-in Linux and Docker command templates.
- Create threshold-based alerts for server and container conditions.
- Keep server credentials in OS-backed secure storage.
- Use light mode, dark mode, keyboard shortcuts, import/export, diagnostics, and metrics export.

## Product Screenshots

### Server Overview

Add and manage SSH server profiles, choose password or private-key authentication, assign tags, and optionally connect through a jump host.

![Servers](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serversTabDarkMode.png?raw=true)

![Add Server](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serversTabAddServer.png?raw=true)

### Real-Time Linux Monitoring

The Status view shows live Linux metrics collected over SSH, including CPU breakdown, RAM, load average, disk usage, disk I/O, network throughput, packet counters, and uptime.

![Server Status](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serverStatus.png?raw=true)

![Multi-Core CPU Status](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serverStatusMultiCores.png?raw=true)

### Docker Container Management

Inspect Docker containers, review resource usage, open logs, view detailed stats, and execute guarded actions such as start, stop, restart, and remove.

![Docker Containers](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerTab.png?raw=true)

![Docker Logs](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerViewLogs.png?raw=true)

![Docker Container Options](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerTabOptions.png?raw=true)

### Command Snippets And Templates

Use your own snippets or built-in command libraries. The Docker templates support live parameter rendering for containers, images, volumes, networks, compose files, follow flags, and tail limits.

![Custom Snippets](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/customSnippets.png?raw=true)

![Docker Command Templates](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerSnippets.png?raw=true)

![Linux Command Templates](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/linuxSnippets.png?raw=true)

### Alerts, Settings, Shortcuts

Create alert rules for CPU, memory, disk, load average, and Docker state. Tune appearance, monitoring, safety, keychain, export/import, metrics export, diagnostics, support, and keyboard shortcuts from Settings.

![Alert Rules](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/alertsRules.png?raw=true)

![Settings](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/settingsTab.png?raw=true)

![Keyboard Shortcuts](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/settingsShortcuts.png?raw=true)

## Core Features

### SSH Server Management

- Add, edit, delete, and organize server profiles.
- Password and private-key SSH authentication.
- Optional SSH keychain for imported or generated keys.
- Server tags for organization.
- Jump host support through a saved jump host or manual jump host configuration.
- Known-host fingerprint verification to reduce man-in-the-middle risk.
- Last-connected timestamps and active server selection.

### Live Server Monitoring

- CPU usage with user, system, I/O wait, steal, idle, and per-core display.
- Memory and swap usage.
- Disk capacity, read/write rates, and IOPS.
- Network throughput, totals, packet counters, and interface addresses.
- Load average, running processes, total processes, and uptime.
- Fast polling for CPU, memory, and network metrics.
- Slower polling for disk metrics to reduce overhead.
- Offline metrics cache for last-known snapshots when a server is unavailable.

### Docker Operations

- List running and stopped containers.
- View container memory, network, block I/O, and CPU usage.
- Open container logs.
- Inspect container metadata with formatted output.
- View Docker disk usage.
- Start guided Docker installation commands over SSH when Docker is missing.
- Start, stop, restart, and remove containers with confirmations.
- Built-in Docker command templates for containers, images, volumes, networks, system commands, and Docker Compose.

### Terminal Pro

- Interactive SSH terminal with xterm emulation.
- Multiple terminal tabs per server in Pro.
- Per-tab command history.
- Snippet and command palette integration.
- Desktop copy/paste shortcuts.
- Reopen handling for lost terminal sessions.
- Resize and terminal color support.

### Commands And Snippets

- Save custom commands with names, descriptions, and tags.
- Execute snippets on selected servers.
- Use read-only Linux command templates.
- Use parameterized Docker templates.
- Insert interactive commands into the terminal when a PTY is required.
- Confirm warning and danger commands before execution.

### Alerts And Monitoring Rules

- Create threshold rules for CPU, memory, disk, load average, and container state.
- Configure duration and cooldown to avoid noisy alerts.
- Enable or disable rules.
- Track active alerts and alert history.
- Optional background alert monitoring.
- Configurable alert history limit.

### Export, Import, Diagnostics, And Metrics

- Export and import app configuration.
- Credentials are excluded from configuration exports.
- Export metrics as CSV or JSON.
- Export diagnostics and logs for support.
- Clear known SSH fingerprints when a server is intentionally rebuilt or rotated.

## Security Model

OlympSSH Commander is designed for administration tasks, so credential handling and risky actions matter.

- SSH passwords, private keys, and passphrases are stored with `flutter_secure_storage`, which uses the platform's secure storage facilities.
- Server profile JSON stores connection metadata such as name, host, port, username, tags, and known-host fingerprint, but not the password or private key.
- Credentials are stored per server ID, so deleting a server also removes that server's stored credentials.
- Keychain private keys and passphrases are stored separately from key metadata.
- Export/import intentionally excludes server credentials.
- SSH host fingerprints are verified and can be cleared from Settings when needed.
- Destructive Docker and command-template actions are gated by confirmations.

Illustrative credential flow:

```dart
// Server metadata is persisted without the secret value.
profile.toJson(); // name, host, port, username, auth type, tags, fingerprint

// Secrets are written separately to OS-backed secure storage.
secureCredentials.savePassword(serverId, password);
secureCredentials.savePrivateKey(serverId, privateKeyPem);
secureCredentials.savePassphrase(serverId, passphrase);
```

Never store production secrets in screenshots, GitHub issues, exported diagnostics, or public support messages.

## Free And Pro

OlympSSH Commander can run in Free mode or Pro mode.

| Capability | Free | Pro Lifetime |
| --- | --- | --- |
| Servers | 1 server | Unlimited servers |
| Status monitoring | Included | Included |
| Docker read/log access | Included | Included |
| Docker actions | Limited | Full guarded actions |
| Terminal tabs | 1 tab | Multiple tabs |
| Snippets and command templates | Limited | Full access |
| Alerts | Limited | Full access |
| Offline Pro use after activation | Not applicable | Supported with locally stored signed license |

Activation is available in `Settings > Activation`. After activation, Pro can continue working offline with the locally stored signed license.

## Installation

Download the latest build from the GitHub Releases page:

https://github.com/OlympProject/olympssh-commander-release/releases

The release repository contains binaries and documentation for end users. It does not grant source-code rights.

## Requirements

- A Linux server reachable through SSH.
- SSH username plus password or private key.
- Docker installed on the server for Docker features.
- Docker permissions for the SSH user when using Docker commands.
- Network access from your device to the target server.

For Docker without `sudo`, the remote user usually needs to be in the `docker` group. For production systems, review the security implications before granting Docker access.

## Quick Start

1. Install OlympSSH Commander from the latest release.
2. Open the app and go to `Servers`.
3. Select `Add Server`.
4. Enter name, host, port, username, authentication method, and optional tags.
5. Save the server.
6. On first connection, verify and accept the SSH fingerprint.
7. Open `Status` for live metrics.
8. Open `Docker` to inspect containers.
9. Open `Terminal` for direct SSH commands.
10. Open `Snippets` to run saved commands or built-in templates.

For a guided workflow, see [USERMANUAL.md](https://github.com/OlympProject/olympssh-commander-release/blob/main/USERMANUAL.md).

## Keyboard Shortcuts

| Shortcut | Action |
| --- | --- |
| `Ctrl + 1` | Open Servers tab |
| `Ctrl + 2` | Open Status tab |
| `Ctrl + 3` | Open Docker tab |
| `Ctrl + 4` | Open Terminal tab |
| `Ctrl + 5` | Open Snippets tab |
| `Ctrl + 6` | Open Alerts tab |
| `Ctrl + 7` | Open Settings tab |
| `Tab` | Switch to the next main tab |
| `Ctrl + S` | Open Snippets/Commands palette in Terminal |
| `Ctrl + H` | Open command history |
| `Ctrl + T` | Open a new terminal tab |
| `Ctrl + Shift + T` | Close active terminal tab |
| `Ctrl + Shift + C` | Copy selected terminal text |
| `Ctrl + Shift + V` | Paste clipboard into terminal |
| `Ctrl + R` | Refresh Status or Docker |
| `Ctrl + M` | Open Offline Metrics |

## Support

For product questions, licensing, and support:

- Website: https://olympstack.com
- Contact: contact@olympstack.com
- Support: support@olympstack.com

When reporting an issue, include the app version, operating system, target server type, and a description of the workflow. Do not include passwords, private keys, activation tokens, or other secrets.

## License

OlympSSH Commander is proprietary software. This repository contains binary releases and related documentation only.

Use of the software is governed by the [OlympSSH Commander EULA](https://github.com/OlympProject/olympssh-commander-release/blob/main/EULA.md).

Copyright (c) 2026 OlympStack. All rights reserved.
