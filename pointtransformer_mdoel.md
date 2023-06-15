# Point Transformer MindSpore

This repo is a MindSpore implementation for Point-Transformer[Zhao et al](https://openaccess.thecvf.com/content/ICCV2021/papers/Zhao_Point_Transformer_ICCV_2021_paper.pdf), including classification tasks on ModelNet40 and part segmentation tasks on ShapeNet.

 ***Due to the lack of official codes in this paper, this repo is improved based on unofficial codes [qq456cvb, Point-Transformer](https://github.com/qq456cvb/Point-Transformers), and the evaluation indicators are slightly different from those in the paper.***
## requirements

```
python = 3.8
MindSpore = 1.7
numpy
tqdm
yaml
argparse
os
sys
```

## Dataset introduction and download 

The datasets used in this model are ModelNet40 and ShapeNet. 

ModelNet40 includes 40 categories, and the download address is this <a href="https://shapenet.cs.stanford.edu/media/modelnet40_normal_resampled.zip">link</a>.
The ModelNet40 structure is shown below.
 
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

The ShapeNet dataset contains 16 categories, which are further divided into 50 widgets, and the download address is this <a href="https://shapenet.cs.stanford.edu/media/shapenetcore_partanno_segmentation_benchmark_v0_normal.zip">link</a>.
The ShapeNet structure is shown below.
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

## Classification 

Download dataset ModelNet40, and modify path and config in 
```shell
./configs/pointtransformer/pointtransformercls.yaml
```
### Train

```shell

#PointTransformer classfication_modelnet40

cd mind3d/

python tools/classification/train.py  -opt ./configs/pointtransformer/pointtransformercls.yaml
```

### Eval

```shell

# PointTransformer classfication_modelnet40

cd mind3d/

python tools/classification/eval.py  -opt ./configs/pointtransformer/pointtransformercls.yaml
```


### Infer
```shell

# PointTransformer classfication_modelnet40

cd mind3d/

python tools/classification/infer.py  -opt ./configs/pointtransformer/pointtransformercls.yaml
```

### Export

```shell

# PointTransformer classfication_modelnet40

cd mind3d/

python tools/classification/export.py  -opt ./configs/pointtransformer/pointtransformercls.yaml
```

### Result
|model|Acc|
|----------------------|------------|
| PointTransformerCls (paper) | 93.7|
| PointTransformerCls (unoffice code) | 91.7|
|PointTransformerCls (our)|91.7|


## Part Segmentation

Download ShapeNet, modify path and config in 
```shell
./configs/pointtransformer/pointtransformercls.yaml
```


### Train
```shell
# PointTransformer Segmentation_ShapeNet

cd mind3d/

python tools/segmentation/shapenetpart/train.py  -opt ./configs/pointtransformer/pointtransformerseg.yaml
```


### Eval

```shell
# PointTransformer Segmentation_ShapeNet

cd mind3d/ 

python tools/segmentation/shapenetpart/eval.py  -opt ./configs/pointtransformer/pointtransformerseg.yaml
```



### Infer

```shell
# PointTransformer Segmentation_ShapeNet

cd mind3d/ 

python tools/segmentation/shapenetpart/infer.py  -opt ./configs/pointtransformer/pointtransformerseg.yaml
```



### export

```shell
# PointTransformer Segmentation_ShapeNet

cd mind3d/

python tools/segmentation/shapenetpart/export.py  -opt ./configs/pointtransformer/pointtransformerseg.yaml
```


### Result
|model|Ins. mIou|
|----------------------|------------|
| PointTransformerSeg (paper) | 86.6|
| PointTransformerSeg (unoffical code) | 83.5|
| PointTransformerSeg (our)| 84.6 |
## Acknowledgements


Our implementation is mainly based on the following codebases. 
We gratefully thank the authors for their wonderful works.
[qq456cvb, Point-Transformer](https://github.com/qq456cvb/Point-Transformers); 
[HelloMaroon, Point-Transformer-classification](https://github.com/HelloMaroon/Point-Transformer-classification); 
[pierrefdz,point-transformer](https://github.com/pierrefdz/point-transformer)