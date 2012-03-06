---
layout: post
title: "Image Batch"
date: 2012-03-06 09:32
comments: true
categories: 
- CML
- Image
---

- Crop one image to same size pieces ([ImageMagick: Tile Cropping, sub-dividing one image into multiple images][]):

        convert target_pic.png  +gravity -crop 32x32  generated_%d.png

    Tip:
    * `generated_%d.png` -> generated\_1.png ... generated\_123.png
    * `generated_%03.png` -> generated\_001.png ... generated\_123.png


### Reference:

- [ImageMagick: Tile Cropping, sub-dividing one image into multiple images][]

[ImageMagick: Tile Cropping, sub-dividing one image into multiple images]: http://www.imagemagick.org/Usage/crop/#crop_tile
