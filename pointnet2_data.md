# PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space (NIPS 2017)

<hr />

## Introduction
### ModelNet40
ModelNet40 dataset is a point cloud classification data set, with 9840 point clouds in training set and 2468 point clouds in test set, totaling 40 categories.

### ScanNet
ScanNet is an RGB-D video dataset containing 2.5 million views in more than 1500 scans, annotated with 3D camera poses, surface reconstructions, and instance-level semantic segmentations.

## Prepare Dataset:
### ModelNet40
You can get our sampled point clouds of ModelNet40 (XYZ and normal from mesh, 10k points per shape) at this link <a href="https://shapenet.cs.stanford.edu/media/modelnet40_normal_resampled.zip">https://shapenet.cs.stanford.edu/media/modelnet40_normal_resampled.zip. 

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

### ScanNet
ScanNet dataset website: <a href="http://www.scan-net.org/">http://www.scan-net.org/

note: If you would like to download the ScanNet data, please fill out an agreement to the ScanNet Terms of Use<a href="http://kaldir.vc.in.tum.de/scannet/ScanNet_TOS.pdf"> http://kaldir.vc.in.tum.de/scannet/ScanNet_TOS.pdf and send it to Scannet-org at <a href="scannet@googlegroups.com"> scannet@googlegroups.com.

```shell
|--./ScanNet/
    |--data
    	|-- scannetv2.txt
    	|-- scannetv2_train.txt
        |-- scannetv2_val.txt
        |-- scannetv2_test.txt
        |-- scannetv2_visualization.txt
    |--preprocessing
    	|-- points
    	|-- scannet_scenes
    	    	|-- scene0000_00.npy
                |-- scene0000_01.npy
                |-- .......
    	|-- collect_scannet_scenes.py
        |-- scannetv2-labels.combined.tsv
    |--scannet           
        |--scene0000_00
            |-- scene0000_00.sens
            |-- scene0000_00_vh_clean.ply
            |-- scene0000_00_vh_clean_2.ply
            |-- scene0000_00_vh_clean_2.0.010000.segs.json            
            |-- scene0000_00.aggregation.json           
            |-- scene0000_00_vh_clean.aggregation.json          
            |-- scene0000_00_vh_clean_2.0.010000.segs.json 
            |-- scene0000_00_vh_clean.segs.json              
            |-- scene0000_00_vh_clean_2.labels.ply             
            |-- scene0000_00_2d-label.zip  
            |-- scene0000_00_2d-instance.zip               
            |-- scene0000_00_2d-label-filt.zip               
            |-- scene0000_00_2d-instance-filt.zip    
        |--scene0000_01     
            |-- .......    
        |-- .......                                                         
        |-- train_test_split
        |-- synsetoffset2category.txt
```

1) Preprocess ScanNet scenes

`Parse the ScanNet data into `*.npy` files and save them in `mind3d/dataset/prepare_data/preprocessing_scannet/scannet_scenes/`

```shell
cd min3d/dataset/preprocessing_scannet
python preprocessing/collect_scannet_scenes.py
python preprocessing/preprocessing_for_mindspore.py
and Copy and paste output into preprocessing/data/scannetv2_train.txt and preprocessing/data/scannetv2_eval.txt
```
2) Sanity check

`Don't forget to visualize the preprocessed scenes to check the consistency`

```shell
python preprocessing/visualize_prep_scene.py --scene_id <scene_id>
```