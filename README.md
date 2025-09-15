# Set GDM Wallpaper for GNOME 45+

A simple script to set a custom background image for the GDM (login screen) on GNOME 45 and newer (45+).

## Description

This script automates the process of changing the GDM background by modifying the `gnome-shell-theme.gresource` file. It works by:


## Requirements

You must have the following command-line tools installed:
- `glib-compile-resources` (often in `libglib2.0-dev` or `glib2-devel`)
- `gresource` (often in `libglib2.0-bin` or `glib2`)
- `coreutils`, `sed`, `find`, `mktemp` (standard on most Linux systems)
 - `ImageMagick` only required if you use the blur option


## Usage (simple)

Make the script executable:

```sh
chmod +x set-gdm-wallpaper
```

- Install a wallpaper:

```sh
sudo ./set-gdm-wallpaper -i /absolute/path/to/image.png
```

- Install with blur (optional):

```sh
sudo ./set-gdm-wallpaper -i /absolute/path/to/image.png -b 8
```

    - Blur strength: recommended 5–15 (try 8); usable range ~1–30+.
    - Requires ImageMagick (`magick`).

- Restore default and remove backups:

```sh
sudo ./set-gdm-wallpaper -r
```

This restores the original GDM theme and deletes all custom backups created by the script.



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
