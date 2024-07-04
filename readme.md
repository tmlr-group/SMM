# Sample-specific Masks for Visual Reprogramming-based Prompting

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) 
[![Static Badge](https://img.shields.io/badge/View-Slides-brightgreen)](https://drive.google.com/file/d/1SUxqoo5Ef0UHJF6vPSjfk_FQ854zei5n/view?usp=sharing)
[![Static Badge](https://img.shields.io/badge/View-Poster-purple)](https://drive.google.com/file/d/1IIiTG6CEu3OzaIBhwnmmn6vtJvq8qJFC/view?usp=sharing)
[![Static Badge](https://img.shields.io/badge/Pub-ICML'24-red)](https://openreview.net/forum?id=4sikyurTLX)


This repository is the official PyTorch implementation of the **ICML2024** paper:
[Sample-specific Masks for Visual Reprogramming-based Prompting](https://arxiv.org/abs/2406.03150),
authored by Chengyi Cai, Zesheng Ye, Lei Feng, Jianzhong Qi, and Feng Liu.

**Key Words:**
Visual Reprogramming, Pre-trained Models, Approximation Error, Machine Learning

**Abstract:**
*Visual reprogramming* (VR) is a prompting technique that aims to re-purpose a pre-trained model (e.g., a classifier on ImageNet) to target tasks (e.g., medical data prediction) by learning a *small-scale pattern* added into input images instead of tuning considerable parameters within the model. 
The location of the pattern within input samples is usually determined by a pre-defined mask *shared across all samples*. 
In this paper, we show that the shared mask potentially limits VR's generalization and increases its approximation error due to the lack of sample-level adaptation.
Motivated by this finding, we design a new framework for VR called *sample-specific multi-channel masks* (SMM). 
Specifically, SMM employs a lightweight ConvNet and patch-wise interpolation to generate sample-specific three-channel masks instead of a shared and pre-defined mask.
Since we generate different masks for individual samples, SMM is theoretically shown to reduce approximation error for the target tasks compared with existing state-of-the-art VR methods. We also empirically demonstrate its performance gain on both ResNet and ViT.
The success of SMM further highlights the broader applicability of VR in leveraging the latent knowledge of pre-trained models for various target tasks.

**Method:**
Comparison between existing methods (a) and our method (b). 
Previous padding-based reprogramming adds zeros around the target image, while resizing-based reprogramming adjusts image dimensions to fit the required input size. 
Both methods use a pre-determined *shared* mask to indicate the valid location of pattern $\delta$. Our method, on the other hand, takes a more dynamic and tailored approach. 
We resize each target image and apply a different three-channel mask accordingly, driven by a lightweight model $f_{\rm mask}$ and an interpolation up-scaling module, allowing for more variability in individual samples.

<p align="center">
  <img src="https://github.com/caichengyi/SMM/blob/main/method.png?raw=true" width=100%/>
</p>


## Dataset
- For CIFAR10, CIFAR100, GTSRB, SVHN, simply run our code and use [TorchVision](https://pytorch.org/vision/0.15/datasets.html) to download them automatically.
- For other datasets, follow [this paper](https://github.com/OPTML-Group/ILM-VP) to prepare them.

Put all the download datasets in `/dataset/`, or modify the `data_path` in `cfg.py`.
## Environment

- Python (3.10.0)
- PyTorch (2.0.1) 
- TorchVision (0.15.2)
        
        pip install -r requirements.txt

## Training

- For CNN-based pretrained model

        python instancewise_vp.py --dataset cifar10 --network resnet18 --seed 0
        python instancewise_vp.py --dataset cifar10 --network resnet50 --seed 0

- For ViT-based pretrained model

        python instancewise_vp.py --dataset cifar10 --network ViT_B32 --seed 0

- Applying SMM to different output label mapping methods
        
        python instancewise_vp.py --dataset cifar10 --mapping_method rlm --seed 0
        python instancewise_vp.py --dataset cifar10 --mapping_method flm --seed 0

## Acknowledgements

This repo is built upon these previous works:

- [lukemelas/PyTorch-Pretrained-ViT](https://github.com/lukemelas/PyTorch-Pretrained-ViT)
- [OPTML-Group/ILM-VP](https://github.com/OPTML-Group/ILM-VP)

## Citation
    
    @inproceedings{cai2024sample,
        title={Sample-specific Masks for Visual Reprogramming-based Prompting},
        author={Chengyi Cai and Zesheng Ye and Lei Feng and Jianzhong Qi and Feng Liu},
        booktitle = {International Conference on Machine Learning (ICML)},
        year={2024}
    }
