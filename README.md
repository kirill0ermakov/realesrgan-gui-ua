# Real-ESRGAN GUI

[![build](https://github.com/TransparentLC/realesrgan-gui/actions/workflows/build.yml/badge.svg)](https://github.com/TransparentLC/realesrgan-gui/actions/workflows/build.yml)
[![download](https://img.shields.io/github/downloads/TransparentLC/realesrgan-gui/total.svg)](https://github.com/TransparentLC/realesrgan-gui/releases)

实用、美观的图片放大工具 [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) 的图形界面，参考 [waifu2x-caffe](https://github.com/lltcggie/waifu2x-caffe) 设计。

<details>

<summary>README translations</summary>

* [简体中文](https://github.com/TransparentLC/realesrgan-gui/blob/master/README.md)
* [English](https://github.com/TransparentLC/realesrgan-gui/blob/master/README.en-US.md)

</details>

![](https://user-images.githubusercontent.com/47057319/166252452-d3e7dfbd-2e91-4aaa-95bd-0937adb3d00b.png)

## 基本介绍

这个程序是 Real-ESRGAN 的命令行程序 [Real-ESRGAN-ncnn-vulkan](https://github.com/xinntao/Real-ESRGAN-ncnn-vulkan) 的图形界面，使用 Python 和 tkinter 编写，同时支持 Windows、Ubuntu 和 macOS 平台。

快速上手：

* ![Windows 10+](https://img.shields.io/badge/Windows-10+-06b?logo=windows) 在 Release 中下载最新的 `realesrgan-gui-windows-bundled-v*.7z`，解压后打开 `realesrgan-gui.exe` 即可使用。
* ![Ubuntu 20.04+](https://img.shields.io/badge/Ubuntu-20.04+-e52?logo=ubuntu) 在 Release 中下载最新的 `realesrgan-gui-ubuntu-bundled-v*.tar.xz`，解压后打开 `realesrgan-gui` 即可使用。
* ![macOS Big Sur+](https://img.shields.io/badge/macOS-Big%20Sur+-111?logo=apple) 在 Release 中下载最新的 `realesrgan-gui-macos-appbundle-v*.tar.xz`，解压后在终端中执行 `xattr -cr "Real-ESRGAN GUI.app"`，打开 `Real-ESRGAN GUI` 即可使用。

<details>

<summary>其它的运行方式和说明</summary>

* Release 中的 `realesrgan-gui-windows.7z` 和 `realesrgan-gui-ubuntu.tar.xz` 不包含 Real-ESRGAN-ncnn-vulkan 的主程序和模型，请自行在[这里](https://github.com/xinntao/Real-ESRGAN/releases)下载后解压到 GUI 的主程序所在的目录。
* Actions 中上传的是根据最新提交的代码打包的版本（相当于 Nightly），同样不包含 Real-ESRGAN-ncnn-vulkan 的主程序和模型。
* 如果需要从源代码运行，请使用 Python 3.10 或以上版本，执行 `pip install -r requirements.txt` 安装依赖，将 Real-ESRGAN-ncnn-vulkan 解压到项目目录，然后执行 `main.py`。
* 在其它的 Linux 发行版中可能也可以运行本项目，不过我没有进行测试。

</details>

> ⚠️ 由于我没有运行 macOS 的设备，因此可能无法处理和 macOS 相关的使用问题。

## 功能介绍

在原版支持的功能的基础上，增加了以下功能：

* 任意尺寸放大
    * Real-ESRGAN 只能将输入的图片以固定的 2-4x 倍率（和选用的模型有关）放大。
    * 这一功能通过多次调用 Real-ESRGAN 后使用常规缩放算法降采样实现。
    * 例如将 640x360 的图片使用 2x 的模型放大到宽度 1600，实际操作为先放大到 1280x720，再放大到 2560x1440，最后降采样到 1600x900。
    * 默认使用 Lanczos 进行降采样，也可以选择其它算法。
* 对 GIF 的处理
    * 将 GIF 的各个帧拆分出来并记录时长，逐个放大后再进行合并。
* 拖拽支持
    * 将图片文件或目录拖拽到窗口的任意位置上，即可自动将它的路径设定为输入和输出路径。
    * 根据拖拽时选择的放大尺寸计算方式，在输出路径中会自动添加形如 x4、w1280、h1080 的后缀。
* 深色模式界面
    * 使用 [darkdetect](https://github.com/albertosottile/darkdetect) 实现。
    * 在启动时根据系统设定选择使用浅色或深色模式界面，支持在修改系统设定时自动切换。
    * 在 macOS 上不适用（？）
* 多语言支持
    * 界面语言和系统语言（使用 `locale.getdefaultlocale` 获取）一致。
    * 目前支持简繁中文和英语。在缺少某个语言的翻译文本的情况下，默认会回退到英语。
    * **欢迎添加更多语言的翻译，或对现有的翻译进行改进～**（参见 [`i18n.ini`](https://github.com/TransparentLC/realesrgan-gui/blob/master/i18n.ini)）

## 效果对比

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

* waifu2x-caffe 使用 `UpResNet10` 和 `UpPhoto` 模型，降噪等级 3，开启 TTA。
* Real-ESRGAN 使用 `realesrgan-x4plus-anime` 和 `realesrgan-x4plus` 模型，开启 TTA。
* 放大倍率均为 4x。
* 为了减小文件大小，展示的 GIF 进行了有损压缩处理。

## 可能遇到的问题

### 如何选择模型

对于三次元图片建议使用 `realesrgan-x4plus`，对于二次元图片建议使用 `realesrgan-x4plus-anime`。

对于同一系列模型的不同倍率版本，建议选择等于或大于想要将图片放大的倍率的版本。例如在想要将图片放大到 3x 但是只有 x2 和 x4 模型的情况下，应该选择 x4 的模型。

带有 `animevideo` 的几个模型是针对二次元视频使用的，特点是模型文件较小以及处理速度较快（我自己的测试是 `realesrgan-x4plus-anime` 的 1.5x 到 3x 不等）。不过这个 GUI 并不会考虑加入视频处理功能，如果需要放大视频的话可以考虑使用 [VapourSynth 的相关插件](https://github.com/HolyWu/vs-realesrgan)，并且确定你的显卡不会跑到冒烟……

### 拆分大小的作用

对应原版的 `-t tile-size` 参数。“自动设定”已经可以满足日常使用了，但是如果想要自己设定的话，在显存充足的情况下建议使用较大的值，处理速度更快，放大后的图片质量更好，细节更多（虽然可能不太明显）。

将 Real-ESRGAN-ncnn-vulkan 自带的 [256x256 的测试图](https://github.com/xinntao/Real-ESRGAN-ncnn-vulkan/blob/master/images/input2.jpg)使用 `realesrgan-x4plus` 模型在 TTA 模式下放大到 4x，选择不同的拆分大小的效果：[32](https://user-images.githubusercontent.com/47057319/168460056-1aaf420a-c2d0-4bbf-a350-703f69cd947f.png)，[256 或以上](https://user-images.githubusercontent.com/47057319/168460053-0c34296f-a5c7-447c-9f34-e86b6ebc7035.png)。

### TTA 模式的作用

理论上可以稍微提升放大后的图片的质量，但是实际上效果非常不明显，还会使处理时间增加数倍，因此一般情况下没有开启的必要。

我自己选择了几张 1200px 以上的高清二次元图片进行实验：先将原图缩小到 1/4，再使用 `realesrgan-x4plus-anime` 模型在使用或不使用 TTA 的情况下放大 4x，比较放大后图片和原图的 SSIM（范围为 0-1，值越大表示两张图越相似）。结果使用 TTA 的 SSIM 仅比不使用高出 0.002 左右，目视就更看不出差异了。

### 高级设定中的“针对 GIF 的透明色进行额外处理”是什么？

GIF 只支持最多 256 种 RGB 颜色的调色板并设定其中一种颜色为透明色（可选），也就是说不存在半透明的情况。对于存在透明部分的 GIF，这就出现了两个问题：

* 图像的 Alpha 通道只有 0 和 255 两个值，可以用只有黑白两色的图像表示，有严重的锯齿。
* 将 GIF 的每一帧拆出来保存为 PNG、WebP 等格式以后，透明部分在 RGB 通道上的颜色会变得不可预料。例如 GIF 中被设为透明色的颜色原本是 `#FFFFFF`，将帧另存为后可能会变成 `#000000`，虽然只看图片的话并没有区别。

对于使用 Real-ESRGAN 直接放大 GIF 的每一帧的做法（[示例](https://user-images.githubusercontent.com/47057319/170273973-d9743d66-d6df-42c2-8fe8-b123fa6edb98.gif)），上面两个问题的影响是：

* Real-ESRGAN 对 Alpha 通道放大的效果非常不理想，和使用常规缩放算法几乎没有区别，导致放大后的帧周围会出现一圈锯齿比较明显的杂边。
* 杂边的颜色是不可预料的，比如有些情况下是黑色，会显得非常难看。

这个选项就是针对这两个问题而添加的，启用后会添加以下操作：

* 在拆出 GIF 的每一帧时，强制把透明部分的颜色设为白色，这样可以将放大后的 GIF 的杂边颜色固定为白色，比较美观。
* 对于每一帧的 Alpha 通道，先添加半径 3px 的高斯模糊以平滑锯齿，然后应用一个增加对比度的曲线（或者是 LUT）以尽可能减小杂边的影响，再通过仿色算法处理为只有 0 和 255 两个值的黑白图像。

这个选项是实验性的，建议在放大存在透明部分的 GIF 时手动开启，在放大不存在透明部分的 GIF 时关闭。可能是由于这里的实现或 Pillow 对 GIF 的处理存在问题，在开启时处理后者会出现一些奇怪的问题（主要是出现不该出现的透明色以及仿色效果非常差）。也许会有更好的处理方法。

### 高级设定中的“使用有损压缩”和“有损压缩质量”是什么？

开启这个选项以后，如果输出的文件是 JPEG 或 WebP 格式，就可以根据设定的值（0-100 表示从低质量到高质量）控制输出的文件的压缩质量了。如果输入的是文件夹，则放大文件夹中 JPEG 或 WebP 格式的图片时输出的压缩质量也会受这个选项影响。

不开启这个选项的话，输出为 WebP 格式时使用的是无损压缩。

### 配置文件的保存位置

项目目录或打包后的可执行文件所在目录下的 `config.ini`，没有这个文件的情况下会使用默认的配置。在退出程序时会自动保存配置。

如果因为配置文件的问题导致程序不能运行的话，可以先尝试将配置文件删除。

## 借物表

* [Pillow](https://github.com/python-pillow/Pillow)
* [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) 原版工具
* [Sun-Valley-ttk-theme](https://github.com/rdbende/Sun-Valley-ttk-theme) Windows 11 风格的 tkinter 主题，在原版基础上将所有控件的图片打包成了单张 Sprite Sheet，具体操作参见[这里](https://github.com/rdbende/Sun-Valley-ttk-theme/issues/30)
* [TkInterDnD2](https://github.com/pmgagne/tkinterdnd2) Tkinter 的拖拽支持
* [darkdetect](https://github.com/albertosottile/darkdetect) 检测是否正在使用深色模式
* [pyinstaller](https://github.com/pyinstaller/pyinstaller)

## 致谢

* 感谢 [@blacklein](https://github.com/blacklein) 提供在 macOS 下使用这个 GUI 和打包为应用程序的帮助。
