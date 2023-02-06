# CIF Specfication

### Table Of Contents
- [CIF Specfication](#cif-specfication)
    - [Table Of Contents](#table-of-contents)
  - [Header](#header)
    - [Magic Numbers](#magic-numbers)
    - [Dimensions of File](#dimensions-of-file)
    - [Header Table](#header-table)
  - [Plotting Pixels](#plotting-pixels)
    - [Irregular dimensions](#irregular-dimensions)
  - [End of File](#end-of-file)
  - [Example Files](#example-files)


## Header

### Magic Numbers
The CIF file begins with magic bytes, which depend on the versioning
of CIF targeted:

| Version| Magic  |
|--------|--------|
|   `v1` |`0xdbfe`|

### Dimensions of File
Next, the dimensions of the CIF file need to be set. Both numbers are 8-bit. For example,
```
00000: db fe ff 20 ff
```
Corresponds to a 255x255 image (`0x20` is used here 
for spacing).

**NOTE**: It is Width X Height, so `2f 20 ff` is 47x255, not 255x47.

### Header Table
|Offset in bytes|Description|Default Value (if applicable)|
|-|-|-|
|`0`|Magic Numbers|See [the magic numbers](#magic-numbers) for details|
|`2`|Dimensions|N/A|


## Plotting Pixels
Each pixel in order corresponds to the pixel on the image. For example, in
this 1x1 image,
```c
0x000: 0xdb 0xfe 0x01 0x20 0x01 0xff 0x00 0x00
```
The first pixel (plotted after `0x01` at offset 6) is a red pixel. The pixels are 32-bit integers in the form of: `0xRRGGBB`.

### Irregular dimensions
If, for example, we have a 2x1 (HxW) image, and we had the same example
as before, except modified:
```c
0x000: 0xdb 0xfe 0x01 0x20 0x02 0xff 0x00 0x00
0x008: 0x20 0xff 0x00 0x00
```
The pixels are seperated by (`0x20`) and if no space is available on the
horizontal axis, they should be plotted at (`0`, `y+1`).

​This applies aswell for 2x1 (WxH).


## End of File
The end of file for CIF files is not signified by EOF, but the sequence
```c
0xff 0xff 0xff 0xff
```
This cannot be treated as a pixel, since there are 4 `0xff`'s, and you
would have one pixel left over, and the spacing would screw up.

## Example Files
See the `example/` directory for examples of common CIF images.