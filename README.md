# omarchy-hyprland

The Hyprland companion tools and desktop portals Omarchy's session depends on, as
a charly layer layered over the compositor itself.

The `omarchy-hyprland` candy deliberately does **not** install Hyprland:
`pod-hyprland` already owns the compositor, Xwayland and the nested session that
runs it, and declaring them twice would put the same behaviour in two places.
What this candy adds is the surrounding set Omarchy's own configuration and
keybindings invoke — the colour picker (`hyprpicker`), the night-light daemon
(`hyprsunset`), the GUI dialogs (`hyprland-guiutils`), the screen-share picker,
the Qt6 Wayland platform plugin, and the xdg-desktop-portal backends without
which screen sharing and file dialogs silently fail inside a Hyprland session.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `omarchy-hyprland` |
| Requires | `layer-omarchy-base`, `pod-hyprland` (the compositor) |
| Tools | `hyprpicker`, `hyprsunset`, `hyprland-guiutils`, `hyprland-preview-share-picker`, `qt6-wayland`, `xdg-terminal-exec` |
| Portals | `xdg-desktop-portal-hyprland`, `xdg-desktop-portal-gtk` |
| Service / port | none (additive over the compositor) |

## How to use it

Compose the layer by pinning the member candy's sub-path in a desktop box's
`candy:` list. The `omarchy-cstream` image does exactly this:

```yaml
omarchy-cstream:
  candy:
    base: omarchy
    candy:
      - '@github.com/opencharly/layer-omarchy-hyprland/candy/omarchy-hyprland:v2026.243.1042'
      # ... the shell, terminal, themes and fonts layers
```

## Layout

- `charly.yml` — repo shape: the `discover:` rule that finds the member candy.
- `candy/omarchy-hyprland/charly.yml` — the candy entity (the `require:` deps,
  the `distro:` package arm, and the `plan:` `check:` assertions).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

This repo carries no `skill:` entity of its own; `/charly-distros:omarchy-base` is the closest
family owning procedure.

- Compositor: `/charly-pod:hyprland` — the compositor this candy layers over.
- Foundation: `/charly-distros:omarchy-base`.
- Streaming desktop: `/charly-distros:omarchy-cstream`.
- [`opencharly/opencharly](https://github.com/opencharly/opencharly) — the umbrella.
