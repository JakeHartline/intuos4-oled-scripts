# Wacom Intuos 4 OLED scripts
This script will convert an image into special format which Linux kernel uses for Intuos 4 OLED screens. There is also helper script for easier setup.

## Dependencies
- `ImageMagick`
- `hexdump` (part of util-linux or busybox)

## Usage
- Create 64x32 png image
- Convert
 ```
 png-to-i4raw image.png output-file
```
- Fix permissions

  By default writing to device files requires elevated privileges. \
  You can ether change those file permissions with `i4oled-helper permissions` or setup udev rules.
- Send it to one of the buttons (0-7)
```
i4oled-helper set 0 output-file
```
  Or you can pipe resulting file into one of the device files manually.


For normal use you would want to save converted images somewhere and integrate the setup into your main tablet script. Sending already converted images should be fastest. That can be useful if you have different layouts, for example.

#### Clear button
```
i4oled-helper clear 0
```

## Brightness
todo




## More detailed explanation
Intuos 4 OLED screen support is in the Linux kernel, but it uses uncommon image format (interweaved, 4 bits per pixel).
The script uses ImageMagick to convert an image to gray format, then shuffles the order of pixels.

There are multiple tools to do this. This one aims to be simple, with least dependencies.
