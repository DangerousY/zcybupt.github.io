---
layout: post
title:  "Darknet Yolo v3"
date:   2019-03-12 23:15:00 +0800
categories: document
tag: 教程
---

* content
{:toc}

![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png)

# Darknet
Darknet is an open source neural network framework written in C and CUDA. It is fast, easy to install, and supports CPU and GPU computation.

For more information see the [Darknet project website](http://pjreddie.com/darknet).

# 环境部署
**服务器环境信息**

```
OS: Ubuntu 16.04
Kernel: x86_64 Linux 4.13.0-38-generic
CPU: Intel Xeon CPU E5-2620 v3 @ 3.2GHz
GPU: 双路 GeForce GTX 1080
RAM: 32 GB
CUDA: 8.0.61
cuDNN: 7.0.5
GCC: 4.9.4
Python: 3.5
```

 **CUDA 及 cuDNN 环境配置**

```
vi ~/.bashrc
```


追加以下内容:

```
export PATH=/usr/local/cuda-8.0/bin:$PATH
# 服务器环境 cuDNN 配置可能存在问题, 故自行配置如下路径
export LD_LIBRARY_PATH=/path/to/your/cudnn-lib-files:$LD_LIBRARY_PATH
# 例: export LD_LIBRARY_PATH=/server_space/zhaoym/cuda/tmp:$LD_LIBRARY_PATH
```

使配置生效:

```
source ~/.bashrc
```

**编译**

克隆官方代码

```
git clone https://github.com/pjreddie/darknet
```

切换到 darknet 目录, 修改 Makefile

```
cd darknet
vi Makefile
```

> GPU=1
> CUDNN=1
> OPENCV=0 # 若需检测视频等, 则修改为 1, OpenCV 配置方法略
>
> . . . . . . .
>
> COMMON+= -DGPU -I/usr/local/cuda/include/	# 需根据服务器 CUDA 安装路径修改
> CFLAGS+= -DGPU
> LDFLAGS+= -L/usr/local/cuda/lib64 -lcuda -lcudart -lcublas -lcurand	# 需根据 cuDNN 路径修改
>
> 例: 
>
> COMMON+= -DGPU -I/usr/local/cuda-8.0/include/
> LDFLAGS+= -L/server_space/zhaoym/cuda/tmp -lcuda -lcudart -lcublas -lcurand

```
make
```

若编译失败需执行 make clean, 修改后重新 make 即可

**判断是否配置成功**

下载官方预训练权重

```
wget https://pjreddie.com/media/files/yolov3.weights
```

检测测试

```
./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg
```

输出如下

```
layer     filters    size              input                output
    0 conv     32  3 x 3 / 1   416 x 416 x   3   ->   416 x 416 x  32  0.299 BFLOPs
    1 conv     64  3 x 3 / 2   416 x 416 x  32   ->   208 x 208 x  64  1.595 BFLOPs
    .......
  105 conv    255  1 x 1 / 1    52 x  52 x 256   ->    52 x  52 x 255  0.353 BFLOPs
  106 detection
truth_thresh: Using default '1.000000'
Loading weights from yolov3.weights...Done!
data/dog.jpg: Predicted in 0.029329 seconds.
dog: 99%
truck: 93%
bicycle: 99%
```

标注图片在项目根目录下, 名为 `predictions.png`

![Predictions.png](https://pjreddie.com/media/image/Screen_Shot_2018-03-24_at_10.48.42_PM.png)

# 训练



# 评估