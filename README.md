# Tizen Studio Arch Guide

This guide aims to help you install Tizen Studio (CLI, IDE version should technically work). Currently the hardest part for getting Tizen Studio to work in Arch Linux is just outdated dependencies like `gnome-doc-util` that still cannot be compiled.

## How-to
1. Download the latest version of the Tizen Studio CLI from the Samsung Developer.
2. Make sure you install all the required dependencies from the patch.
   - `yay -S procps-ng gettext dbus curl expect gtk2 grep zip make qemu-user libpng12`
   - Excluded some dependencies that takes too long to install or troublesome.
   - `yay -S webkitgtk2-bin` to install `webkitgtk2` binary.
3. This is the hacky part, install `debtap` from AUR. 
4. Download the binary for `gonome-doc-util`. You can get it [here](https://packages.ubuntu.com/bionic/gnome-doc-utils) or by other source.
5. After successfully downloaded all the files above, now run `debtap gnome-doc-utils*deb`
6. It will generate `.zst` file for `pacman` to install. 
   
   **WARNING: This can break your system, this method is not recommended but only way to circumvent the out-of-date packages**
7. After the `.zst` generated install the file using `pacman -U` <em>the package name that you generated</em>
8. Now after all done, install `gnome-desktop2`, using `yay` or any other package manager that you use, but edit the `PKGBUILD`. For `yay` you can do `yay -S --editmenu gnome-desktop2`.
9. Add `--disable-desktop-docs` on `build()`
   ![](./readme/gnome_desktop2.png)

10. After all of it done, now apply the patch on this repository. 

      `patch -u -b web-cli_Tizen_Studio_5.1_ubuntu-64.bin -i tizen_studio_cli.patch`

11. And that's all, now run the executable `./web-cli_Tizen_Studio_5.1_ubuntu-64.bin` and it should install normally.