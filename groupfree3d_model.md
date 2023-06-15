# GroupFree-3D

### Introduction
[<a href="https://arxiv.org/pdf/2104.00678.pdf">paper</a>]

Title: Group-Free 3D Object Detection via Transformers

Authors: Ze Liu, Zheng Zhang, Yue Cao, Han Hu, Xin Tong

Abstract: Recently, directly detecting 3D objects from 3D point clouds has received increasing attention. To extract object representation from an irregular point cloud, existing methods usually take a point grouping step to assign the points to an object candidate so that a PointNet-like network could be used to derive object features from the grouped points. However, the inaccurate point assignments caused by the hand-crafted grouping scheme decrease the performance of 3D object detection.
In this paper, we present a simple yet effective method for directly detecting 3D objects from the 3D point cloud. Instead of grouping local points to each object candidate, our method computes the feature of an object from all the points in the point cloud with the help of an attention mechanism in the Transformers, where the contribution of each point is automatically learned in the network training. With an improved attention stacking scheme, our method fuses object features in different stages and generates more accurate object detection results. With few bells and whistles, the proposed method achieves state-of-the-art 3D object detection performance on two widely used benchmarks, ScanNet V2 and SUN RGB-D.

## Running 

Change the parameter settings in the scannet.yaml file

### Inference

- The following configuration for infer.

  ```shell
  mpirun -n 2 python tools/detection/infer.py -opt 'configs/groupfree_3d/scannet.yaml'
  ```

### Evaluation

- The following configuration for eval.

  ```shell
  mpirun -n 2 python tools/detection/eval.py -opt 'configs/groupfree_3d/scannet.yaml'
  ```
  
### Training

- The following configuration for train.

  ```shell
  mpirun -n 2 python tools/detection/train.py -opt 'configs/groupfree_3d/scannet.yaml'  
  ```


Note that we just provide these hyper parameter ranges for reference only, and we can not guarantee that they are the optimal range of this model.

### Model export

- The following configuration for exporting model.

  ```shell
  python tools/detection/export.py -opt 'configs/groupfree_3d/scannet.yaml'
  ```