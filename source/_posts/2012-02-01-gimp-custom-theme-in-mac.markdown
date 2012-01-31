---
layout: post
title: "GIMP custom theme in Mac"
date: 2012-02-01 01:25
comments: true
categories: 
- Mac
- Gimp
---

### Add new theme:

Themes can be downloaded at: [Gnome themes](http://art.gnome.org/themes/gtk2/?page=1)

Suppose downloaded a theme file: `Cillop-Midnite.zip`, then __renamed__ the subfolder(`gtk-2.0`) to `Cillop-Midnite` like this:

    sudo mv Cillop-Midnite/gtk-2.0 /opt/local/share/gimp/2.0/themes/Cillop-Midnite

`gtkrc` is the important file:

    - Cillop-Midnite(renamed, it was "gtk-2.0")
    -- gtkrc
    -- someImage.png
    -- ...

### Change theme:

After copied files to `.../gimp/2.0/themes/`, run `GIMP` & set the theme: `Edit` -> `Preferences` -> `Theme`, choose the theme.
