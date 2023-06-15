# Dataset Descrption

Kitti Dataset: [Link](https://www.cvlibs.net/datasets/kitti/raw_data.php)

* Dataset Size：about 50G
* Training split：21 sequences
* Testing split：29 sequences
* Data format：.bin and .jpg

  ![1669703400198](image/data/1669703400198.png)


NuScenes Dataset: [Link](https://www.nuscenes.org/nuscenes)

* Dataset Size：about 300G
* Train split：700 scenes
* Val split：150 scenes
* Test split：150 scenes

  ![1669703485697](image/data/1669703485697.png)



# Other Data Preparation

After downloading the dataset needed, since EagerMOT rely on other detection algorithms to provide detection results, you should also get the results of official format (txt for Kitti sequences and json for NuScenes split). Here we provide several state-of-art detection results, you can also use your own's with same format.

1. Download detections from the [website](https://github.com/aleksandrkim61/EagerMOT#download-3d-and-2d-detections-which-ones-to-download-depends-on-what-you-want-to-run).
2. The prepared data should be stored in the following way. **Note** the sub folder of split should be listed under the folder of detection names, such as training, testing for Kitti and train, val, test for NuScenes. For example, see ab3dmot.

```
${root_dir}
   |-- datasets
       |-- nuscenes
       |-- kitti
   |-- workspace
       |-- nuscenes
       |-- kitti
   |-- ab3dmot
       |-- training
       |-- testing
   |-- detections_segmentations_RRC_BB2SegNet
   |-- detections_segmentations_trackrcnn_BB2SegNet
   |-- mmdetection_cascade_x101
   |-- centerpoint
   |-- pointgnn
   |-- trackrcnn
```
