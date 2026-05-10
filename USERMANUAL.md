# OlympSSH Commander User Manual

This manual explains the main workflows in OlympSSH Commander: adding servers, monitoring Linux metrics, managing Docker, using terminal sessions, running snippets, configuring alerts, and handling settings.

Website: https://olympstack.com  
Support: support@olympstack.com

## 1. First Start

After launching OlympSSH Commander, the main navigation appears at the bottom:

- `Servers`
- `Status`
- `Docker`
- `Terminal`
- `Snippets`
- `Alerts`
- `Settings`

![Servers Tab](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serversTabDarkMode.png?raw=true)

Use `Servers` first. Most other screens require an active server.

## 2. Add A Server

Open `Servers`, then select the `+` button.

![Add Server](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serversTabAddServer.png?raw=true)

Fill in:

| Field | Description |
| --- | --- |
| Type | `Server` for a normal target or `Jumphost` for a bastion server |
| Server Name | Friendly display name |
| Host | IP address or DNS name |
| Port | SSH port, usually `22` |
| Username | Remote SSH user |
| Tags | Optional comma-separated labels |
| Authentication | `Password` or `Private Key` |
| Connect via Jump Host | Optional saved or manual jump host route |

For password authentication, enter the SSH password.

For private-key authentication, either select a key from the Keychain or paste a private key manually. If the key is encrypted, enter the passphrase.

### First SSH Fingerprint

On the first connection, the app may ask you to accept the server's SSH fingerprint. Verify it against the server before accepting. On many Linux servers you can compare with:

```bash
ssh-keygen -lf /etc/ssh/ssh_host_ed25519_key.pub
```

If a fingerprint changes unexpectedly, do not accept it until you know why it changed.

## 3. Manage Servers

The `Servers` screen lists configured servers with authentication type and last connection time.

![Servers Light Mode](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serversTabLightMode.png?raw=true)

Common actions:

| Action | How |
| --- | --- |
| Select server | Click a server card |
| Edit server | Open the server menu and choose `Edit` |
| Delete server | Open the server menu and choose `Delete` |
| Refresh list | Use the refresh icon |
| Open overview grid | Use the grid icon |

Deleting a server removes its related stored credentials.

## 4. Monitor Server Status

Select a server, then open `Status`.

![Server Status](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serverStatus.png?raw=true)

The Status screen shows:

- CPU usage with user, system, I/O wait, steal, idle, and per-core rows.
- Memory and swap usage.
- Load average for 1, 5, and 15 minutes.
- Disk usage, read/write throughput, and IOPS.
- Network throughput, totals, packets, and interface information.
- Uptime.

Controls:

| Control | Purpose |
| --- | --- |
| Pause / Play | Stop or resume monitoring |
| Refresh | Reconnect and refresh metrics |
| More menu | Open Offline Metrics |
| Pull to refresh | Reconnect and reload the status view |

![Multi-Core Status](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/serverStatusMultiCores.png?raw=true)

### Offline Metrics

Open the menu on the Status screen and choose `Offline Metrics` to view cached last-known snapshots when the server is unavailable.

## 5. Manage Docker Containers

Select a server with Docker installed, then open `Docker`.

![Docker Containers](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerTab.png?raw=true)

The Docker screen shows container name, image, memory, network usage, block I/O, and CPU usage.

Available container actions can include:

- View logs.
- View stats.
- Inspect container.
- Start stopped container.
- Stop running container.
- Restart container.
- Remove container.

![Docker Container Options](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerTabOptions.png?raw=true)

Actions that can interrupt or delete workloads require confirmation.

### View Docker Logs

Open a container menu and choose `View Logs`.

![Docker Logs](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerViewLogs.png?raw=true)

Use logs to inspect service output, health checks, application errors, and container startup behavior.

### Docker Stats And Installation

OlympSSH Commander can show live container stats. If Docker is missing on a supported Linux distribution, the Docker screen can also run a guided installation workflow over SSH.

![Docker Stats](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerContainerTabContainerStats.png?raw=true)

![Docker Installation](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerInstallationStart.png?raw=true)

![Docker Installation Completed](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerInstallationEnd.png?raw=true)

## 6. Use Terminal

Open `Terminal` after selecting a server.

Terminal features:

- Interactive SSH shell.
- Multiple terminal tabs in Pro.
- Command history.
- Full terminal color support.
- Resize support.
- Snippets/Commands palette.
- Desktop copy and paste shortcuts.

Useful shortcuts:

| Shortcut | Action |
| --- | --- |
| `Ctrl + S` | Open Snippets/Commands palette |
| `Esc` | Close palette or history |
| `Ctrl + H` | Open command history |
| `Ctrl + T` | Open a new terminal tab |
| `Ctrl + Shift + T` | Close active terminal tab |
| `Ctrl + Shift + C` | Copy selected terminal text |
| `Ctrl + Shift + V` | Paste clipboard into terminal |

Interactive commands, such as `docker exec -it`, should be inserted into Terminal rather than run through a non-interactive command runner.

## 7. Use Snippets And Command Templates

Open `Snippets`.

![Custom Snippets](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/customSnippets.png?raw=true)

The Commands screen contains three sections:

| Section | Purpose |
| --- | --- |
| My Snippets | Your editable local commands |
| OlympSSH | Built-in Linux command templates |
| Docker | Built-in Docker and Docker Compose templates |

### Create A Custom Snippet

Select the `+` button and enter a name, command, description, and optional tags.

![Add Snippet](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/customSnippetsAdd.png?raw=true)

![Filled Snippet](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/customSnippetsAddFilled.png?raw=true)

### Use Linux Templates

Open the `OlympSSH` tab to browse built-in Linux commands.

![Linux Snippets](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/linuxSnippets.png?raw=true)

### Use Docker Templates

Open the `Docker` tab to search Docker commands by group.

![Docker Snippets](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/dockerSnippets.png?raw=true)

Docker templates can render parameters such as:

- Container
- Image
- Volume
- Network
- Compose file
- Environment file
- Follow logs
- Tail line count
- Force flags

Review generated commands before running them. Warning and danger commands require confirmation.

## 8. Configure Alerts

Open `Alerts`.

![Alert Rules](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/alertsRules.png?raw=true)

The Alerts screen has:

- `Active Alerts`
- `Rules`

Create a rule with the `+` button.

![Edit Alert Rule](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/alertsEditRule.png?raw=true)

Alert rule options include:

| Option | Description |
| --- | --- |
| Type | CPU, memory, disk, load average, or container state |
| Threshold | Value that must be exceeded |
| Duration | How long the condition must remain true |
| Cooldown | Minimum time before the next alert |
| Severity | Importance level |
| Enabled | Turns the rule on or off |

Use duration and cooldown values to avoid noisy alerts during short spikes.

## 9. Settings

Open `Settings` for app-wide configuration.

![Settings](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/settingsTab.png?raw=true)

Settings areas:

| Area | Purpose |
| --- | --- |
| Activation | View and activate the current plan |
| Appearance | Choose system, light, or dark mode |
| Monitoring & Notifications | Background monitoring and alert delivery |
| Safety & Security | Read-only mode, confirmations, and app lock settings |
| Clear SSH Fingerprints | Remove saved known-host fingerprints |
| Keychain | Manage SSH keys |
| Export / Import | Backup and restore configuration |
| Metrics Export | Export metrics as CSV or JSON |
| Diagnostics | System information and log export |
| Shortcuts | View keyboard shortcuts |
| Support | Share app, feedback, acknowledgements |

### Appearance

OlympSSH Commander supports system, light, and dark mode.

![Settings Light Mode](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/settingsTabLightMode.png?raw=true)

### Keyboard Shortcuts

The shortcut list is available in `Settings > Shortcuts`.

![Shortcuts](https://github.com/OlympProject/olympssh-commander-release/blob/main/screenshots/settingsShortcuts.png?raw=true)

## 10. Keychain And Credentials

Open `Settings > Keychain` to manage SSH keys.

Keychain supports:

- Import private key from clipboard.
- Import private key from file.
- Generate key pair.
- Copy public key.
- Export public key.
- Export private key after warning.
- Delete stored key.

Supported generated key types include ED25519 and RSA 2048.

Credential storage behavior:

- Passwords, private keys, and passphrases are written to OS-backed secure storage.
- Server metadata is stored separately from secrets.
- Configuration exports exclude credentials.
- Private-key export requires explicit confirmation because private keys are sensitive.

Illustrative storage flow:

```dart
secureCredentials.savePassword(serverId, password);
secureCredentials.savePrivateKey(serverId, privateKeyPem);
secureCredentials.savePassphrase(serverId, passphrase);
```

Do not share private keys, passwords, passphrases, activation tokens, exported diagnostics with secrets, or screenshots that reveal sensitive infrastructure details.

## 11. Export, Import, Metrics, And Diagnostics

Use `Settings > Export / Import` to back up or restore configuration.

Export can include:

- Server profiles without credentials.
- Snippets.
- Alert rules.

Imported servers require credentials to be entered again.

Use `Settings > Metrics Export` to export collected metrics as CSV or JSON.

Use `Settings > Diagnostics` when support needs technical context. Review exported diagnostics before sharing them publicly.

## 12. Free And Pro Limits

Free mode is intended for trying the app with a limited workflow:

- 1 server.
- Status access.
- Docker read/log access.
- 1 terminal tab.

Pro Lifetime unlocks:

- Unlimited servers.
- Docker actions.
- Multiple terminal tabs.
- Snippets and command templates.
- Alerts.

Activation is available in `Settings > Activation`. After activation, Pro can work offline from a locally stored signed license.

## 13. Troubleshooting

### Cannot Connect To Server

Check:

- Hostname or IP address is correct.
- SSH port is correct.
- Server is reachable from your network.
- Firewall allows SSH.
- Username and credentials are correct.
- Jump host configuration is correct if used.

### Fingerprint Warning

A changed fingerprint can mean:

- The server was rebuilt.
- SSH host keys were rotated.
- DNS or IP now points to another machine.
- A man-in-the-middle attack is possible.

Only accept a new fingerprint after verifying it.

### Docker Features Do Not Work

Check:

- Docker is installed on the server.
- Docker daemon is running.
- The SSH user has permission to use Docker.
- Commands work in a normal SSH shell.

### Terminal Stops Responding

Try:

- Open a new terminal tab.
- Reconnect from the Status screen.
- Check network stability.
- Verify the server accepts SSH sessions.

### Metrics Stop Updating

Try:

- Use refresh on the Status screen.
- Check whether monitoring is paused.
- Confirm the server is still connected.
- Check SSH session availability.

## 14. Support

For support, contact:

- support@olympstack.com
- contact@olympstack.com
- https://olympstack.com

Include app version, operating system, target server type, and the affected workflow. Do not send passwords, private keys, passphrases, license keys, activation tokens, or other secrets.

Copyright (c) 2026 OlympStack. All rights reserved.
