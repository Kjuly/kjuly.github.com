---
layout: post
title: "Resize images by Command in Mac"
date: 2012-01-31 21:17
comments: true
categories: 
- Mac
- Cmd
---

Retaining image's aspect ratio:

    sips -Z 1024 example.png

or ignoring aspect ratio, resizing the image to `1024×768`:

    sips -z 768 1024 example.png

`Sips`: Scriptable Image Processing System.

## References:

- [Resizing images using the command line][]


## Reading List:
- [How do you use “sips” at the terminal to resize an image, without upscaling?][]

[Resizing images using the command line]: http://www.ainotenshi.org/818/resizing-images-using-the-command-line

[How do you use “sips” at the terminal to resize an image, without upscaling?]: http://superuser.com/questions/241212/how-do-you-use-sips-at-the-terminal-to-resize-an-image-without-upscaling
