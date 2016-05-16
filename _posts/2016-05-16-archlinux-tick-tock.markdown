---
published: true
title: ArchLinux - tick tock
layout: post
---
We all need time. And we all feel the need to keep looking at a clock.

For a default installation of arch + openbox, I do not have any clock. For seeing the time, I often have to use date command, or just look for my phone or wallclock.

A simple one liner to fix it.

> xclock -digital -update 1 &

Tadaa.. You have a clock on your screen. Enter `exit` to quit the terminal.

Pro tip : Right click on title bar. Select Un/decorate. You have persistent clock which looks as if it is a part of the background. Beware, it becomes unmoveable.

Pro tip 2 : Use `killall xclock` to remove the clock.

Cheers

