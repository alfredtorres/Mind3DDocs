# EagerMOT

# Introduction

[[paper]](https://ieeexplore.ieee.org/document/9562072/)

**Title**: EagerMOT: 3D Multi-Object Tracking via Sensor Fusion

**Authors**: Aleksandr Kim, Aljosa sa Osep, Laura Leal-Taixe

**Abstract**: Multi-object tracking (MOT) enables mobile robots to perform well-informed motion planning and navigation by localizing surrounding objects in 3D space and time. Existing methods rely on depth sensors (e.g., LiDAR) to detect and track targets in 3D space, but only up to a limited sensing range due to the sparsity of the signal. On the other hand, cameras provide a dense and rich visual signal that helps to localize even distant objects, but only in the image domain. In this paper, we propose EagerMOT, a simple tracking formulation that eagerly integrates all available object observations from both sensor modalities to obtain a well-informed interpretation of the scene dynamics. Using images, we can identify distant incoming objects, while depth estimates allow for precise trajectory localization as soon as objects are within the depth-sensing range. With EagerMOT, we achieve state-of-the-art results across several MOT tasks on the KITTI and NuScenes datasets.

![1669702079478](image/model/1669702079478.png)

# Quickstart with Mindspore

## Model Hyper-Parameters:

`max_ages(list of int)`: Defaults to `[3, 3].`
`min_hits(list of int)`: Minimal number of hits to be recoginized as a track. Defaults to `[1, 2]`.
`det_scores(list of int)`: 3D detection thresholds. Defaults to `[0, 0].`
`seg_scores(list of float)`: 2D detection thresholds. Defaults to `[0.0, 0.9]`.
`fusion_iou_threshold (list of float) `: Pre-stage fusion thresholds.Defaults to `[0.01, 0.01]`.
`first_matching_method (str) `: Fusion mode. Defaults to `dist_2d_full`.
`thresholds_per_class (list of float)` : First stage threshold. Defaults to `{1: -3.5, 2: -0.3}`.
`max_age_2d (list of int)` : Defaults to `[3, 3]`.
`leftover_matching_thres (float)` : Final stage threshlod. Defaults to `0.3`.

## Running Example

### Inference

You can run the following script for inference:

```
# change dir
cd tools/tracking/eagermot

# infer 0001 on kitti：
python infer.py --dataset /kitti --split /val --sequence 0001

# eval on kitti:
python eval.py --dataset /kitti --split /val
```

### Evaluation
```
# change dir
cd tools/tracking/eagermot

# eval on kitti:
python eval.py --dataset /kitti

# eval on nuscenes：
python eval.py --dataset /nuscenes
```
If you want to modify the 2D and 3D detection sources, you can change source_2d and source_3d in .yaml file.

If you want to modify the algorithm parameters, you can enter `configs/eagermot/param.yaml`.

The following is the completeness of the testing results of the kitti testing source training

pointgnn_ T3 (all available), pointgnn_ T2 (training missing), ad3dmot (all available)

motsfusion_ Rrc (all available), motsfusion_ Trackrcnn (training missing), trackrcnn (training only)

Nuscenes test results currently only provide val and test, and training test results can be made by yourself

On the NuScenes dataset, if you want to evaluate the 3D MOT of train or val, the source code has been evaluated by default. If you want to evaluate the test results, please submit the tracking results. json file to this [website](https://eval.ai/web/challenges/challenge-page/476/overview) to conduct evaluation

On the Kitti dataset, you can use the official [example](https://github.com/JonathonLuiten/TrackEval) to evaluate 2D MOT. If you want to evaluate 3D MOT, you can use this [link](https://github.com/xinshuoweng/AB3DMOT) for evaluation.

# Visualization

We provide visual code for kitti dataset in the following ways:

```
python tools/tracking/eagermot/visualize.py
```

Several paths and visualization parameters are defined in main, and you can modify them as needed. The visualization results are saved in the same directory of the above code by default in **gif** format.

If you want to test the algorithm module, data reading and module, you can use the script or py file in the test folder

```
#change dir
cd test/eagermot_test

#All tests
bash test.sh
```

The following is the completeness of the testing results of the kitti testing source training

pointgnn_ T3 (all available), pointgnn_ T2 (training missing), ad3dmot (all available)

motsfusion_ Rrc (all available), motsfusion_ Trackrcnn (training missing), trackrcnn (training only)

Nuscenes test results currently only provide val and test, and training test results can be made by yourself

For Dataset and Data preparation, see [Data](./eagermot_data)
