# Antigravity Unlocker — Use Antigravity Without a VPN or Google Account Region Change

A Windows and Linux utility intended to let Google accounts from different countries use Antigravity 2.0, Antigravity IDE, and Antigravity CLI. Setup is performed once per computer; afterward, you can sign in with different accounts. After an Antigravity update, the unlocker can reapply its patch.

**Video guide:** https://youtu.be/aybWT_7wtqA

## Installation

1. Download the latest release from [Releases](https://github.com/confeden/Antigravity/releases) and install Antigravity from the [official website](https://antigravity.google/download).
2. Run the unlocker **as Administrator** (right-click the executable). Without administrator privileges, only the client patch is installed; the service that addresses the “400 — User location is not supported” error is not installed.
3. Enter a free key available in the pinned messages in the [Telegram group](https://t.me/nova_txt/69864). Each unlocker version requires its own key, so you will need a new one after updating the unlocker.
4. Click **Enable All**. Antigravity will close briefly.
5. Start Antigravity, sign in, and send a message in the chat. The status card at the top of the window should turn green and show **“Working. Model responded …”**.

You can disable any switch to roll back that part of the configuration.

## With or Without a VPN

No additional VPN or DNS configuration is required. Connections from Antigravity to two Google servers are routed through a local service on your computer, so your VPN does not intercept those connections. The tool chooses a route based on which one actually receives a model response, not just which one is faster; routes that return errors are temporarily deprioritized.

## Terminal UI (TUI)

Use this mode on a server over SSH or if the graphical window does not open. The command downloads the latest version automatically.

On Linux/macOS-compatible shells:

```bash
curl -fsSL https://raw.githubusercontent.com/confeden/Antigravity/main/tui.sh | sh
```

In PowerShell, run as Administrator:

```powershell
irm https://raw.githubusercontent.com/confeden/Antigravity/main/tui.ps1 | iex
```

Enter the key and press Enter. Use the arrow keys to navigate, Space to toggle an option, and `q` to quit.

## Linux

Extract the archive and run `launch.sh` (double-click it or run `bash launch.sh`). Root privileges are not required. If Antigravity is installed in a root-owned directory such as `/opt`, the unlocker will request a password through `pkexec` only when it needs permission to modify the patch.

## Troubleshooting

Check the status card at the top of the window. It reports detected issues (such as antivirus software, a firewall, or another program) and suggests what to do next. If the issue persists, click **Copy Report** and share the report with the support group.

## What Changes on Your System

Changes are targeted and can be reverted using the corresponding switches.

1. **Language Server / CLI** (`language_server.exe`, `agy.exe`): two equal-length strings are changed — `ineligible` to `inexigible` (to bypass the eligibility check) and `https_proxy` to `AG_LS_PROXY`. File sizes remain unchanged.
2. **Local proxy and service** (`%ProgramData%\\AGUnlocker`, `127.0.0.1:53129`): only `AG_LS_PROXY` points to it. The system-wide `HTTPS_PROXY` variable is not changed, so Git and browsers continue to work as before. TLS traffic is not decrypted, and no certificates are installed.
3. **DNS rules (NRPT)** for `cloudcode-pa.googleapis.com` and `daily-cloudcode-pa.googleapis.com` only. Other DNS traffic, including sign-in, uses the normal route.
4. **IPv4 preference** over IPv6, only when global IPv6 is unavailable. This is reverted when the changes are rolled back.

Gemini CLI is not supported: Google has restricted sign-in for personal accounts in that client, and the README states that this cannot be bypassed client-side.

The public source code does not include the data for built-in routes, to avoid overloading public servers; the rest is built from source.

## VirusTotal

Antivirus products may flag unsigned software or software with complex internals. The source code is available publicly. If you do not trust the executable, consider testing it in a virtual machine.

---

## Project

**Telegram support group:** [@nova_txt](https://t.me/nova_txt) — questions, updates, and support.

**[Donate](https://nova-app.eu/donate)** — optional support if you find Antigravity Unlocker useful.
