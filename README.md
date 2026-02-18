# ZMK Config - Brain Keyboard

ZMK firmware configuration for the [Brain](https://github.com/Wesztman/brain) 40-key wireless split keyboard.

## Hardware

- **Keyboard**: Brain (based on Urchin design)
- **MCU**: nice!nano v2 (nRF52840)
- **Switches**: Kailh Choc v1 (hotswap)
- **Display**: nice!view
- **Split communication**: Bluetooth (left half is central)

## Layout

40 keys arranged as:
- Top row: 10 keys (5+5)
- Middle row: 12 keys (6+6, with outer pinky columns)
- Bottom row: 12 keys (6+6, with outer pinky columns)
- Thumb cluster: 6 keys (3+3)

```
         ╭─────────────────╮ ╭─────────────────╮
         │  Q  W  E  R  T  │ │  Y  U  I  O  P  │
    SHFT │  A  S  D  F  G  │ │  H  J  K  L  Ö  │ Å
    CTRL │  Z  X  C  V  B  │ │  N  M  ,  .  ?  │ Ä
         ╰───╮ TAB GUI SPC │ │ ENT BSP ESC ╭───╯
              ╰─────────────╯ ╰─────────────╯
```

## Layers

| # | Layer | Activation |
|---|-------|------------|
| 0 | Default | QWERTY with Swedish characters |
| 1 | Gaming | Alternative layout for games |
| 2 | Symbols (SWE) | Swedish symbol mappings |
| 3 | Function | F-keys, arrows, media |
| 4 | Number | Numpad-style number entry |
| 5 | Settings | Bluetooth, power, bootloader (tri-layer: Symbols + Function) |

## Features

- **Homerow mods**: Hold home row keys for modifiers (200ms/300ms tapping term)
- **Swedish key support**: Full Swedish keyboard layout via `swe_keys.h`
- **ZMK Studio**: Live keymap editing over USB (left half only)
- **nice!view display**: Battery and connection status
- **Conditional layer**: Settings layer activates when Symbols and Function are both held

## Building

Firmware builds automatically via GitHub Actions on push. Download `.uf2` files from the [Actions tab](../../actions).

To flash: double-tap reset on the nice!nano, then copy the `.uf2` to the USB drive that appears.

## Repo Structure

```
build.yaml                          # GitHub Actions build matrix
config/
  brain.conf                        # Keyboard config (display, etc.)
  brain.keymap                      # Keymap definitions
  brain.json                        # Layout for keymap-drawer
  swe_keys.h                        # Swedish key definitions
  west.yml                          # West/Zephyr manifest
boards/shields/brain/
  brain.dtsi                        # Base shield devicetree
  brain-layout.dtsi                 # Physical layout (ZMK Studio)
  brain_left.overlay                # Left half GPIO matrix
  brain_right.overlay               # Right half GPIO matrix
  brain.zmk.yml                     # ZMK shield metadata
  Kconfig.shield / Kconfig.defconfig
docs/export/
  brain.svg                         # Auto-generated keymap diagram
```

## References

- [Brain keyboard hardware](https://github.com/Wesztman/brain)
- [ZMK documentation](https://zmk.dev)
- [ZMK Studio](https://zmk.studio)
