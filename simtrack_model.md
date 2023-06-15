# Simtrack

# Introduction

[[Paper]](https://arxiv.org/pdf/2108.10312.pdf)

**Title:** Exploring Simple 3D Multi-Object Tracking for Autonomous Driving

**Authors:** Chenxu Luo, Xiaodong Yang, Alan Yuille

**Abstract:** 3D multi-object tracking in LiDAR point clouds is a key ingredient for self-driving vehicles. Existing methods are predominantly based on the tracking-by-detection pipeline and inevitably require a heuristic matching step for the detection association. In this paper, we present SimTrack to simplify the hand-crafted tracking paradigm by proposing an end-to-end trainable model for joint detection and tracking from raw point clouds. Our key design is to predict the first-appear location of each object in a given snippet to get the tracking identity and then update the location based on motion estimation. In the inference, the heuristic matching step can be completely waived by a simple read-off operation. SimTrack integrates the tracked object association, newborn object detection, and dead track killing in a single unified model. We conduct extensive evaluations on two large-scale datasets: nuScenes and Waymo Open Dataset. Experimental results reveal that our simple approach compares favorably with the state-of-the-art methods while ruling out the heuristic matching rules.

# Quickstart with Mindspore

## Running Example

#Training
python ./tools/tracking/train.py --config ./configs/simtrack/simtrack.yaml

# Test      
python ./tools/tracking/eval.py --config ./configs/simtrack/simtrack.yaml

# infer      
python ./tools/tracking/infer.py --config ./configs/simtrack/simtrack.yaml

# export      
python ./tools/tracking/export.py --config ./configs/simtrack/simtrack.yaml