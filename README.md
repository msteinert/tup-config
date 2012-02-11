# Tup-Config

Tup-config is a software configuration system based on the
[Linux Kernel](http://kernel.org/) configuration system (Kconfig). It is
designed to integrate with the [Tup](http://gittup.org/tup/) build system.
The goal of this project is to enhance the kernel build tools so they can
easily be used to configure any software package while remaining
backward-compatible with the kernel configuration system.

Currently the only changes to this software are to modify the build system
and add two new commands, `pushd` and `popd` (added by
[Mike Shal](mailto:marfey@gmail.com) to support the
[Gittup project](http://gittup.org/)).

## Included Programs

This software package includes various programs for working with Kconfig
files.

### Tup-conf

This is a command line application. Depending on what environment variables
are set this application will behave differently. This is the application
that runs when you configure the kernel with `make config`, `make oldconfig`,
etc.

### Tup-mconf

This is an [Ncurses](http://www.gnu.org/software/ncurses/)-based program. It
incorporates a modified version of the code from
[Dialog](http://invisible-island.net/dialog/) to draw widgets. This is the
application that runs when you configure the kernel with `make menuconfig`.

### Tup-nconf

This is a newer [Ncurses](http://www.gnu.org/software/ncurses/)-based program
which uses the Panel & Menu Ncurses libraries. This is the application that
runs when you configure the kernel with `make nconfig`.

### Tup-gconf

This is a graphical configuration application based on
[Gtk+](http://www.gtk.org/) and [Glade](http://glade.gnome.org/). To build
`tup-gconf` you will need the Gtk+ and Glad development files. This is the
application that runs when you configure the kernel with `make gconfig`.

### Tup-qconf

This is a graphical configuration application based on Qt. To build
`tup-qconf` this application you will need the Qt development files. This is
the application that runs when you configure the kernel with `make xconfig`.

## The Chicken and the Egg

The Tup-config software is configured using the Kconfig format. Ostensibly
you would require one of the Tup-config programs to configure this package.
In order to solve this conundrum a default configuration file is included
with the source code. The default configuration will build `tup-conf` and
`tup-mconf` (requires Ncurses).

If Ncurses is not available you can disable it in the default configuration:

    CONFIG_TUP_CONFIG_MCONF=n
    CONFIG_TUP_CONFIG_LXDIALOG=n

## Building

Tup-config is built using Tup, so you will want to
[get the source code](https://github.com/gittup/tup) and install it. The
[Tup website](http://gittup.org/tup/) explains how to install Tup (there
are even instruction for Windows & Mac). Once Tup is installed, you can build
like so (from the root of the source tree):

    $ tup init
    $ tup upd

If you used the default configuration then the configuration programs
`conf/tup-conf` and `mconf/tup-mconf` should be built.

## Installation

Currently the is no straightforward way (that I'm aware of) to automate the
installation process with Tup. No problem, simply copy the built programs
somewhere into your `PATH`:

    $ sudo cp conf/tup-conf /usr/local/bin
    $ sudo cp mconf/tup-mconf /usr/local/bin

You should now be able to reconfigure Tup-config with the newly installed
programs.
