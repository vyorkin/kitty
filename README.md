# kitty

My config for the Kitty terminal.

## Branches

- **`main`** — macOS.
- **`omarchy`** — Linux/Omarchy only. Use this branch exclusively on
  [Omarchy](https://omarchy.org/) (Arch Linux + Hyprland). It is a port of
  `main`: macOS-only options are removed, shortcuts are remapped for Hyprland,
  and colors follow the active Omarchy theme instead of a bundled color scheme.

The `omarchy` branch is deployed to `~/.config/kitty/`.

## omarchy branch

### What differs from `main`

- **No bundled color schemes.** `themes/`, `Tokyo Night.conf`,
  `dark-theme.auto.conf`, `light-theme.auto.conf` and
  `no-preference-theme.auto.conf` were removed. Colors come from
  `include ~/.local/state/omarchy/current/theme/kitty.conf`, which Omarchy
  writes from the active theme (`omarchy theme set ...`). The session-only
  `set_colors` shortcuts are gone, so the terminal always matches the OS theme.
- **macOS options dropped:** `macos_*`, the Option/Cmd maps, and the 36pt
  camera-notch `window_margin_width` / `single_window_margin_width`.
- **`kitty_mod` is `ctrl+shift`** (kitty's default) because SUPER drives
  Hyprland; `main` used SUPER/Cmd.
- **Window moves remapped.** Splits stay on `ctrl+shift+l` / `ctrl+shift+j`.
  Because `kitty_mod` already contains Shift, `main`'s
  `kitty_mod+shift+h/j/k/l` would collapse onto `kitty_mod+h/j/k/l`, so moves
  use `ctrl+shift+alt+h/j/k/l`.
- **Tabs and clipboard remapped:** `ctrl+shift+t` new tab, `ctrl+shift+1..9`
  goto tab, `ctrl+shift+c` / `ctrl+shift+v` copy/paste.
- **Opacity and blur are the compositor's job.** `background_opacity 1.00`;
  native `background_blur`, `dynamic_background_opacity`, and kitty's own
  opacity-adjust maps are dropped. Omarchy applies opacity and blur through a
  Hyprland window rule (`~/.config/hypr/glass.lua` + `terminal-glass`).
- **Remote control socket matches Omarchy:**
  `listen_on unix:${XDG_RUNTIME_DIR}/omarchy-kitty-{kitty_pid}`, so
  `omarchy-cmd-terminal-cwd` and `omarchy launch terminal` can resolve the
  active terminal's working directory.
- **Icons:** the primary font is JuliaMono (from `main`); its Nerd Font glyph
  ranges are mapped to the installed JetBrainsMono Nerd Font instead of the
  macOS-only `Symbols Nerd Font Mono`.

### Requirements

- Omarchy (Arch Linux + Hyprland).
- `kitty` set as the default terminal: `omarchy default terminal kitty`.
- JuliaMono and JetBrainsMono Nerd Font installed.

### Usage

Copy `kitty.conf` to `~/.config/kitty/kitty.conf`, then reload:

```sh
omarchy restart terminal
```
