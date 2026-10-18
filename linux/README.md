# Antigravity Unlocker — Linux (Beta Port)

Unlock Antigravity 2.0 / IDE / CLI on Linux. The tool does two things:

1. **Patches client binaries and JavaScript** to bypass the eligibility check.
2. **Proxy routing (to work around the “400 — User location is not supported” error):** starts a local proxy and routes requests to Google servers through an exit in a supported region, addressing the server-side regional restriction. You do **not** need your own VPN or proxy; the tool uses its built-in exit route.

Everything runs as a **regular user, without root privileges** (sudo is not requested).

## Quick Start

1. Extract the archive anywhere. A shared VM folder or a Windows drive is also fine. If programs cannot be launched from that location, the unlocker will copy itself to your home directory.
2. Double-click **`launch.sh`** and choose **“Run as a Program”**, or run `bash launch.sh` in a terminal. **Do not use `sudo`**; the unlocker will not run under sudo and will explain why. It will first ask for a key (available for free in the [Telegram group](https://t.me/nova_txt)), then show the available switches.
3. Click **“Enable All”**.
4. **Fully close Antigravity and reopen it.** The language server will pick up the proxy, and the 400 error should be resolved.

To launch it from your applications menu, run `bash install.sh` once.

Without a graphical desktop (for example, on a server over SSH), the unlocker opens directly in the terminal. You can also launch the terminal UI without downloading the archive manually:

```bash
curl -fsSL https://raw.githubusercontent.com/confeden/Antigravity/main/tui.sh | sh
```

## How to Disable It

Turn off the same switches you enabled. **“Unlock Account Sign-in”** restores the original files, while **“Bypass Error 400”** removes the local proxy and `AG_LS_PROXY`.

To disable it manually, remove `~/.config/environment.d/ag-unlocker.conf` and run:

```bash
systemctl --user disable --now ag-unlocker-proxy
```

## If the Installation Is Not Detected Automatically

Click the **✏ pencil icon** next to the relevant installation and enter its path manually. Common locations include:

- `/opt/antigravity`
- `~/.local/share/antigravity`
- `~/.local/bin` (CLI)

The Snap version cannot be patched because it is read-only. Use a non-Snap installation instead.

## Linux Limitations

The DNS layer (NRPT rules and a local relay on port `:53`) is Windows-only. On Linux, the client patch and proxy routing through the built-in exit route are available; DNS-related switches in the interface will not install anything.

## Files

| File | Description |
|---|---|
| `ag_unlocker` | Patcher, proxy, graphical interface, and terminal UI (ELF x86-64, glibc 2.17+) |
| `launch.sh` | Launcher wrapper: checks execution permissions and starts the terminal UI when no graphical session is available |
| `Antigravity-Unlocker.desktop` | Desktop shortcut |
| `install.sh` | Adds the shortcut to the applications menu |
