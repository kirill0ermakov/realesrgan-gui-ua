# Real-ESRGAN GUI

[![build](https://github.com/TransparentLC/realesrgan-gui/actions/workflows/build.yml/badge.svg)](https://github.com/TransparentLC/realesrgan-gui/actions/workflows/build.yml)
[![download](https://img.shields.io/github/downloads/TransparentLC/realesrgan-gui/total.svg)](https://github.com/TransparentLC/realesrgan-gui/releases)

A cross-platform GUI for image upscaler [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) with additional features. Inspired by [waifu2x-caffe](https://github.com/lltcggie/waifu2x-caffe).

<details>

<summary>README translations</summary>

* [简体中文](https://github.com/TransparentLC/realesrgan-gui/blob/master/README.md)
* [English](https://github.com/TransparentLC/realesrgan-gui/blob/master/README.en-US.md)

</details>

![](https://user-images.githubusercontent.com/47057319/190863242-a47a3675-fb22-4a1f-96e9-8edb810386be.png)

## Introduction

This application uses Real-ESRGAN's portable executable file ([Real-ESRGAN-ncnn-vulkan](https://github.com/xinntao/Real-ESRGAN-ncnn-vulkan)) to upscale images with extremely high quality. It is written in Python and provides an user-friendly GUI with Tkinter.

Quick Start：

* ![Windows 10+](https://img.shields.io/badge/Windows-10+-06b?logo=windows) Download the latest `realesrgan-gui-windows-bundled-v*.7z` from Release, extract the archive then launch `realesrgan-gui.exe`.
* ![Ubuntu 20.04+](https://img.shields.io/badge/Ubuntu-20.04+-e52?logo=ubuntu) Download the latest `realesrgan-gui-ubuntu-bundled-v*.tar.xz` from Release, extract the archive then launch `realesrgan-gui`.
* ![macOS Big Sur+](https://img.shields.io/badge/macOS-Big%20Sur+-111?logo=apple) Download the latest `realesrgan-gui-macos-appbundle-v*.tar.xz` from Release, extract the archive and run `xattr -cr "Real-ESRGAN GUI.app"` in terminal, then launch `Real-ESRGAN GUI`.

<details>

<summary>Notes</summary>

* Real-ESRGAN-ncnn-vulkan's executable file and models are not contained in  `realesrgan-gui-windows.7z` and `realesrgan-gui-ubuntu.tar.xz`. You have to download manually from [here](https://github.com/xinntao/Real-ESRGAN/releases) and extract them to the directory where Real-ESRGAN GUI's executable file is located.
* The artifacts in GitHub Actions are built based on the latest commits. They don't contain Real-ESRGAN-ncnn-vulkan's executable file and models either.
* Use Python 3.10 or above if you want to run Real-ESRGAN GUI from source. Don't forget to install the dependcies by `pip install -r requirements.txt` and extract Real-ESRGAN-ncnn-vulkan to the repository before running `python main.py`.
* It may be possible to run Real-ESRGAN GUI in other Linux distributions, but I have not tested it.

</details>

> ⚠️ Since I don't have any device running macOS, I may not be able to handle macOS-related issues.

## Features

In addition to the features supported by Real-ESRGAN-ncnn-vulkan, Real-ESRGAN GUI also supports these additional features:

* Upscale to arbitrary size
    * Real-ESRGAN-ncnn-vulkan can only upscale the input image at a fixed 2-4x ratio (depending on the model chosen).
    * Real-ESRGAN GUI uses Real-ESRGAN-ncnn-vulkan to upscale the input image  in multiple times, then downsamples the output image to the desired size  with general image scaling algorithms.
    * For example, to upscale a 640x360 image to 1600 in width with a 2x model, it will be upscaled twice to 1280x720 and 2560x1440 then downsampled to 1600x900.
    * Lanczos is used by default to downsample the image. Other algorithms are also available.
* Upscale GIF images
    * Split animated GIF into frames and reads their duration. Upscale the frames one by one then merge them into upscaled animated GIF image.
* Drag and drop support
    * Drag and drop image files or directories onto the GUI and the input and output path will be set automatically.
    * The output path will contain a suffix like x4, w1280, h1080 based on the chosen resize mode.
* Dark theme
    * Choose to use light or dark theme according to system settings.
    * The detection is done using [darkdetect](https://github.com/albertosottile/darkdetect).
    * Not available on macOS?
* Multi-language support
    * Simplified and traditional Chinese and English are currently supported.
    * Uses `locale.getdefaultlocale` for language detection.
    * Fallback to English by default if translated text is missing.
    * You can add or improve translations by editing [`i18n.ini`](https://github.com/TransparentLC/realesrgan-gui/blob/master/i18n.ini). Contributions are very welcome!

## Samples

| Nearest Neighbor | Lanczos | waifu2x-caffe | Real-ESRGAN |
| --- | --- | --- | --- |
| ![](https://user-images.githubusercontent.com/47057319/166262181-cf1e6c02-a8d2-4d49-88d9-1dfe65107c18.png) | ![](https://user-images.githubusercontent.com/47057319/166262508-32010b72-76b1-4edb-ba8a-f850283873ea.png) | ![](https://user-images.githubusercontent.com/47057319/166262200-a350b33b-9ebb-4159-889c-38d9d5bba386.png) | ![](https://user-images.githubusercontent.com/47057319/166262192-735fb21b-7452-48fe-b99d-ed8233af6d31.png) |

| Nearest Neighbor | Lanczos | waifu2x-caffe | Real-ESRGAN |
| --- | --- | --- | --- |
| ![](https://user-images.githubusercontent.com/47057319/166262217-7623a30d-e4e9-46e4-a869-1dcabdbbd74e.png) | ![](https://user-images.githubusercontent.com/47057319/166262210-a836ed72-b197-4f5f-bcfd-3e459ebf5776.png) | ![](https://user-images.githubusercontent.com/47057319/166262243-810b894d-657d-4a84-84bb-88e76845404f.png) | ![](https://user-images.githubusercontent.com/47057319/166262229-6bc75e4b-9980-4c14-b4e4-4c0d53642a35.png) |

| Nearest Neighbor | Real-ESRGAN |
| --- | --- |
| ![](https://user-images.githubusercontent.com/47057319/168476063-28a142d4-87ef-491e-b50e-6c981236133f.gif) | ![](https://user-images.githubusercontent.com/47057319/168476067-68e76ed6-9589-44f8-ada8-2792dda0ded4.gif) |

| Nearest Neighbor | Real-ESRGAN |
| --- | --- |
| ![](https://user-images.githubusercontent.com/47057319/170270314-dce674be-e1d3-433f-a71f-763983b33e97.gif) | ![](https://user-images.githubusercontent.com/47057319/170273963-4b11551b-44e7-42f8-b0fd-5b2599087a95.gif) |

* waifu2x-caffe samples are upscaled using `UpResNet10` and `UpPhoto` models with noise reduction level 3 and TTA enabled.
* Real-ESRGAN samples are upscaled `using realesrgan-x4plus-anime` and `realesrgan-x4plus` models with TTA enabled.
* The original images are upscaled to 4x.
* The displayed GIFs are lossy compressed to reduce the file size.

## Frequently asked questions

### Which model should I choose?

I recommend `realesrgan-x4plus` for real-life photos and `realesrgan-x4plus-anime` for anime images.

For different upscale ratio versions of the same model, it is recommended to choose the version that is equal to or greater than the ratio at which you want to enlarge the image. For example, if a model has x2 and x4 version and you want to upscale an image by 3x, you should choose the x4 version.

Models with `animevideo` in the filename are designed for anime videos. These models are small and have a faster processing speed (about 1.5-3x compare to `realesrgan-x4plus-anime`). However, I recommend [VapourSynth](https://www.vapoursynth.com/) and its [Real-ESRGAN plugin](https://github.com/HolyWu/vs-realesrgan) if you want to upscale an video. Real-ESRGAN GUI will not consider adding video processing related features.

### The usage of tile size

Corresponding to Real-ESRGAN-ncnn-vulkan's `-t tile-size` param. You can choose "auto" in most cases, or use a larger value if you have enough VRAM. Larger tile size can slightly increase processing speed and the upscaled image's quality, although it may not be obvious.

You can check the difference between the two images upscaled to 4x with tile size [32](https://user-images.githubusercontent.com/47057319/168460056-1aaf420a-c2d0-4bbf-a350-703f69cd947f.png) and [256](https://user-images.githubusercontent.com/47057319/168460053-0c34296f-a5c7-447c-9f34-e86b6ebc7035.png) from the [256x256 test image](https://github.com/xinntao/Real-ESRGAN-ncnn-vulkan/blob/master/images/input2.jpg) comes with Real-ESRGAN-ncnn-vulkan.

### The usage of TTA mode

Slightly improve the quality of upscaled image, but the effect is actually very insignificant. The processing speed will become extremely slow if TTA mode is enabled, so it is not recommended to enable it.

I downloaded some anime images larger than 1200px to conduct an experiment: downsample the image to 1/4 then upscale them with `realesrgan-x4plus-anime` model, measure upscaling quality by SSIM compared with the original image. The TTA-enabled image's SSIM is only about 0.002 higher than TTA-not-enabled image. It is difficult to see the difference with eyes.

### What is "additional processing for GIF with transparency"?

GIFs only support a palette of up to 256 RGB colors and set one of them to be transparent (optional), which means that there is no translucency. For GIFs with transparent parts, this raises two problems.

* The Alpha channel of the image has only two values, 0 and 255, and can be represented by an image with only black and white colors, with severe jaggies.
* The color of the transparent part on the RGB channel becomes unpredictable after each frame of a GIF is split out and saved as a PNG, WebP, etc. For example, the color set as transparent in a GIF is originally #FFFFFF, but after saving the frame it may become #000000, although it makes no difference if you just look at the image.

For upscaling GIF images using Real-ESRGAN directly ([Example](https://user-images.githubusercontent.com/47057319/170273973-d9743d66-d6df-42c2-8fe8-b123fa6edb98.gif)), the impact of the two problems above are:

* The upscaled alpha channel's quality is very poor, resulting in a jagged ring around the scaled frame.
* The color of the jagged ring is unpredictable, for example black in some cases and looks very ugly.

This option was added to resolve these issues. It adds the following actions:

* Force the color of the transparent part to be white when splitting out each frame of the GIF.
* Add a 3px Gaussian blur and apply a contrast curve to smooth out the jagged rings in the alpha channel. Then dither the alpha channel to a black and white image with only 0 and 255 values.

This option is experimental and it is recommended to enable it only when upscaling GIFs with transparency.

### About lossy compression and compression quality

If lossy compression is enabled and the output format is JPEG or WebP, you can control the compression quality of the output image to the set value. If the input is a directory, the output compression quality will also be affected by this option when upscaling JPEG or WebP images in the directory.

If this option is not turned on, lossless compression is used when the output is in WebP format.

### Where the configuration file is saved?

`config.ini` in the repository's directory or in the directory where Real-ESRGAN GUI's executable is located, without this file the default configuration is used.

The configuration will be saved automatically when exiting the program.

## Open-source libraries used

* [Pillow](https://github.com/python-pillow/Pillow)
* [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)
* [Sun-Valley-ttk-theme](https://github.com/rdbende/Sun-Valley-ttk-theme)
* [TkInterDnD2](https://github.com/pmgagne/tkinterdnd2)
* [darkdetect](https://github.com/albertosottile/darkdetect)
* [pyinstaller](https://github.com/pyinstaller/pyinstaller)

## Credits

* Thanks [@blacklein](https://github.com/blacklein) for offering helps on using and bundling this application in macOS.
