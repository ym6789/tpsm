首先，先祈求自己一次性部署成功！(但是往往事与愿违，在部署过程中，一大堆的环境及以来程序的安装，能让你疯到姥姥家，不信你跟着我一起试试）
#本部署参考：
https://github.com/natlamir/tpsm
https://github.com/yoyo-nb/Thin-Plate-Spline-Motion-Model

#实践步骤：
1.懂得上网：如果不懂上网，你会更加的抓狂，因为你的大量依赖库，都是会被告知无法下载，哈哈哈哈~~~，当然，能原生看到本文件的人，应该都懂得上网了吧
2.硬件基础：需要有一张N系列显卡，本人用于测试的是RTX3060 12G的显卡
3.驱动软件依赖：安装显卡驱动和工具包：CUDA，自定在 https://www.nvidia.cn/Download/Find.aspx?lang=cn 根据实际下载安装
4.多虚拟环境配置管理工具Anaconda3：用户Anaconda(conda命令)来创建一个虚拟环境，可以给这个虚拟环境命名，切换到该虚拟环境后，然后在虚拟环境安装所有的程序以及对应的依赖，在运行的过程中，就会自然引用该虚拟环境下的变量、命令和配置，完美解决一台系统下可以多个不同环境的目标；


Anaconda3，具有一台系统搭建多个不懂运行环境的需求，比如你电脑里原来运行python2的程序，现在需要安装python3.9来运行本程序，那么你在不懂conda管理的时候，第一想法是吧python2给升级为python3.9,然后你可能要抓狂的是，当你安装完成python3.9后，发现原来python2的程序，都无法正常运行了，然后你又继续把python3.9给卸载重新安装python2,然后你就没有然后，然后你就想放弃本次安装，有种日了dog的感觉吧
不过没有关系，只要你稍微了解下Anaconda,就能解决你要使用python3.9的目标了；




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
