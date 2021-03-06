**original copyright**
>This project extracts frames from video recorded by iPhone 3Gs 
using the LGPL FFmpeg libraries.

>This software is licensed under the GNU-LGPL version 2.1 or later.

>Copyright 2010 Lajos Kamocsay

>lajos at codza dot com

## Introduction ##

This project is forked from <https://github.com/lajos/iFrameExtractor>.
I update the code for the latest ffmpeg and iOS version. The source code is tested on `Mac OS 10.7.4(Lion)` for `ffmpeg 0.11.1` and `iOS 5.1` with `Xcode 4.3.2`.

## Build steps ##

- Download the code using

`git clone git@github.com:SharpX/sharp_ios_ffmpeg.git`

- Download the latest ffmpeg (0.11.x) using

`git clone git://source.ffmpeg.org/ffmpeg.git`
`git checkout 0.11.2`

- Put the ffmpeg source code into the folder `ffmpeg`

- Copy the perl script `gas-preprocessor.pl` into `/usr/local/bin` folder

- Change directory to your `ffmpeg` folder, select your target platform and follow the scripts below

### Platforms ###

- `armv7` (for iPhone 3GS and devices after 3GS)

##### configure #####

```
#!/bin/tcsh -f

rm -rf compiled/*

./configure \
--cc=/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/gcc \
--as='/usr/local/bin/gas-preprocessor.pl /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/gcc' \
--sysroot=/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS5.1.sdk \
--target-os=darwin \
--arch=arm \
--cpu=cortex-a8 \
--extra-cflags='-arch armv7' \
--extra-ldflags='-arch armv7 -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS5.1.sdk' \
--prefix=compiled/armv7 \
--enable-cross-compile \
--enable-nonfree \
--enable-decoders \
--enable-encoders \
--enable-muxers \
--enable-muxer=mpegts \
--enable-bsf=h264_mp4toannexb \
--enable-protocols \
--enable-static \
--enable-decoder=h264 \
--enable-decoder=svq3 \
--enable-decoder=rawvideo \
--disable-armv5te \
--disable-swscale-alpha \
--disable-doc \
--disable-ffmpeg \
--disable-ffplay \
--disable-ffprobe \
--disable-ffserver \
--disable-asm \
--disable-bzlib \
--disable-gpl \
--disable-shared \
#--disable-mmx \
#--disable-neon \
#--disable-demuxers \
#--disable-parsers \
#--disable-filters \
#--disable-bsfs \
--disable-postproc 
#--disable-debug 

```


### The complied static libraries (*.a) lie in the`ffmpeg/compiled` folder. ####