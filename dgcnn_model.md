#DGCNN_mindspore
- [DGCNN\_mindspore](#DGCNN_mindspore)
- [Description](#description)
- [Model Architecture](#model-architecture)
- [Dataset](#dataset)
- [Environment Requirements](#environment-requirements)
- [Quick Start](#quick-start)
  - [Dataset Preparation](#dataset-preparation)
  - [Model Checkpoints](#model-checkpoints)
  - [Running](#running)
- [Model Description](#model-description)
  - [Performance](#performance)
    - [DGCNN on ModelNet40 dataset and S3DIS](#i3d-on-kinetics400-dataset-with-detector)
      
#[DGCNN\_mindspore](#contents)
# DGCNN: Dynamic Graph CNN for Learning on Point Clouds (TOG2019)
This repo is a Mindspore implementation for Dynamic Graph CNN for Learning on Point Clouds (DGCNN)(https://arxiv.org/pdf/1801.07829). Our code skeleton is borrowed from WangYueFt/dgcnn.

# [Description](#contents)
> **Abstract:** *author propose a new neural network module dubbed EdgeConv suitable for CNN-based high-level tasks on point clouds including classification and segmentation. EdgeConv is differentiable and can be plugged into existing architectures.* 

## Introduction
DGCNN, another representative work of point cloud feature extraction after Pointnet
Pointnet extracts MLP from the features of each point separately (without feature exchange between points), and finally uses MAXpool to fuse the features of all points together to obtain a 1024 dimensional feature descriptor for the overall point cloud. Therefore, Pointnet can be used as an extractor for the global features of the point cloud
Compared with Pointnet, DGCNN can extract and utilize the local geometric features of point cloud DGCNN uses graph neural network to update and fuse point cloud features step by step, namely Edgeconv
The edge of each point cloud of nodes in DGCNN is determined by the neighborhood defined in the feature space. This is also different from the common graph neural network, that is, dynamic. After each update of node characteristics, the connection relationship between nodes is determined according to the similarity matrix of features
That is to say, the link relationship of the graph is learned by the network itself, so the receptive field of edgconv can reach the maximum diameter of the whole point cloud.

# [Model Architecture](#contents)
## Diagram of DGCNN
![Illustration of DGCNN](./figure/dgcnn.png)

# [Dataset](#contents)
# Classification (ModelNet40)
You can get our sampled point clouds of ModelNet40 (XYZ and normal from mesh, 10k points per shape) at this <a href="https://shapenet.cs.stanford.edu/media/modelnet40_normal_resampled.zip">link</a>. 
```shell
|--./ModelNet40/
    |--airplane
    	|-- airplane_0001.txt
    	|-- airplane_0002.txt
        |-- .......
    |--bathtub
    	|-- bathtub_0001.txt
    	|-- bathtub_0002.txt
        |-- .......
    |--filelist.txt
    |-- modelnet40_shape_names.txt
    |-- modelnet40_test.txt
    |-- modelnet40_train.txt
```

# S3DIS
Download 3D indoor parsing dataset (S3DIS) here and save in data/Stanford3dDataset_v1.2_Aligned_Version/.
```shell
cd mind3d/dataset/
python S3DIS.py
```
Processed data will save in data/stanford_indoor3d/.
```shell
|--./data/
    |--indoor3d_sem_seg_hdf5_data
    	|-- all_files.txt
    	|-- room_filelist.txt
        |-- ply_data_all_1.h5
        |-- ply_data_all_1.h5
        |-- ply_data_all_1.h5
        |--....
    |--indoor3d_sem_seg_hdf5_data_test
    	|-- raw_data3d
    	    |-- Area_1
                |--conferenceRoom_1(0).txt
                |-- .......
    	|-- all_files.txt
        |-- room_filelist.txt
        |-- ply_data_all_0.h5
        |-- ........
    |--Stanford3dDataset_v1.2_Aligned_Version
        |--Aera_1
            |-- ConferenceRoom_1
                |--Annotations
                    |--beam_1.txt
                    |--board_1.txt
                    |--board_2.txt
                |-- conferenceRoom_1.txt
            |-- ConferenceRoom_2
            |-- .......        
        |--Aera_2  
   |--stanford_indoor3d   
        |-- Aera_1_conferenceRoom_1.npy                                                       
        |-- Aera_1_conferenceRoom_2.npy   
        |-- .......  
```

# [Environment Requirements](#contents)
- Framework
  - [MindSpore](https://www.mindspore.cn/install/en)

- Requirements
```text
Python and dependencies
    - Ubuntu 20.04
    - NVIDIA GPU + [CUDA](https://developer.nvidia.com/cuda-downloads)
    - Python 3.7
    - MindSpore 1.8.1
    - Package: h5py, sklearn, plyfile
```

# [Quick Start](#contents)
## [Dataset Preparation](#contents)
1) Preprocess ModelNet40
Download ModelNet40 at this  <a href="https://shapenet.cs.stanford.edu/media/modelnet40_normal_resampled.zip">link</a>. 

2) Preprocess S3DIS
Users need to go to https://goo.gl/forms/4SoGp4KtH1jfRqEj2 Download Standfor3dDataset_ v1.2_ Aligned_ Version.zip, unzip and put into the 'dataset/data'
and use S3DIS.py
```shell
cd mind3d/dataset/
python S3DIS.py
```

## [Model Checkpoints](#contents)
The pretrain model is trained on the the ModelNet40 and S3DIS dataset. It can be downloaded here:链接: https://pan.baidu.com/s/1o99dDIpEUcDoTz41pxrd1Q?pwd=m1sp 提取码: m1sp 

## [Running](#contents)
## Train:
```shell
# DGCNN classfication
cd mind3d
python tools/classification/train.py -opt ./configs/dgcnn/dgcnn_modelnet40_cls.yaml

# DGCNN segmentation
cd mind3d
python tools/segmentation/semantictrain.py -opt ./configs/dgcnn/dgcnn_s3dis_seg.yaml
```
## Test:

```shell
# DGCNN classfication
cd mind3d
python tools/classification/test.py -opt ./configs/dgcnn/dgcnn_modelnet40_cls.yaml

# DGCNN segmentation
cd mind3d
python tools/segmentation/semantic/test.py -opt ./configs/dgcnn/dgcnn_s3dis_seg.yaml
```
## Export:
```shell
# DGCNN classfication
cd mind3d
python tools/classification/export.py -opt ./configs/dgcnn/dgcnn_modelnet40_cls.yaml

# DGCNN segmentation
cd mind3d
python tools/segmentation/semantic/export.py -opt ./configs/dgcnn/dgcnn_s3dis_seg.yaml
```
## Visualization:
```shell
# DGCNN classfication
cd mind3d
python tools/classification/infer.py -opt ./configs/dgcnn/dgcnn_modelnet40_cls.yaml

# DGCNN segmentation
cd mind3d
python tools/segmentation/semantic/infer.py -opt ./configs/dgcnn/dgcnn_s3dis_seg.yaml
```

# [Model Description](#contents)
### Modelnet40
|     Model       | Point number |   ACC  |
| --------------  |  ----------- |  ----- |
|    MindSpore    |     1024     |  0.920 |
| original paper  |     1024     |  0.917 |
### S3DIS
|     Model       |      IOU     |   ACC  |
| --------------  |  ----------- |  ----- |
|    MindSpore    |     56.6     |  0.851 |
| original paper  |     56.1     |  0.841 |
