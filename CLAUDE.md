# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Personal kitty terminal configuration (dotfiles). Deployed to `~/.config/kitty/`. This is not a software project — there is no build system, tests, or linting.

## Repository Structure

- `kitty.conf` — Main configuration file. Uses vim foldmarkers (`{{{`/`}}}`) for sections.
- `themes/` — ~170 color theme `.conf` files (one per theme).
- `*.auto.conf` — OS-level automatic theme switching files: `dark-theme.auto.conf`, `light-theme.auto.conf`, `no-preference-theme.auto.conf`. These are loaded by kitty based on macOS appearance settings.
- `Tokyo Night.conf` — Standalone Tokyo Night theme (from tokyonight.nvim).

## Key Configuration Choices

- **kitty_mod** is set to `super` (Cmd on macOS), not the default `ctrl+shift`.
- **macOS-specific**: `macos_option_as_alt yes`, `hide_window_decorations titlebar-only`, `macos_traditional_fullscreen yes`, `macos_quit_when_last_window_closed yes`.
- **Transparency**: `background_opacity 0.72` with `dynamic_background_opacity yes`. Opacity shortcuts use `super+a>` prefix (l/h to adjust, 1/2/d for presets).
- **Remote control**: Enabled via `allow_remote_control socket-only` with `listen_on unix:/tmp/kitty`.
- **Font**: JuliaMono (managed by kitty's `BEGIN_KITTY_FONTS`/`END_KITTY_FONTS` block at the end of the file — don't manually edit this block).
- **Tab bar**: Powerline style with angled separators, shown even with 1 tab.
- **Theme switching shortcuts**: `cmd+alt+1` through `cmd+alt+0` switch between preset color themes.
- **Window splits**: `super+l` for horizontal split, `super+j` for vertical split. `super+shift+h/j/k/l` to move windows.
- **Window margin**: Top margin of 36pt (`window_margin_width 36 0 0 0`) to accommodate macOS camera.

## When Editing

- Themes in `kitty.conf` are referenced via `include ~/.config/kitty/themes/...` paths (the deployed location), not relative paths.
- Many options are commented out with their defaults shown — these are documentation, not dead code. Only uncomment if changing from default.
- The config uses kitty's fold marker syntax (`#: Section {{{` / `#: }}}`) for organization.
