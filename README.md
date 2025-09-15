# Set GDM Wallpaper for GNOME 45+

A simple script to set a custom background image for the GDM (login screen) on GNOME 45 and newer (45+).

## Description

This script automates the process of changing the GDM background by modifying the `gnome-shell-theme.gresource` file. It works by:
1. Extracting the default GDM theme resources.
2. Adding your custom wallpaper to the resource bundle.
3. Patching the relevant CSS files to display your wallpaper.
4. Re-compiling the theme resources.
5. Backing up the original theme file.
6. Installing the new theme file.
7. Restarting GDM to apply the changes.

## Requirements

You must have the following command-line tools installed:
- `glib-compile-resources` (often in `libglib2.0-dev` or `glib2-devel`)
- `gresource` (often in `libglib2.0-bin` or `glib2`)
- `coreutils`, `sed`, `find`, `mktemp` (standard on most Linux systems)


## Usage

Download the `set-gdm-wallpaper45` script and make it executable:

```sh
chmod +x set-gdm-wallpaper45
```

### Install a custom wallpaper

```sh
sudo ./set-gdm-wallpaper45 -i /absolute/path/to/image.png
```

### Blur the wallpaper (optional)

You can blur the wallpaper using ImageMagick before installing:

```sh
sudo ./set-gdm-wallpaper45 -i /absolute/path/to/image.png -b 8
```

- The `-b` or `--blur` option takes a blur strength (recommended: 5–15, try 8; range: 1–30+).
- Requires ImageMagick (`magick` command).

### Restore the default GDM theme and remove all backups

```sh
sudo ./set-gdm-wallpaper45 -r
```

This restores the original GDM theme and deletes all custom backups created by the script.



> **Warning:** The script will prompt you before restarting the GNOME Display Manager (`gdm`). Restarting GDM will immediately terminate your current user session and log you out. Save any open work before running it. If you choose not to restart GDM immediately, you must do so manually (or reboot) for the wallpaper change to take effect.

## Reverting Changes

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
