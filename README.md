# Build Emacs for OSX

This repository allows you to build
[Emacs](http://www.gnu.org/software/emacs/) for Mac OSX. If you are not
familiar with Emacs building process I suggest you to grab a ready-to-use
binary version at [Emacs For Mac OSX](http://emacsformacosx.com/).

## What this version does?

Ok this is an other [Emacs](http://www.gnu.org/software/emacs/) build but
what are the differences with
[Emacs For Mac OSX](http://emacsformacosx.com/)?

- You can choose the version you want to build from any commit within the
  whole Emacs history. Well this is true for most of them (Emacs >= 24).

- A stand alone `Emacs.App` is generated. This means you only need
  dependencies for the building process. Then you can deploy the `Emacs.App`
  on any OSX desktop.

- Some very basic patches are applied:

  - Full screen support: Emacs supports OSX full screen mechanisms but lacks
    of a full screen toggle function. This patch adds `ns-toggle-fullscreen`
    which allows you to toggle full screen from Emacs itself.

  - Show git commit ID in `emacs-version`:
  ```
  GNU Emacs 24.4.50.1 (x86_64-apple-darwin, NS apple-appkit-1187.40, git sha1 10292e9) of 2014-04-28 on scrat
  ```
 All patches are included in `emacs-patches-directory` (which is located in
 the application bundle at `Contents/Resources/patches`). A list of all
 applied patched is stored in the `emacs-patches-list` variable.

 The `view-emacs-patches` function opens a `dired` buffer in
 `emacs-patches-list`. The `view-emacs-patch` opens a particular patch.


- Users Emacs directory: instead of just searching `init.el` in `~/.emacs.d`
  your configuration files will be searched in that order:

	- `~/.emacs.d-GIT_COMMIT` (i.e. `~/.emacs.d-10292e9`)
	- `~/.emacs.d-EMACS_VERSION` (i.e. `~/.emacs.d-24.4.50.1`)
	- `~/.emacs.d-EMACS_MAJOR_VERSION` (i.e. `~/.emacs.d-24`)
	- `~/.emacs.d-EMACS_MAJOR_MINOR_VERSION` (i.e. `~/.emacs.d-24.4`)
	- `~/.emacs.d`

- The C source files are included in `Contents/Resources/src` in the
  application bundle.


## Requirements

First you need to install following tools (you may want to use
[brew](http://brew.sh/) for that):

- `automake`
- `imagemagick`: you need to activate some options:
  - `--enable-hdri`
  - `--with-fontconfig`
  - `--with-ghostscript`
  - `--with-jp2`
  - `--with-liblqr`
  - `--with-rsvg`
  - `--with-libtiff`
  - `--with-libwmf`
  - `--with-little-cms`
  - `--with-little-cms2`
  - `--with-openexr`
  - `--with-perl`
  - `--with-quantum-depth-16`
  - `--with-webp`
- `gnutls`

You also need to checkout an Emacs git repository. I suggest you to use
[Savannah's](this) which is the most up-to-date.

	git clone git://git.savannah.gnu.org/emacs.git


## Building Emacs for OSX

Once all requirements are installed you can just run:

	./build-emacs

If you want to build a specific version you just can pass the commit id or
tag to the `build-emacs` script:

	./build-emacs emacs-24.4

## configuration report

This is a summary of activated options given during the configure part:

    Configured for `x86_64-apple-darwin'.
    
      Where should the build process find the source code?    .
      What compiler should emacs be built with?               gcc -std=gnu99  -pipe -march=nocona
      Should Emacs use the GNU version of malloc?             no
        (The GNU allocators don't work with this system configuration.)
      Should Emacs use a relocating allocator for buffers?    no
      Should Emacs use mmap(2) for buffer allocation?         no
      What window system should Emacs use?                    nextstep
      What toolkit should Emacs use?                          none
      Where do we find X Windows header files?                /usr/X11/include
      Where do we find X Windows libraries?                   /usr/X11/lib
      Does Emacs use -lXaw3d?                                 no
      Does Emacs use -lXpm?                                   no
      Does Emacs use -ljpeg?                                  no
      Does Emacs use -ltiff?                                  no
      Does Emacs use a gif library?                           no
      Does Emacs use a png library?                           no
      Does Emacs use -lrsvg-2?                                no
      Does Emacs use imagemagick?                             yes
      Does Emacs support sound?                               no
      Does Emacs use -lgpm?                                   no
      Does Emacs use -ldbus?                                  no
      Does Emacs use -lgconf?                                 no
      Does Emacs use GSettings?                               no
      Does Emacs use a file notification library?             no
      Does Emacs use access control lists?                    yes
      Does Emacs use -lselinux?                               no
      Does Emacs use -lgnutls?                                yes
      Does Emacs use -lxml2?                                  yes
      Does Emacs use -lfreetype?                              no
      Does Emacs use -lm17n-flt?                              no
      Does Emacs use -lotf?                                   no
      Does Emacs use -lxft?                                   no
      Does Emacs directly use zlib?                           yes
      Does Emacs use toolkit scroll bars?                     yes
