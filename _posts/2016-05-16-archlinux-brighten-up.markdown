---
published: true
title: ArchLinux - Brighten up
layout: post
---
Even though we have sophisticated commands like xbrightness and xrandr, it is fun to learn this mundane way to vary screen brightness.

With root permissions, navigate to this location `/sys/class/backlight`.

You might have one out of `intel_backlight` (Intel graphics) or `acpi_video0` (ATI graphics). Go into that directory.


    $ ls /sys/class/backlight/intel_backlight
    actual_brightness  brightness  max_brightness  subsystem  uevent
    bl_power           device      power           type


Now, `cat` `max_brightness` and `brightness` files to find out the max and current values of brightness.

    $ cat /sys/class/backlight/intel_backlight/max_brightness 
    4882

    $ cat /sys/class/backlight/intel_backlight/brightness 
    400

Now, to change brightness, change the value in the brightness file. You cannot make it higher than the max_brightness.

    $ echo 200 > /sys/class/backlight/intel_backlight/brightness 


There you go, mundane method to change screen brightness.

Cheers


Refer

1. [https://wiki.archlinux.org/index.php/backlight](https://wiki.archlinux.org/index.php/backlight)
