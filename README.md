# Neon Dreams CredRig Emulator

A software CredRig for Raspberry Pi cyberdecks. It speaks the same serial
protocol as the hardware rigs, so a deck can send, receive and loot credits
with any other deck or rig it's cabled to.

## Install

You need a Raspberry Pi running the current 64-bit Raspberry Pi OS.

1. Download the latest `credrig-emu` file from the
   [Releases page](https://github.com/justintesmer/neon-dreams-playerdeck-credrig/releases/latest).
2. Open a terminal in the folder you saved it to and run:

```bash
chmod +x credrig-emu-*
./credrig-emu-*
```

Nothing else needs installing. Your wallet and settings are kept in the
`.credrig` folder in your home directory.

## Test mode

A fresh install starts in **TEST MODE**. Your deck gives itself a temporary
ID (`TEST_` plus four characters) and 125 test credits. Everything works, so
you can cable up to another deck and check your build before the event.

At the event, staff will check your deck in. That assigns your real ID and
sets your starting balance. Test credits don't carry over.

## Controls

| Key | Action |
| --- | --- |
| Left / Right | Change page (INFO / MAIN / LOOT) |
| Up / Down | Dial the amount to send |
| Enter | Send, start a loot, or submit |
| PgUp / PgDn / End | Scroll the protocol log / back to live |
| Esc | Quit |

## Serial connection

The top right of the screen shows the serial port in use, or **OFFLINE** in
red if none was found.

By default the emulator looks for a USB-to-serial adapter first, then the
Pi's GPIO serial pins. Use 3.3 V logic only, and connect TX, RX and GND.

To set the port yourself, run the emulator once, then edit
`~/.credrig/config.json` and change `serial_port`, for example to
`/dev/ttyUSB0` or `/dev/serial0`.

If the port won't open, add yourself to the serial group, then log out and
back in:

```bash
sudo usermod -aG dialout $USER
```

## Settings

`~/.credrig/config.json`:

| Setting | Default | Meaning |
| --- | --- | --- |
| `serial_port` | `"auto"` | `"auto"` or a device path |
| `fullscreen` | `false` | `true` fills the screen (800×480 layout) |
