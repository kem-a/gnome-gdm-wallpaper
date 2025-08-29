# Set GDM Wallpaper for GNOME 45+

A simple script to set a custom background image for the GDM (login screen) on GNOME 45, 46, 47, and 48.

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

1.  Download the `set-gdm-wallpaper45` script.
2.  Make it executable:
    ```sh
    chmod +x set-gdm-wallpaper45
    ```
3.  Run the script with `sudo`, passing the absolute path to your desired wallpaper image. The image must be a PNG or JPG/JPEG file.

    ```sh
    sudo ./set-gdm-wallpaper45 /home/user/Pictures/my-awesome-wallpaper.png
    ```

> **Warning:** The script will restart the GNOME Display Manager (`gdm`), which will immediately terminate your current user session and log you out. Save any open work before running it.

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
