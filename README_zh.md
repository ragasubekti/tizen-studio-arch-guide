以下是Tizen Studio Arch指南。

该指南的目的是帮助在Arch Linux上安装Tizen Studio，特别是CLI版本，尽管IDE版本也应该能够工作。在Arch Linux上安装Tizen Studio最具挑战性的方面是处理过时的依赖项，例如无法编译的 `gnome-doc-util`。

### 操作步骤

要在Arch Linux上安装Tizen Studio，请按照以下步骤操作：

1. 从Samsung Developer网站下载最新版本的[Tizen Studio CLI](https://developer.tizen.org/development/tizen-studio/download)。
2. 运行以下命令从补丁中安装所有必要的依赖项：

   ```
   yay -S procps-ng gettext dbus curl expect gtk2 grep zip make qemu-user libpng12 webkitgtk2-bin
   ```
   注意：某些需要很长时间安装或麻烦的依赖项已被排除。

   ```
   yay -S webkitgtk2-bin
   ```
   要安装`webkitgtk2`二进制版本，请自行编译并删除`-bin`。

3. 从AUR存储库安装`debtap`。
4. 从[此处](https://packages.ubuntu.com/bionic/gnome-doc-utils)或任何其他来源下载“gnome-doc-utils”的二进制文件。
5. 成功下载所需的所有文件后，运行`debtap gnome-doc-utils*deb`。
6. 该命令将生成一个可以使用`pacman`安装的`.zst`文件。
7. 使用`pacman -U`安装生成的`.zst`文件。**请注意，此方法不被推荐，可能会破坏您的系统。**
8. 使用`yay`或您使用的任何其他软件包管理器安装`gnome-desktop2`。在`build()`中添加`--disable-desktop-docs`以编辑`PKGBUILD`。

   ![](./readme/gnome_desktop2.png)

9. 完成上述步骤后，应用补丁到此存储库：

   ```
   patch -u -b web-cli_Tizen_Studio_5.1_ubuntu-64.bin -i tizen_studio_cli.patch
   ```

10. 最后，运行可执行文件`./web-cli_Tizen_Studio_5.1_ubuntu-64.bin`以完成安装。

按照这些步骤，您应该能够成功在Arch Linux上安装Tizen Studio。