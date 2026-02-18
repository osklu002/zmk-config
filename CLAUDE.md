# ZMK Config - Brain Keyboard

## Project Overview

This is a ZMK firmware configuration for the Brain 40-key wireless split keyboard using nice!nano v2 controllers with nice!view displays.

## Key Facts

- **Board**: nice_nano_v2
- **Shield**: brain (split: brain_left, brain_right)
- **ZMK version**: v0.3 (set in config/west.yml)
- **Build workflow**: .github/workflows/build.yml uses zmkfirmware/zmk/.github/workflows/build-user-config.yml@v0.3
- **Left half is central** (connects to computer via USB, has ZMK Studio enabled)
- **Split communication is Bluetooth only** - no wired split connection between halves
- **Swedish keyboard layout** - uses swe_keys.h for Swedish character definitions

## File Layout

- `config/brain.keymap` - The actual keymap (6 layers: default, gaming, symbols, func, number, settings)
- `config/brain.conf` - Kconfig options (display enabled)
- `config/swe_keys.h` - Swedish key code definitions (#defines for SE_* keys)
- `boards/shields/brain/` - Shield hardware definitions (GPIO matrix, physical layout)
- `boards/shields/brain/brain-layout.dtsi` - Physical layout for ZMK Studio (included by brain.dtsi)
- `build.yaml` - Build matrix (nice_nano_v2 + brain_left/right + nice_view)
- `zephyr/module.yml` - Declares board_root so build system finds shields in boards/

## Important Notes

- The shield's `boards/shields/brain/brain.keymap` is just an `#include "../../../brain.keymap"` redirect to config/brain.keymap
- ZMK Studio requires: no `zmk,matrix_transform` in the chosen node (transform comes from the physical layout instead), and `&studio_unlock` bound to a key
- `&studio_unlock` is currently on the default layer bottom-left outer key (position 22, replacing LCTRL) - this is temporary so it's accessible without the right half
- The settings layer is a conditional tri-layer activated by holding Symbols (layer 2) + Function (layer 3) simultaneously
- Keymap-drawer workflow auto-generates docs/export/brain.svg on push
- The repo needs GitHub Actions workflow write permissions enabled (Settings > Actions > General > Workflow permissions > Read and write)
- The `brain.zmk.yml` shield metadata says `requires: [pro_micro]` (nice!nano is pro_micro compatible)

## Common Tasks

- **Edit keymap**: Modify config/brain.keymap, push, download .uf2 from Actions, flash via double-tap reset
- **Live editing**: Use ZMK Studio at zmk.studio over USB (left half only)
- **Add display config**: Options go in config/brain.conf
- **Modify shield hardware**: Edit files in boards/shields/brain/

## Git

- Remote: https://github.com/osklu002/zmk-config.git
- This is a personal repo; the work machine authenticates as a different GitHub user (osklu), so pushing requires a PAT or SSH key for the osklu002 account
