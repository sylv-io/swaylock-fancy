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

**IMPORTANT NOTE: the way to install swaylock-fancy has changed! If you are a
  package maintainer or previously installed manually you may have to review
  and update your configurations. The new change simplifies a lot of
  things so updates will be easier in the future.**

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

        -n, --nofork     Do not fork swaylock after starting.

        --               Must be last option. Set command to use for taking a
                         screenshot. Default is 'import -window root'. Using 'scrot'
                         or 'maim' will increase script speed and allow setting
                         custom flags like haing a delay.

example: ```swaylock-fancy -gpf Comic-Sans-MS -- scrot -z```

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
Not supported currently.

Static image
------------
If you would like to run `swaylock-color` with a static image in the style of
i3lock-fancy, run `convert` from image magick directly on the background image
you want to use. Then specify the result `newimage.png` to `swaylock -i`:
```
#!/bin/sh
# Add a lock icon and text to the center of an image
convert /path/to/background.png -font Liberation-Sans \
    -pointsize 26 -fill white -gravity center \
    -annotate +0+160 "Type Password to Unlock" lock.png \
    -gravity center -composite newimage.png
```

```
swaylock -i newimage.png
```
