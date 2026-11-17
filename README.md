<p align="center">
  <img src="assets/ssh-vita-logo.png" alt="ssh-vita logo" width="128" height="128">
</p>

<h1 align="center">ssh-vita</h1>

SSH and SFTP for homebrew-enabled PlayStation Vita systems.

[Third-party notices](LICENSE.md)

**Version:** 1.4.2  
**Tested firmware:** 3.65

<p align="center">
  <img src="assets/ssh-vita-screenshot.png" alt="ssh-vita app interface" width="960">
</p>

## Uses
Examples
- SSH to access your vita
- Allow your agent to take full control of your Vita
- Agents can create and modify games; Create cheats, modify saved files, and more
- Agents can directly create plugins
- Change UI layout and more

## Features

- SSH-2 terminal access, command execution, and SFTP file transfers.
- Optional background startup with a delayed service launcher.
- Select + D-pad Left opens a text menu from LiveArea or a game.
 <p align="center">
  <img src="assets/mini-menu.png" alt="ssh-vita mini-menu interface" width="400">
</p>
- Start, stop, and restart SSH from the menu without opening the app.
- Manual background keep-awake; OFF after every reboot.
- The app defaults to keeping its screen awake while open.
- Process and module inspection, checked memory tools, and screenshots.
- Timed button, touch, and analog commands.
- AES-CTR and ChaCha20-Poly1305 SSH ciphers.
- Archive extraction, HTTP downloads, installed-app listings, and additional text tools.
- Memory search, filtering, and timed value freezing.
- Optional saved safe memory mode, with timed write unlocking on the Vita.
- Login lockout after repeated authentication failures.

## Changes in 1.4.2

- Bound login fields and wrap connection instructions to fit the app display.
- Includes the expanded commands and optional safe memory mode introduced in 1.4.0 and 1.4.1.

## Changes in 1.4.1

- Optional safe memory mode is OFF by default and saved across reboots.
- D-pad Right toggles the mode; D-pad Left unlocks memory writes for 10 minutes.
- While enabled, the mode restricts memory ranges and operation sizes, checks memory availability for heavy commands, and protects its settings from shell and SFTP changes.
- The mapped-range check is a heuristic, not a guarantee that every memory operation is valid.

## Changes in 1.4.0

- Added AES-128-CTR and AES-256-CTR with HMAC-SHA2-256, alongside ChaCha20-Poly1305.
- Added `unzip`, `tar`, `gunzip`, `curl`, `wget`, `nc -z`, `apps`, and text utilities.
- Added `mem search`, `mem filter`, `mem results`, `mem freeze`, and `mem clear`.
- Added a 60-second address lockout after five failed logins and a default-password reminder.
- HTTP downloads accept numeric IPv4 addresses; HTTPS and DNS are not supported.

## Changes in 1.3.8

- One SSH service replaces the separate app/background controls.
- A resident menu shows the service state, address, and connected clients, with controls for SSH and background keep-awake.
- Stopping SSH leaves the menu available to start it again. Restart closes existing SSH sessions before reopening the listener.
- App screen always-on defaults to ON and does not enable background keep-awake.

## Install

1. Download the release ZIP and extract `ssh-vita.vpk`.
2. Transfer the VPK to the Vita and install it with VitaShell.
3. Open **ssh-vita**. The app displays the address, port, and login information.
4. Reboot after an upgrade so the background service and kernel helper match.

Connect using the address and login shown by the app:

```sh
ssh USER@VITA_IP
sftp USER@VITA_IP
```

## App controls

| Button | Action |
| --- | --- |
| X | Start or stop SSH |
| Up | Restart SSH |
| Down | Toggle background keep-awake ON/OFF |
| L | Install or remove automatic SSH startup |
| R | Save a screenshot |
| Select | Toggle app screen always-on (defaults ON) |
| Select + Left | Open or close the resident text menu |
| Start | Reload settings |
| Triangle | Toggle password authentication |
| Square | Generate a new password |
| Circle | Exit the app |
| D-pad Right | Toggle safe memory mode (saved; defaults OFF) |
| D-pad Left | Unlock memory writes for 10 minutes while safe memory mode is ON |

## Plugin menu

Install automatic startup with **L** in the app, then reboot after upgrading.
Press **Select + D-pad Left** from LiveArea or a game to open the text menu.
SSH runs independently of the app, including after closing it.

The menu displays SSH's current state, the device address and port, and the
number of connected clients.

| Menu item | Action |
| --- | --- |
| Start SSH / Stop SSH | Start or stop the listener; the menu remains available when SSH is stopped |
| Restart SSH | Disconnect existing clients and restart the listener |
| Keep awake: ON/OFF | Toggle background keep-awake without opening the app |

Use **Up/Down** to choose an item and **X** to apply it. Press **Circle** or
**Select + D-pad Left** again to close the menu. Menu button navigation is
filtered so it does not also move the underlying Vita interface or game.
Stopping or restarting SSH disconnects existing clients.

Background keep-awake is **OFF after every reboot**. Toggle it in the menu or
with **Down inside ssh-vita**. An explicit enable continues after leaving the
app. The app's separate screen always-on setting defaults to **ON each time
the app opens** and only applies while the app is active.

## Startup and recovery

Press **L** in the app to enable or remove automatic SSH startup. When enabled,
the service starts after a short boot delay and becomes reachable once Wi-Fi
is connected. The app does not need to be opened; closing it does not stop SSH.
Removing startup changes future boots and does not stop the current service.

Hold **D-pad Up from power-on until LiveArea appears** to skip background SSH
for that boot. The app can still be opened manually. The next normal boot
restores enabled startup. For an earlier module-loading failure, the standard
**hold L at boot** plugin bypass remains available.

Run `help` for the full command list. Memory and input tools require the matching
kernel helper. Screen capture requires an available application framebuffer.

## Third-party notices

See [Third-party notices](LICENSE.md) for the bundled components’ copyright notices and license terms.
