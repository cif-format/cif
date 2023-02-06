# CIF Specfication

### Table Of Contents
- [CIF Specfication](#cif-specfication)
    - [Table Of Contents](#table-of-contents)
  - [Header](#header)
    - [Magic Numbers](#magic-numbers)
    - [Dimensions of File](#dimensions-of-file)
    - [Header Table](#header-table)
  - [Plotting Pixels](#plotting-pixels)
  - [Example File](#example-file)


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

### Header Table
|Offset in bytes|Description|Default Value (if applicable)|
|-|-|-|
|`0`|Magic Numbers|See [the magic numbers](#magic-numbers) for details|
|`2`|Dimensions|N/A


## Plotting Pixels

## Example File