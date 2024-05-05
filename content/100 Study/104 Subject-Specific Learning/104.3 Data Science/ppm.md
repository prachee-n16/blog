---
title: PPM
---
*Short for Portable Pixmap Format, it's a bitmap file i.e. uncompressed raster file* 

The idea behind `.ppm` files are making the task of sharing between formats easier. If we have `n` image formats, to convert from any format to another, we would need to devise `n x n` ways to cover all grounds. A more optimized solution is converting all `n` image formats into `.ppm` files and vice-versa. This allows for `2 x n` programs to convert from one image format to another.

Here's an example of a PPM image:
```
P3
3 2
255
255 0   0    0   255 0      0 0 255
255 255 0    255 255 255    0 0 0
```

So, the magic number is either "P1", "P2", "P3", "P4", "P5", or "P6". It varies based on how it's stored.
- P1 and P4 indicate it's a bitmap
- P2 and P5 indicate greyscale images
- P3 and P6 indicate full color PPM
- P1 - P3 indicate image data in ASCII characters, compatible with text editors
- P4 - P6 indicate binary encoding

In the header, we determine the image width and image height (3 x 2 pixels). Also, we state the maximum color value cannot exceed 255 but will be less. Finally, in this uncompressed version, we state the ASCII color code for all 3x2=6 pixels. 

Related: [[../104.2 Programming/imageFormats|Image Formats and Compression Comparision]]
