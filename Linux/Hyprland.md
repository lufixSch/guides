# Hyprland

Tips and Tricks for setting up Hyprland from ground up. A lot of the tips below might also help on other setups but I encountered them while setting up Hyprland.

> NOTE: I'm using arch but most solutions should also work on other distros

## Dolphin

### "Open With" not displaying applications

Link the `*-applications.menu` (prefix depends on your setup. Could for example be `arch` or `plasma`) in `/etc/xdg/menus` to `applications.menu`

```bash
sudo ln -s /etc/xdg/menus/<xxx>-applications.menu /etc/xdg/menus/applications.menu
```

You might need to install `xdg-menu` (`archlinux-xdg-menu` on arch)

### Terminal konsole not found

This error usually occurs when Dolphin tries to open a terminal ui using the 'Konsole' terminal emulator.

Change `TerminalApplication` in `.config/kdeglobales` to your terminal emulator

```
[General]
TerminalApplication=you-terminal
```

## Screens-Sharing and Screenshots

Install the `xdg-desktop-portal-hyprland` as described in the [Hyprland Wiki](https://wiki.hyprland.org/Useful-Utilities/xdg-desktop-portal-hyprland/)
If screen-sharing doesn't work check the logs with:

```bash
journalctl -f --user-unit xdg-desktop-portal-hyprland
```

Or refer to the fixes in the Hyprland Wiki.

For screenshots you need to install `grim` (`pacman -S grim` for arch). Additionally, you might want to add `slurp` (`pacman -S slurp`) for selecting screen regions and `hyprpicker` (`yay -S hyprpicker`) as a color picker.

Create a screenshot with the following commands:

```bash
grim # Create a screenshot including all screens and saves it to ~/Pictures
slurp | grim -g - # Lets you select a region of the screen and screenshots that region
```

### Discord

**It doesn't work!**

If you really need it try using OBS with virtual camera

