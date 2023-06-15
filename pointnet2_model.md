# PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space (NIPS 2017)

<hr />

## Introduction

pointnnert++ is based on NIPS'17 paper. You can find arXiv version of the paper <a href="https://arxiv.org/pdf/1706.02413.pdf">here</a> or check <a href="http://stanford.edu/~rqi/pointnet2">project webpage</a> for a quick overview. PointNet++ is a follow-up project that builds on and extends <a href="https://github.com/charlesq34/pointnet">PointNet</a>. It is version 2.0 of the PointNet architecture.

PointNet (the v1 model) either transforms features of *individual points* independently or process global features of the *entire point set*. However, in many cases there are well defined distance metrics such as Euclidean distance for 3D point clouds collected by 3D sensors or geodesic distance for manifolds like isometric shape surfaces. In PointNet++ authors want to respect *spatial localities* of those point sets. PointNet++ learns hierarchical features with increasing scales of contexts, just like that in convolutional neural networks. Besides, authors also observe one challenge that is not present in convnets (with images) -- non-uniform densities in natural point clouds. To deal with those non-uniform densities, we further propose special layers that are able to intelligently aggregate information from different scales.



## Create Environment:

- Python 3 (Recommend to use [Anaconda](https://www.anaconda.com/download/#linux))

- NVIDIA GPU + [CUDA](https://developer.nvidia.com/cuda-downloads)

- Python packages:

```shell
pip install -r requirements.txt
```


## Train:

```shell
# PointNet++ classfication
cd mind3d/
python tools/classification/train.py -opt ./configs/pointnet2/pointnet2_modelnet40_cls.yaml

# PointNet++ segmentation_scannet
cd mind3d/
python tools/segmentation/semantic/train.py -opt ./configs/pointnet2/pointnet2_scannet_seg.yaml

```

## Test:

```shell
# PointNet++ classfication
cd mind3d/
python tools/classification/eval.py -opt ./configs/pointnet2/pointnet2_modelnet40_cls.yaml

# PointNet++ segmentation_scannet
cd mind3d/
python tools/segmentation/semantic/eval.py -opt ./configs/pointnet2/pointnet2_scannet_seg.yaml
```

## visualization:

```shell
cd mind3d/
python tools/segmentation/semantic/infer.py -opt ./configs/pointnet2/pointnet2_scannet_seg.yaml
(you can change the scene ID in ./ScanNet/data/scannetv2_visualization.txt)
```


## Results

### Classfication_Modelnet40

|     Model     |   npoints  | use_norm | Methods  | Accuracy |
|  :--------:   | :--------: |:--------:|:--------:|:--------:|
|   PointNet++  |   1024     |  FALSE   |   SSG    |  0.918   |



### segmengation_scannetv2

|   Model       |       use XYZ     |   use color       |   use normal      | use multiview     |   use MSG         |   mIoU    |
|  :--------:   | :--------:        |:--------:         | :--------:        |:--------:         |:--------:         |:--------: |
|   PointNet++  |:heavy_check_mark: |  -                |  -                |  -                | -                 |   34.0    |




## Citation
If you find the code helpful in your resarch or work, please cite the following paper:

```shell

# PointNet++
@article{qi2017pointnetplusplus,
  title={PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space},
  author={Qi, Charles R and Yi, Li and Su, Hao and Guibas, Leonidas J},
  journal={arXiv preprint arXiv:1706.02413},
  year={2017}
}

```


## Acknowledgement
We thank the authors of [pointnet++](https://github.com/charlesq34/pointnet2) for sharing their codes and data.
We thank the authors of [Pointnet2.ScanNet](https://github.com/daveredrum/Pointnet2.ScanNet) for sharing their codes and data.
