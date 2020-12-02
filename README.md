# Ovulation_prediction
For 597SD Class

You need to have the image inside the same folder when you run

#seek-thermal

**NOTE: The library does not support absolute temperature readings since we don't know how.**

## Credits

The code is based on ideas from the following repo's:
* https://github.com/BjornVT/Masterproef.git
* https://github.com/zougloub/libseek
* https://github.com/OpenThermal/libseek-thermal.git

## Build

Dependencies:
* cmake
* libopencv-dev (>= 2.4)
* libusb-1.0-0-dev

## Getting USB access

You need to add a udev rule to be able to run the program as non root user:

Udev rule:

```
SUBSYSTEM=="usb", ATTRS{idVendor}=="289d", ATTRS{idProduct}=="XXXX", MODE="0666", GROUP="users"
```

Replace 'XXXX' with:
* 0010: Seek Thermal Compact/CompactXR
* 0011: Seek Thermal CompactPRO

or manually chmod the device file after plugging the usb cable:

```
sudo chmod 666 /dev/bus/usb/00x/00x
```

with '00x' the usb bus found with the lsusb command


### seek_viewer
seek_viewer is bare bones UI for the seek thermal devices. It can display video on screen, record it to a file, or stream it to a v4l2 loopback device for integration with image processing pipelines. It supports image rotation, scaling, and color mapping using any of the OpenCV color maps. While running `f` will set the display output full screen and `s` will freezeframe.

```
seek_viewer --camtype=seekpro --colormap=11 --rotate=0                          # view color mapped thermal video
seek_viewer --camtype=seekpro --colormap=11 --mode=file --output=seek.avi       # record color mapped thermal video
seek_viewer --camtype=seekpro --colormap=11 --mode=v4l2 --output=/dev/video0    # stream the thermal video to v4l2 device
```

# when using the Seek Thermal compact
```
seek_test flat_field.png
seek_viewer -t seek -F flat_field.png
```
