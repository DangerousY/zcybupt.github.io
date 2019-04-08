# RFBNet
代码 [Github](https://github.com/ruinmessi/RFBNet)

论文 [Receptive Field Block Net for Accurate and Fast Object Detection](https://eccv2018.org/openaccess/content_ECCV_2018/papers/Songtao_Liu_Receptive_Field_Block_ECCV_2018_paper.pdf)

## 环境部署
**推荐使用 `Miniconda` 管理 Python 环境**

**修改 `Conda` 源为清华源**

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

**添加清华 `PyTorch` 源**

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
```

**创建环境**

```
conda create -n RFBNet python=3.5
```

**安装`PyTorch`,`CUDA`, `cuDNN`等**

截至2019 年 3 月 13 RFBNet 仅支持 PyTorch 0.4.0

```
conda activate RFBNet	# 激活环境
conda install pytorch=0.4.0 cuda90 cudnn=7.1.2	# cudnn 版本需与 pytorch build 版本一致
conda install cython opencv
```

克隆官方代码

```
git clone https://github.com/ruinmessi/RFBNet.git
```

**编译**

```
cd RFBNet
```

编译前需根据本机 GPU 配置修改 `utils/build.py`, 从 [GPU 算力表](https://developer.nvidia.com/cuda-gpus)中找到相应的 算力, 例如 GPU 为 ` GeForce GTX 1080`, 查表知 `Compute Capability` 为6.1, 故将 `utils/build.py` 131行 `-arch=sm_52`改为`-arch=sm_61`

```
./make.sh	# 编译
```

## 训练



## 评估

