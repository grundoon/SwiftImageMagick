# SwiftImageMagick

Swift wrapper for ImageMagick 6.9.10-81 library.

This is provided for use with https://github.com/grundoon/swiftarr-fotomat, and the following is really only of concern if  modifying `swiftarr-fotomat` itself on macOS using Xcode. You should otherwise probably just be running the microservice from the containerized Docker version, or directly on bare metal Ubuntu. The linux side of things is not nearly so version-picky.

Unless you happen to have the exact 6.9.10-81 version installed, and in the same location, you'll need to edit `module.modulemap`.

On macOS:

1. Install ImageMagick using Homebrew.

```shell
% brew install imagemagick@6
```

2. In order for `pkg-config` to find the ImageMagick@6 installation, add it to your `PKG-CONFIG-PATH` (if you don't have `pkg-config` installed, `brew install pkg-config`).

```shell
% echo 'export PKG_CONFIG_PATH="/usr/local/opt/imagemagick@6/lib/pkgconfig:$PKG_CONFIG_PATH"' >> ~/.zshrc
```

3. `pkg-config` should now be able to find the installed packages.

```shell
% pkg-config --list-all | grep -i Magick // should list out a dozen
```

4. Find the header file directory.

```shell
% pkg-config --cflags-only-I MagickWand
-I/usr/local/Cellar/imagemagick@6/6.9.10-81/include/ImageMagick-6
                                  ^^^^^^^^^
```

5. Edit the "header" line in `module.modulemap` to match that version.
