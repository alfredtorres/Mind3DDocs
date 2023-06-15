# PointNet

## Introduction
<a href="https://arxiv.org/abs/1612.00593">paper</a>

**Title:** PointNet:Deep Learning on Point Sets for 3D Classification and Segmentation

**Authors:** Charles R. Qi, Hao Su, Kaichun Mo, Leonidas J. Guibas

**Abstract:** Point cloud is an important type of geometric data structure. Due to its irregular format, most researchers transform such data to regular 3D voxel grids or collections
of images. This, however, renders data unnecessarily voluminous and causes issues. In this paper, we design a novel type of neural network that directly consumes point clouds, which well respects the permutation invariance of
points in the input. Our network, named PointNet, provides a unified architecture for applications ranging from object classification, part segmentation, to scene semantic parsing. Though simple, PointNet is highly efficient and
effective. Empirically, it shows strong performance on par or even better than state of the art. Theoretically, we provide analysis towards understanding of what the network has learnt and why the network is robust with respect to input perturbation and corruption.

## Prepare Dataset:

### ModelNet40
You can get the sampled point clouds of ModelNet40 (XYZ and normal from mesh, 10k points per shape) at this <a href="https://shapenet.cs.stanford.edu/media/modelnet40_normal_resampled.zip">link</a>. 

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
### ShapeNetpart
Download alignment **ShapeNet** [here](https://shapenet.cs.stanford.edu/media/shapenetcore_partanno_segmentation_benchmark_v0_normal.zip)

```shell
|--./shapenetcore_partanno_segmentation_benchmark_v0_normal/
    |--02691156
    	|-- 1a04e3eab45ca15dd86060f189eb133.txt
    	|-- 1a32f10b20170883663e90eaf6b4ca52.txt
        |-- .......
    |--02773838
    |--02954340
    |-- .......
    |--train_test_split
    |--synsetoffset2category.txt
```

## Train

```shell

# PointNet classfication_modelnet40
python tools/classification/train.py  -opt ./configs/pointnet/pointnet_modelnet40_cls.yaml

# PointNet segmentation_shapenetpart
python tools/segmentation/shapenetpart/train.py  -opt ./configs/pointnet/pointnet_shapenetpart_seg.yaml
```

## Eval

```shell

# PointNet classfication_modelnet40
python tools/classification/eval.py  -opt ./configs/pointnet/pointnet_modelnet40_cls.yaml

# PointNet segmentation_shapenetpart
python tools/segmentation/shapenetpart/eval.py  -opt ./configs/pointnet/pointnet_shapenetpart_seg.yaml

```

## Infer

```shell

# PointNet classfication_modelnet40
python tools/classification/infer.py  -opt ./configs/pointnet/pointnet_modelnet40_cls.yaml

# PointNet segmentation_shapenetpart
python tools/segmentation/shapenetpart/infer.py  -opt ./configs/pointnet/pointnet_shapenetpart_seg.yaml

```

## Export

```shell

# export model
# PointNet classfication_modelnet40
python tools/classification/export.py -opt ./configs/pointnet/pointnet_modelnet40_cls.yaml

# PointNet segmentation_shapenetpart
python tools/segmentation/shapenetpart/export.py  -opt ./configs/pointnet/pointnet_shapenetpart_seg.yaml

```
