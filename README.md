**首先，**先祈求自己一次性部署成功！(但是往往事与愿违，在部署过程中，一大堆的环境及以来程序的安装，能让你疯到姥姥家，不信你跟着我一起试试）
```
我没有写过github.com的说明规范，看起来很不规则也是正常的，慢慢适应就可以了
```



#本部署参考：

### https://github.com/natlamir/tpsm

### https://github.com/yoyo-nb/Thin-Plate-Spline-Motion-Model


### windows 10系统 专业版 实践步骤：**
  ### 1.懂得上网：如果不懂上网，你会更加的抓狂，因为你的大量依赖库，都是会被告知无法下载，哈哈哈哈~~~，当然，能原生看到本文件的人，应该都懂得上网了吧

  ### 2.硬件基础：需要有一张N系列显卡，本人用于测试的是RTX3060 12G的显卡

  ### 3.驱动软件依赖：安装显卡驱动和工具包：CUDA，自定在 https://www.nvidia.cn/Download/Find.aspx?lang=cn 根据实际下载安装

  ### 4.多虚拟环境配置管理工具Anaconda3：用户Anaconda(conda命令)来创建一个虚拟环境，可以给这个虚拟环境命名，切换到该虚拟环境后，然后在虚拟环境安装所有的程序以及对应的依赖，在运行的过程中，就会自然引用该虚拟环境下的变量、命令和配置，完美解决一台系统下可以多个不同环境的目标；


  tips:Anaconda3，具有一台系统搭建多个不懂运行环境的需求，比如你电脑里原来运行python2的程序，现在需要安装python3.9来运行本程序，那么你在不懂conda管理的时候，第一想法是吧python2给升级为python3.9,然后你可能要抓狂的是，当你安装完成python3.9后，发现原来python2的程序，都无法正常运行了，然后你又继续把python3.9给卸载重新安装python2,然后你就没有然后，然后你就想放弃本次安装，有种日了dog的感觉吧
不过没有关系，只要你稍微了解下Anaconda,就能解决你要使用python3.9的目标了；

### 安装步骤：（最好不要安装在C盘，安装程序尽量不要又空格的目录）
1.安装Anaconda3，自行去官网下载安装，然后可以菜单通过它的powerShell Prompt，也可以直接cmd，然后cd到你需要安装该程序的目录下，我的是H:\AI目录
2.创建环境
```
#创建虚拟环境
conda create --name tpsm python=3.9 -y
#切换到虚拟环境
conda activate tpsm
下载模型程序

git clone https://github.com/ym6789/tpsm.git tpsm
cd tpsm
```

3.安装PyTorch(我也不知道这是啥，反正后面这个是最折腾人的)
 ```
 conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia -y
（这里我也搞不懂，我这边的cuda版本是12.3,也不知道是不是这里出问题了）

安装完成后，我查看下是这样的：
(tpsm) PS H:\AI\tpsm> pip list
Package            Version
------------------ ----------
Brotli             1.0.9
certifi            2023.11.17
cffi               1.16.0
charset-normalizer 2.0.4
cryptography       41.0.7
filelock           3.13.1
gmpy2              2.1.2
idna               3.4
Jinja2             3.1.2
MarkupSafe         2.1.3
mkl-fft            1.3.8
mkl-random         1.2.4
mkl-service        2.4.0
mpmath             1.3.0
networkx           3.1
numpy              1.26.3
Pillow             10.0.1
pip                23.3.1
pycparser          2.21
pyOpenSSL          23.2.0
PySocks            1.7.1
PyYAML             6.0.1
requests           2.31.0
setuptools         68.2.2
sympy              1.12
torch              2.1.2
torchaudio         2.1.2
torchvision        0.16.2
typing_extensions  4.9.0
urllib3            1.26.18
wheel              0.41.2
win-inet-pton      1.1.0




安装requirements.txt文件的依赖组件
(tpsm) PS H:\AI\tpsm> pip install -r requirements.txt

(tpsm) PS H:\AI\tpsm> pip list
Package            Version
------------------ ----------
Brotli             1.0.9
certifi            2023.11.17
cffi               1.14.6
charset-normalizer 2.0.4
colorama           0.4.6
cryptography       41.0.7
cycler             0.10.0
decorator          5.1.0
face-alignment     1.3.5
filelock           3.13.1
fsspec             2023.12.2
gmpy2              2.1.2
idna               3.4
imageio            2.9.0
imageio-ffmpeg     0.4.5
Jinja2             3.1.2
joblib             1.3.2
kiwisolver         1.3.2
llvmlite           0.39.1
MarkupSafe         2.1.3
matplotlib         3.4.3
mkl-fft            1.3.8
mkl-random         1.2.4
mkl-service        2.4.0
mpmath             1.3.0
networkx           2.6.3
numba              0.56.4
numpy              1.20.3
opencv-python      4.9.0.80
pandas             1.3.3
Pillow             9.2.0
pip                23.3.1
pycparser          2.20
pyOpenSSL          23.2.0
pyparsing          2.4.7
PySocks            1.7.1
python-dateutil    2.8.2
pytz               2021.1
PyWavelets         1.1.1
PyYAML             5.4.1
requests           2.31.0
scikit-image       0.18.3
scikit-learn       1.0
scipy              1.7.1
setuptools         68.2.2
six                1.16.0
sympy              1.12
threadpoolctl      3.2.0
tifffile           2023.12.9
torch              2.1.2
torchaudio         2.1.2
torchvision        0.16.2
tqdm               4.62.3
typing_extensions  4.9.0
urllib3            1.26.18
wheel              0.41.2
win-inet-pton      1.1.0
(tpsm) PS H:\AI\tpsm>




```
# 测试pytorch安装是否成功：
```
import torch

print(torch.__version__)

输出：2.1.2（这个版本后续可能会又一大堆的报错，那也没关系，先继续实施看）

```

### 下载模型数据集 Datasets
tips:具体每一个数据集主要偏向与那个领域，未研究

1) **MGif**. Follow [Monkey-Net](https://github.com/AliaksandrSiarohin/monkey-net).

2) **TaiChiHD** and **VoxCeleb**. Follow instructions from [video-preprocessing](https://github.com/AliaksandrSiarohin/video-preprocessing). 

3) **TED-talks**. Follow instructions from [MRAA](https://github.com/snap-research/articulated-animation).

Here are **VoxCeleb**, **TaiChiHD** and **TED-talks**  pre-processed datasets used in the paper. [Baidu Yun](https://pan.baidu.com/s/1HKJOtXBIiP_tlLiFbzn3oA?pwd=x7xv)
Download all files under the folder, then merge the files and decompress, for example:
```bash

cat vox.tar.* > vox.tar
tar xvf vox.tar

下载后，把文件解压到H:\AI\tpsm\checkpoints

(tpsm) PS H:\AI\tpsm\checkpoints> dir
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         2024/1/12     20:26     1359827700 drive-download-20240112T122126Z-001.zip
------          2022/5/2     16:27      306156401 mgif.pth.tar
------          2022/5/2     16:27      350993469 taichi.pth.tar
------          2022/5/2     16:27      350993469 ted.pth.tar
------          2023/7/8      2:04         667037 Thin-Plate-Spline-Motion-Model.ipynb
------          2022/5/2     16:27      350993469 vox.pth.tar


```
# 素材准备：找一个某人的一寸头像照片(png)，放在assets文件夹下，替换source.png文件

# 开始执行命令：（到这里后，应该会觉得报错，这个是安装大量的github项目告诉我的经验，虽然还没有执行）
```
python demo.py --config config/vox-256.yaml --checkpoint checkpoints/vox.pth.tar --source_image assets/source.png --driving_video assets/driving.mp4
```

```
H:\AI\Anaconda3\envs\tpsm\python.exe: can't open file 'H:\AI\tpsm\checkpoints\demo.py': [Errno 2] No such file or directory
(tpsm) PS H:\AI\tpsm\checkpoints> cd ..
(tpsm) PS H:\AI\tpsm> python demo.py --config config/vox-256.yaml --checkpoint checkpoints/vox.pth.tar --source_image assets/source.png --driving_video assets/driving.mp4
H:\AI\Anaconda3\envs\tpsm\lib\site-packages\torchvision\models\_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
  warnings.warn(
H:\AI\Anaconda3\envs\tpsm\lib\site-packages\torchvision\models\_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=None`.
  warnings.warn(msg)
H:\AI\Anaconda3\envs\tpsm\lib\site-packages\torch\functional.py:504: UserWarning: torch.meshgrid: in an upcoming release, it will be required to pass the indexing argument. (Triggered internally at C:\cb\pytorch_1000000000000\work\aten\src\ATen\native\TensorShape.cpp:3527.)
  return _VF.meshgrid(tensors, **kwargs)  # type: ignore[attr-defined]
  0%|                                                                                                                                                                                                               | 0/169 [00:00<?, ?it/s]AttributeError: 'NoneType' object has no attribute 'close'
Exception ignored in: 'scipy.spatial.qhull._Qhull.__dealloc__'
Traceback (most recent call last):
  File "H:\AI\tpsm\demo.py", line 25, in relative_kp
    source_area = ConvexHull(kp_source['fg_kp'][0].data.cpu().numpy()).volume
AttributeError: 'NoneType' object has no attribute 'close'
  0%|                                                                                                                                                                                                               | 0/169 [00:00<?, ?it/s]
Traceback (most recent call last):
  File "H:\AI\tpsm\demo.py", line 179, in <module>
    predictions = make_animation(source_image, driving_video, inpainting, kp_detector, dense_motion_network, avd_network, device = device, mode = opt.mode)
  File "H:\AI\tpsm\demo.py", line 86, in make_animation
    kp_norm = relative_kp(kp_source=kp_source, kp_driving=kp_driving,
  File "H:\AI\tpsm\demo.py", line 25, in relative_kp
    source_area = ConvexHull(kp_source['fg_kp'][0].data.cpu().numpy()).volume
  File "qhull.pyx", line 2434, in scipy.spatial.qhull.ConvexHull.__init__
  File "qhull.pyx", line 269, in scipy.spatial.qhull._Qhull.__init__
  File "messagestream.pyx", line 36, in scipy._lib.messagestream.MessageStream.__init__
OSError: Failed to open file b'C:\\Users\\\xe5\x8d\x8e\xe5\xb8\x88\xe7\xa7\x91\xe6\x95\x99\\AppData\\Local\\Temp\\scipy-hh_y9mwf'

(tpsm) PS H:\AI\tpsm>
查询了下，然后告知说因为有中文路径，修改了环境变量中的temp，所以参考链接https://blog.csdn.net/datao3022/article/details/109186403
右键点击计算机 -> 属性 -> 高级系统设置 -> 环境变量

关闭命令窗口重启（如果不行，就重启电脑再试试）
```
```
继续执行：
conda activate tpsm
python demo.py --config config/vox-256.yaml --checkpoint checkpoints/vox.pth.tar --source_image assets/source.png --driving_video assets/driving.mp4

H:\AI\Anaconda3\envs\tpsm\lib\site-packages\torchvision\models\_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
  warnings.warn(
H:\AI\Anaconda3\envs\tpsm\lib\site-packages\torchvision\models\_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=None`.
  warnings.warn(msg)
H:\AI\Anaconda3\envs\tpsm\lib\site-packages\torch\functional.py:504: UserWarning: torch.meshgrid: in an upcoming release, it will be required to pass the indexing argument. (Triggered internally at C:\cb\pytorch_1000000000000\work\aten\src\ATen\native\TensorShape.cpp:3527.)
  return _VF.meshgrid(tensors, **kwargs)  # type: ignore[attr-defined]
100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 169/169 [00:12<00:00, 13.58it/s]


到了这里，执行完成！！！
(tpsm) PS H:\AI\tpsm>
查看路径：‪H:\AI\tpsm\result.mp4 ，这个是新生成的视频
然后打开播放，发现图片是头像是替换了，但是视频的声音没有了
起码来说，程序是执行了，抽空在来执行吧，希望大拿来指定指导，大家一起共同学习学习

为此还特意花了6000刀配置了一台电脑~~~


```






# [CVPR2022] Thin-Plate Spline Motion Model for Image Animation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![stars](https://img.shields.io/github/stars/yoyo-nb/Thin-Plate-Spline-Motion-Model.svg?style=flat)
![GitHub repo size](https://img.shields.io/github/repo-size/yoyo-nb/Thin-Plate-Spline-Motion-Model.svg)

Source code of the CVPR'2022 paper "Thin-Plate Spline Motion Model for Image Animation"

[**Paper**](https://arxiv.org/abs/2203.14367) **|** [**Supp**](https://cloud.tsinghua.edu.cn/f/f7b8573bb5b04583949f/?dl=1)

### Example animation

![vox](assets/vox.gif)
![ted](assets/ted.gif)

**PS**: The paper trains the model for 100 epochs for a fair comparison. You can use more data and train for more epochs to get better performance.


### Web demo for animation
- Integrated into [Huggingface Spaces 🤗](https://huggingface.co/spaces) using [Gradio](https://github.com/gradio-app/gradio). Try out the Web Demo: [![Hugging Face Spaces](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/CVPR/Image-Animation-using-Thin-Plate-Spline-Motion-Model)
- Try the web demo for animation here: [![Replicate](https://replicate.com/yoyo-nb/thin-plate-spline-motion-model/badge)](https://replicate.com/yoyo-nb/thin-plate-spline-motion-model)
- Google Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1DREfdpnaBhqISg0fuQlAAIwyGVn1loH_?usp=sharing)

### Pre-trained models
- ~~[Tsinghua Cloud](https://cloud.tsinghua.edu.cn/d/30ab8765da364fefa101/)~~
- [Yandex](https://disk.yandex.com/d/bWopgbGj1ZUV1w)
- [Google Drive](https://drive.google.com/drive/folders/1pNDo1ODQIb5HVObRtCmubqJikmR7VVLT?usp=sharing)
- [Baidu Yun](https://pan.baidu.com/s/1hnXmDpIbRC6WqE3tF9c5QA?pwd=1234)

### Installation

We support ```python3```.(Recommended version is Python 3.9).
To install the dependencies run:
```bash
pip install -r requirements.txt
```


### YAML configs
 
There are several configuration files one for each `dataset` in the `config` folder named as ```config/dataset_name.yaml```. 

See description of the parameters in the ```config/taichi-256.yaml```.

### Datasets

1) **MGif**. Follow [Monkey-Net](https://github.com/AliaksandrSiarohin/monkey-net).

2) **TaiChiHD** and **VoxCeleb**. Follow instructions from [video-preprocessing](https://github.com/AliaksandrSiarohin/video-preprocessing). 

3) **TED-talks**. Follow instructions from [MRAA](https://github.com/snap-research/articulated-animation).

Here are **VoxCeleb**, **TaiChiHD** and **TED-talks**  pre-processed datasets used in the paper. [Baidu Yun](https://pan.baidu.com/s/1HKJOtXBIiP_tlLiFbzn3oA?pwd=x7xv)
Download all files under the folder, then merge the files and decompress, for example:
```bash
cat vox.tar.* > vox.tar
tar xvf vox.tar
```


### Training
To train a model on specific dataset run:
```
CUDA_VISIBLE_DEVICES=0,1 python run.py --config config/dataset_name.yaml --device_ids 0,1
```
A log folder named after the timestamp will be created. Checkpoints, loss values, reconstruction results will be saved to this folder.


#### Training AVD network
To train a model on specific dataset run:
```
CUDA_VISIBLE_DEVICES=0 python run.py --mode train_avd --checkpoint '{checkpoint_folder}/checkpoint.pth.tar' --config config/dataset_name.yaml
```
Checkpoints, loss values, reconstruction results will be saved to `{checkpoint_folder}`.



### Evaluation on video reconstruction

To evaluate the reconstruction performance run:
```
CUDA_VISIBLE_DEVICES=0 python run.py --mode reconstruction --config config/dataset_name.yaml --checkpoint '{checkpoint_folder}/checkpoint.pth.tar'
```
The `reconstruction` subfolder will be created in `{checkpoint_folder}`.
The generated video will be stored to this folder, also generated videos will be stored in ```png``` subfolder in loss-less '.png' format for evaluation.
To compute metrics, follow instructions from [pose-evaluation](https://github.com/AliaksandrSiarohin/pose-evaluation).


### Image animation demo
- notebook: `demo.ipynb`, edit the config cell and run for image animation.
- python:
```bash
CUDA_VISIBLE_DEVICES=0 python demo.py --config config/vox-256.yaml --checkpoint checkpoints/vox.pth.tar --source_image ./source.jpg --driving_video ./driving.mp4
```

# Acknowledgments
The main code is based upon [FOMM](https://github.com/AliaksandrSiarohin/first-order-model) and [MRAA](https://github.com/snap-research/articulated-animation)

Thanks for the excellent works!

And Thanks to:

- [@chenxwh](https://github.com/chenxwh): Add Web Demo & Docker environment [![Replicate](https://replicate.com/yoyo-nb/thin-plate-spline-motion-model/badge)](https://replicate.com/yoyo-nb/thin-plate-spline-motion-model) 

- [@TalkUHulk](https://github.com/TalkUHulk): The C++/Python demo is provided in [Image-Animation-Turbo-Boost](https://github.com/TalkUHulk/Image-Animation-Turbo-Boost)

- [@AK391](https://github.com/AK391): Add huggingface web demo [![Hugging Face Spaces](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/CVPR/Image-Animation-using-Thin-Plate-Spline-Motion-Model)
