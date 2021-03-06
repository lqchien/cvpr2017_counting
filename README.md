# Counting Everyday Objects in Everyday Scenes

![](img/seq_new.png?raw=true)

## Introduction

**Counting Everyday Objects in Everyday Scenes**  
Prithvijit Chattopadhyay*, Ramakrishna Vedantam*, Ramprasaath Ramaswamy Selvaraju, Dhruv Batra, Devi Parikh  
[CVPR 2017][3]

This repository contains code for training one-shot and contextual deep counting models mentioned in the CVPR 2017 version of the paper.

## Abstract

We are interested in counting the number of instances of object classes in natural, everyday images. Previous counting approaches tackle the problem in restricted domains such as counting pedestrians in surveillance videos. Counts can also be estimated from outputs of other vision tasks like object detection. In this work, we build dedicated models for counting designed to tackle the large variance in counts, appearances, and scales of objects found in natural scenes. Our approach is inspired by the phenomenon of subitizing – the ability of humans to make quick assessments of counts given a perceptual signal, for small count values. Given a natural scene, we employ a divide and conquer strategy while incorporating context across the scene to adapt the subitizing idea to counting. Our approach offers consistent improvements over numerous baseline approaches for counting on the PASCAL VOC 2007 and COCO datasets. Subsequently, we study how counting can be used to improve object detection. We then show a proof of concept application of our counting methods to the task of Visual Question Answering, by studying the ‘how many?’ questions in the VQA and COCO-QA datasets.


## Instructions

### Install Torch

```shell
git clone https://github.com/torch/distro.git ~/torch --recursive
cd ~/torch; bash install-deps;
./install.sh
source ~/.bashrc
```

### Required Packages
* [torch-hdf5][4]
* [Element-Research/rnn][5]
* [Element-Research/dpnn][6]

### Train Models

* Run the script `train.lua` with appropriate arguments to train models.
* Import forward pass functions from `fprop_utils.lua` and evaluate predictions by importing functions from `eval.lua`

### Feature Extraction, Storage and Use

#### Glance

* Extract and store data from your desired CNN and dataset in `data/feature/your_feat_dir`
* Store features and ground truth counts on a per-image basis in `data/feature/your_feat_dir/<image-name>.h5` under the keys `/data` and `/label` respectively 

#### Associative and Sequential Subitizing

* Based on the descretization; extract and store data from your desired CNN and dataset in `data/feature/your_feat_dir`
* Store features and ground truth counts on a per-image basis in `data/feature/your_feat_dir/<image-name>.h5` under the keys `/data` and `/label` respectively
* Unlike glance, each `<image-name>.h5` should contain features and counts for all the cells based on the discretization used (9 features per-image for discretization 3)
* The image below shows how the cell features for a 3x3 discretization should be ordered:

<p align="center">
  <img src="img/feat_inst.png?raw=true" alt="Feature Demo Image"/>
</p>

The orderings in the above image correspond to the row-indices of the feature and count tensor (with dimensions `[9 x feat_dim]` and `[9 x num_classes]` respectively) stored under the keys `/data` and `/label` respectively. 

### Datasets

* [Count-QA Splits for VQA/COCO-QA][7]

### Model Checkpoints (Trained with ResNet-152 features)

* [Seq-Sub (3) COCO][12]
* [Seq-Sub (3) PASCAL][13]
* [Aso-Sub (3) COCO][8]
* [Aso-Sub (3) PASCAL][9]
* [Glance COCO][10]
* [Glance PASCAL][11]

## Cite this work

If you find this code useful, consider citing our work:

```
@InProceedings{Chattopadhyay_2017_CVPR,
author = {Chattopadhyay, Prithvijit and Vedantam, Ramakrishna and Selvaraju, Ramprasaath R. and Batra, Dhruv and Parikh, Devi},
title = {Counting Everyday Objects in Everyday Scenes},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {July},
year = {2017}
}
```

## Authors

* [Prithvijit Chattopadhyay][2] (prithvijit3@gatech.edu)
* [Ramakrishna Vedantam][1] (vrama@gatech.edu)

## License

BSD

[1]: http://vrama91.github.io/
[2]: http://prithv1.github.io
[3]: http://openaccess.thecvf.com/content_cvpr_2017/papers/Chattopadhyay_Counting_Everyday_Objects_CVPR_2017_paper.pdf
[4]: https://github.com/deepmind/torch-hdf5
[5]: https://github.com/Element-Research/rnn
[6]: https://github.com/Element-Research/dpnn
[7]: https://filebox.ece.vt.edu/~prithv1/datasets/
[8]: https://filebox.ece.vt.edu/~prithv1/checkpoints/aso_sub_resnet-152_coco_3_1hl_500/
[9]: https://filebox.ece.vt.edu/~prithv1/checkpoints/aso_sub_resnet-152_pascal_3_1hl_500/
[10]: https://filebox.ece.vt.edu/~prithv1/checkpoints/glance_resnet-152_coco_1_2hl_250/
[11]: https://filebox.ece.vt.edu/~prithv1/checkpoints/glance_resnet-152_pascal_1_2hl_250/
[12]: https://filebox.ece.vt.edu/~prithv1/checkpoints/seq_sub_resnet-152_coco_3_2hl_500/
[13]: https://filebox.ece.vt.edu/~prithv1/checkpoints/seq_sub_resnet-152_pascal_3_2hl_500/