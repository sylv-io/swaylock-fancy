swaylock-fancy
============

This is an swaylock bash script that takes a screenshot of the desktop, blurs the background and adds a lock icon and text

![screen shot of lockscreen](https://raw.githubusercontent.com/meskarune/i3lock-fancy/master/screenshot.png)

Dependencies
------------
* <s>[i3lock-color-git](https://github.com/eBrnd/i3lock-color)</s>
* <s>[i3lock-color-git](https://github.com/PandorasFox/i3lock-color) - this is a fork of i3lock-color that is kept up to date with i3lock</s>
* [i3lock-fancy-git](https://github.com/meskarune/i3lock-fancy) - this is a fork of i3lock-fancy that is kept up to date with i3lock
* imagemagick
* bash
* awk
* util-linux
* grim

Optional Dependencies
---------------------
* wmctrl

Installation
------------

To install swaylock-fancy manually, git clone the repository:

    git clone https://github.com/Big-B/swaylock-fancy.git

Then change to the directory and run make.

    cd swaylock-fancy
    sudo make install

### The following distro's have packages you can use to install:
* Arch Linux: https://aur.archlinux.org/packages/swaylock-fancy-git/

Usage
-----

    swaylock-fancy [options]

    Options:
        -h, --help       This help menu.

        -d, --desktop    Attempt to minimize all windows before locking. Requires wmctrl.

        -g, --greyscale  Set background to greyscale instead of color.

        -p, --pixelate   Pixelate the background instead of blur, runs faster.

        -f <fontname>, --font <fontname>  Set a custom font.

        -t <text>, --text <text> Set a custom text prompt.

        -l, --listfonts  Display a list of possible fonts for use with -f/--font.
                         Note: this option will not lock the screen, it displays
                         the list and exits immediately.

example: ```swaylock-fancy -gpf Comic-Sans-MS```

Extras
------

The lock screen in action:

![lockscreen animation](https://raw.githubusercontent.com/meskarune/i3lock-fancy/master/action.gif)

To use this script you can set a hotkey in your window manager to run the lock command,
set xautolock to run at boot, or use a systemd script to either lock on suspend or run xautolock.

xautolock is a utility to automatically lock the screen after a set time. It also
supports hot corners.

Systemd Unit file example (edit for your own use):

    [Unit]
    Description=Lock the screen automatically after a timeout

    [Service]
    Type=simple
    User=meskarune
    Environment=DISPLAY=:0
    ExecStart=/usr/bin/xautolock -time 5 -locker /usr/bin/swaylock-fancy -detectsleep

    [Install]
    WantedBy=graphical.target

Multiple Monitors
-----------------
Work in progress
