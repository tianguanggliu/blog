---
title: openseadragon
title_cn: openseadragon副本
keywords: openseadragonKeywo0rd教程
date: 2018-10-18 17:21:29
tags:
    - H5
    - 移动端
categories: HTML5
description: openseadragon教程
img: http://pgtoq1cmw.bkt.clouddn.com/blog/imgbanner.jpg
---
###### 项目介绍：H5页面，实现长按按钮图片（清明上河图）自动播放 . . .
> [openseadragon](https://github.com/openseadragon/openseadragon "openseadragon") 基于Web的开源查看器，用于高分辨率可缩放图像，以纯JavaScript实现，适用于桌面和移动设备。

### 技术背景

图片大部分都是压缩过的，大部分为JPEG PNG BMP其中BMP格式是点阵形式，当图片翻译到内存之后无论压没压缩过都会变成BMP格式放进内存，在这个过程中，图片数据会几倍的增大，就比如JPEG，一张1M大小的JPEG格式的图片，翻译到内存可能就会变成7倍左右，也就是7M会放在电脑内存里面，如果显示一张100M的JPEG图片，放进内存的话可能就会成为1G，好了如果是1G的图片呢，你的电脑内存还够用吗，再如果在手机端显示呢？ **最后找到两个js库来实现项目需求 [Leaflet](https://github.com/Leaflet/Leaflet) 和 [openseadragon](https://github.com/openseadragon/openseadragon)**

### 技术实现

##### 一、库文件下载
首先进入[官网](http://openseadragon.github.io/)或[GitHub](https://github.com/openseadragon/openseadragon)下载工程中我们只需要用到openseadragon.min.js库

##### 二、准备图片
OpenSeadragon支持很多图片协议和格式，通常这些图片都是由很多图片的切片组成的，例如一张很大的图，需要剪裁成很多小图，按照一定的命名和存储规则存放。官网为我们提供了许多切图[工具](http://openseadragon.github.io/examples/creating-zooming-images/) 根据需要可以根据编程或客户端来实现，我选取的是[Deep Zoom Composer](https://download.microsoft.com/download/4/D/5/4D55442C-D183-4F0F-9163-AD31A09BDFC1/Deep%20Zoom%20Composer.msi)（点击可直接下载）
安装完成后打开软件新建一个工程，把大图片拖进去，显示如下图
<img src="http://pgtoq1cmw.bkt.clouddn.com/blog/imgdeep-zoom-composer.jpg" width="50%" hegiht="50%" align=center alt="新工程" />

点击Export，Output Type选择imags，随便起个名字例如bingImg，Export options选择Export as a collection，点击Export即可在相应路径生成文件。如下图，标注部分请注意
<img src="http://pgtoq1cmw.bkt.clouddn.com/blog/imgexport.jpg" width="50%" hegiht="50%" align=center alt="导出页面" />
找到导出后的文件dzc_output_images下的就是我们需要的文件，xml中有代码需要用到的数据，_files文件夹就是所有图片文件。*XML如下:*
```html
  <Image TileSize="256" Overlap="1" Format="jpg" ServerFormat="Default" xmlns="http://schemas.microsoft.com/deepzoom/2009">
  <Size Width="1920" Height="1080" /></Image>
```
##### 三、代码
直接上代码，查看[完整代码](https://github.com/tianguanggliu/H5demo/tree/master/openseadragon)，查看[效果](https://blog.emper.cn/cases/openseadragon.html)
```javascript
    function openMap() {
        openSeadragonInstance = OpenSeadragon({
        minZoomLevel: defaultZoomLevel,     // 最小缩放等级
        animationTime: 0.3,
        visibilityRatio: 1.0,
        maxZoomLevel: 16,
        constrainDuringPan: true,
        showNavigator: false,               // 显示导航
        showZoomControl: false,             // 则显示+和 - 按钮以放大和缩小。
        showHomeControl: false,             // 显示主页
        showFullPageControl: false,         // 显示全屏
        iOSDevice: !isAndroid(),
        immediateRender: true,              // 提供非常模糊到锐利的效果。建议将移动设备的设置更改为true。
        defaultZoomLevel: defaultZoomLevel, // 首次打开图像或单击主页按钮时使用的缩放级别。如果为0，则调整以适合查看者。
        useCanvas: true,                    // 设置为false，即使支持canvas，也不使用HTML canvas元素进行图像渲染。 安卓关闭 ios 开启
        id: 'openSeadragon',
        prefixUrl: './images/',
        preserveImageSizeOnResize: true,
        minPixelRatio: 1,
        tileSources: {
            Image: {
                xmlns: 'http://schemas.microsoft.com/deepzoom/2009', // 在xml中可以找到
                Url: './ios_files/',                                 // 文件夹
                Overlap: '1',
                TileSize: '256',                                    // 在xml中可以找到
                Format: 'jpg',                                      // 在xml中可以找到
                Size: {
                    Height: '46756',
                    Width: '2071'
                }

            }

        }

    });
}

```
    
