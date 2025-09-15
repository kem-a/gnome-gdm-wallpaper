# Set GDM Wallpaper for GNOME 45+

A simple script to set a custom background image for the GDM (login screen) on GNOME 45 and newer (45+)

## Requirements

You must have the following command-line tools installed:
- `glib-compile-resources` (often in `libglib2.0-dev` or `glib2-devel`)
- `gresource` (often in `libglib2.0-bin` or `glib2`)
- `ImageMagick` (`magick`) — only required if you use the blur option
#### Installing dependencies

```bash
sudo dnf install glib2 glib2-devel ImageMagick
```

## Usage

#### Download and make it executable

```bash
git clone https://github.com/kem-a/gnome-gdm-wallpaper && cd gnome-gdm-wallpaper && chmod +x set-gdm-wallpaper
```

#### Install GDM wallpaper

```sh
sudo ./set-gdm-wallpaper -i /absolute/path/to/image.png -b 8
```

#### Restore default

```sh
sudo ./set-gdm-wallpaper -r
```

#### Command-line arguments

| Argument | Description |
| --- | --- |
| `-i, --install <image>` | Install a custom wallpaper for GDM from an absolute image path (`.png`/`.jpg`/`.jpeg`). |
| `-b, --blur <XX>` | Blur the wallpaper using ImageMagick before installing. Recommended: 5–15 (try 8); usable range ~1–30+. Requires `magick`. |
| `-r, --remove` | Restore the default GDM theme and delete all custom backups created by the script. |
| `-h, --help` | Show usage help and exit. |



> **Warning:** The script will prompt you before restarting the GNOME Display Manager (`gdm`). Restarting GDM will immediately terminate your current user session and log you out. Save any open work before running it. If you choose not to restart GDM immediately, you must do so manually (or reboot) for the wallpaper change to take effect.

## Manually Reverting Changes

The script automatically creates a timestamped backup of the original theme file in `/usr/share/gnome-shell/` with a name like `gnome-shell-theme.gresource.bak-YYYYMMDD-HHMMSS`.

To restore the original login screen, you can list the backups and copy one back into place.

1.  Find a backup:
    ```sh
    ls -l /usr/share/gnome-shell/gnome-shell-theme.gresource.bak-*
    ```
2.  Copy the backup over the modified file (you will need `sudo`):
    ```sh
    sudo cp /usr/share/gnome-shell/gnome-shell-theme.gresource.bak-20250829-123456 /usr/share/gnome-shell/gnome-shell-theme.gresource
    ```
3.  Restart GDM to see the change:
    ```sh
    sudo systemctl restart gdm
    ```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
