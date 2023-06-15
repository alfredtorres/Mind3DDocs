## [PointPillars ](#contents)Introduction of Fast Encoders for Object Detection from Point Clouds algorithm

PointPillars is a one-stage end-to-end point cloud object detection network. The network structure of PointNet is used for extracting features, but at the same time the idea of voxel is adopted: in a certain range of vertical columns, the points in this range are collated and their z-direction information is ignored, so that they can be processed with 2D convolution. This method combines the advantages of the above two methods and achieves a faster encoding of point cloud object detection while maintaining accuracy.

PointPillars entire network structure is divided into three parts.

* Pillar Feature Net: Converts the input point cloud into a sparse Pseudo image
* Backbone:Process Pseudo image to get high level features
* Detection Head:Detect and return to 3D box

> [Paper](https://arxiv.org/abs/1812.05784):  PointPillars: Fast Encoders for Object Detection from Point Clouds. Alex H. Lang, Sourabh Vora, Holger Caesar, Lubing Zhou, Jiong Yang, Oscar Beijbom, 2018.

## [Dataset](#contents) Overview of 3D detection dataset kitti

Dataset official website: [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d)

1. Sensor Configuration

   Due to the Bayer array (Bayer Pattern) [interpolation](https://so.csdn.net/so/search?q=%E6%8F%92%E5%80%BC&spm=1001.2101.3001.7020) processing in the color camera imaging process, the color image resolution is low and for light sensitivity is not high, so the acquisition vehicle is equipped with two sets of binocular cameras, a group of grayscale, a group of color. Personally, I guess that in order to increase the horizontal field of view of the camera, each camera lens is installed in front of another optical lens.
2. Dataset Acquisition

   The entire KITTI dataset was collected in Karlsruhe, Germany, over a 6-hour period, and the data released on KITTI's website represents approximately 25% of the total collection. ", "Residential", "Campus" and "Pedestrian".

   Image: Saved in 8bit PNG format. The hood and sky parts of the original image were cropped out, and the distortion was corrected according to the camera parameters, resulting in a final image of about 500,000 pixels.
   Laser: counterclockwise rotation, saved in a floating point binary file. The laser point ( x , y , z ) (x,y,z) (x,y,z) coordinates and reflectivity r rr information are saved, with an average of 120,000 laser points per frame.
   Image and laser synchronization: The camera exposure timing is controlled by the laser, which triggers the camera shutter when it scans directly in front (i.e., the camera facing angle), and KITTI records the laser's 3 timestamps, the moment the rotation starts and ends, and the moment it triggers the camera exposure.
3. Data Annotation

   For each dynamic target in the camera's field of view, KITTI provides 3D annotation information based on the laser coordinate system, defining seven target types: car, van, truck, pedestrian, seated person, bicycle, and tram, with other niche types such as trailers and mobility scooters grouped under the "Misc" category. 3D labeling information includes target size, world coordinates and yaw angle (roll angle and pitch angle are equal to 0 by default).
4. Sensor calibration

   In order to minimize system deviations brought about by time, KITTI recalibrates all sensors once a day after data collection.
   Sensor synchronization: The timestamp of the LiDAR is used as a reference class to synchronize other sensors. For the cameras, the deviation due to dynamic targets is minimized by means of the LIDAR-triggered camera shutter. the GPS/IMU cannot be synchronized, but the maximum time error is only 5 ms due to the high acquisition frequency. the timestamps of all sensors are recorded using the system clock.
   Camera calibration: All 4 camera optical centers are aligned to the same plane. Due to the presence of pillow distortion in the image, the distortion-corrected images were cropped from 1392 × 512 1392\times5121392×512 to 1224 × 370 1224\times3701224×370 pixels in size.
   Laser calibration: The LIDAR was first installed according to the position of the left grayscale camera, and then the calibration error was optimized based on the selection of 50 hand-picked points, and the calibration robustness was ensured according to the performance variation of the Top3 method of the KITTI stereo vision list.
5. Labeled data analysis

   | Fields     | Field Length | Unit      | Implication                                                                                                                                   |
   | ---------- | ------------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
   | Type       | 1            | -         | Target Type                                                                                                                                   |
   | Truncated  | 1            | -         | Target truncation degree: a floating point number between 0 and 1<br />indicates the degree of distance of the target from the image boundary |
   | Occluded   | 1            | -         | Target obscuration degree: integer between 0 and 3                                                                                            |
   | Alpha      | 1            | Curvature | Target observation angle：[−p i, p i]                                                                                                        |
   | Bbox       | 4            | Pixel     | Target 2D detection frame position: pixel coordinates of the top left vertex and bottom right vertex                                          |
   | Dimensions | 3            | metre     | 3D target size: height, width,                                                                                                                |
   | Location   | 3            | metre     | Target 3D frame bottom center coordinates: ( x , y , z ) Camera coordinate system                                                             |
   | Rotation_y | 1            | Curvature | Target orientation angle：[−p i, p i]                                                                                                        |

## Environment Configuration

- Hardware（GPU）

  - Prepare a hardware environment with a GPU processor.
- AI algorithm framework

  - [MindSpore](https://gitee.com/mindspore/mindspore)
- Download [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d), Put `ImageSets` into `/src/data/ImageSets/`

  - [Download left color images of object data set (12 GB)](https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_image_2.zip)
  - [Download camera calibration matrices of object data set (16 MB)](https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_calib.zip)
  - [Download training labels of object data set (5 MB)](https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_label_2.zip)
  - [Download Velodyne point clouds, if you want to use laser information (29 GB)](https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_velodyne.zip)
- Unzip all downloaded dataset files with the following directory structure.

  └── KITTI
  ├── training
  │   ├── image_2 <-- for visualization
  │   ├── calib
  │   ├── label_2
  │   ├── velodyne
  │   └── velodyne_reduced <-- create this empty directory
  └── testing
  ├── image_2 <-- for visualization
  ├── calib
  ├── velodyne
  └── velodyne_reduced <-- create this empty directory
- A script is required to pre-process the KITTI dataset before executing this code

```shell
#Step1: Create KITTI infos:
cd ./dataset/kitti/src
python create_data.py create_kitti_info_file --data_path=KITTI_DATASET_ROOT
```

```shell
#Step2: Create KITTI infos:Create reduced point cloud:
python create_data.py create_reduced_point_cloud --data_path=KITTI_DATASET_ROOT
```

```shell
#Step3：Create groundtruth-database infos:
python create_data.py create_groundtruth_database --data_path=KITTI_DATASET_ROOT
```

```text
#Step4: The network model configuration file `car_xyres16.yaml` or `ped_xyres16.yaml` or `ped_cycle_xyres16.yaml` needs to change the location of the preprocessed file
train_input_reader:
  ...
  database_sampler:
    database_info_path: "/path/to/kitti_dbinfos_train.pkl"
    ...
  kitti_info_path: "/path/to/kitti_infos_train.pkl"
  kitti_root_path: "KITTI_DATASET_ROOT"
...
eval_input_reader:
  ...
  kitti_info_path: "/path/to/kitti_infos_val.pkl"
  kitti_root_path: "KITTI_DATASET_ROOT"
```

* Install the required python environment

```
conda create --name pointpillars python=3.7
conda activate pointpillars 
pip install -r requirements.txt
```

## YAML file configuration

Before executing the project, it is necessary to/ Configure the YAML file in the configs/pointpillars folder, with configuration items including: train_set_up，eval_set_up，infer_set_up， export_set_up

## Training and Evaluation

After preparing the dataset according to the above steps, the training and evaluation of pointpilliar can be carried out according to the following specific steps. Here note that the training set of KITTI dataset is divided into train and val, and the test dataset needs to be submitted to the official website for evaluation.

#### Train
```shell
python ./tools/detection/train.py --opt ./configs/pointpillars/car_xyres16.yaml
```
or

```shell
python ./tools/detection/train.py --opt ./configs/pointpillars/ped_cycle_xyres16.yaml
```
#### Evaluate

```shell
python ./tools/detection/eval.py --opt ./configs/pointpillars/car_xyres16.yaml
```
or
```shell
python ./tools/detection/eval.py --opt ./configs/pointpillars/ped_cycle_xyres16.yaml
```

* Evaluation results： Performance in KITTI validation set (50/50 split; 160 epochs)
  |                      |               | Easy  | Mod   | Hard  |
  | -------------------- | ------------- | ----- | ----- | ----- |
  | **Cyclist**    | **AP@** | 0.50  | 0.50  | 0.50  |
  | bbox                 | AP:           | 84.33 | 66.74 | 63.42 |
  | bev                  | AP:           | 81.94 | 62.29 | 58.85 |
  | 3d                   | AP:           | 78.28 | 59.01 | 59.01 |
  | aos                  | AP:           | 83.83 | 65.60 | 62.19 |
  | **Pedestrian** | **AP@** | 0.50  | 0.50  | 0.50  |
  | bbox                 | AP:           | 65.07 | 62.50 | 59.33 |
  | bev                  | AP:           | 72.30 | 67.32 | 62.35 |
  | 3d                   | AP:           | 65.02 | 59.86 | 54.64 |
  | aos                  | AP:           | 42.59 | 41.99 | 39.74 |

  |               |               | Easy  | Mod   | Hard  |
  | ------------- | ------------- | ----- | ----- | ----- |
  | **Car** | **AP@** | 0.70  | 0.70  | 0.70  |
  | bbox          | AP:           | 90.66 | 88.81 | 86.74 |
  | bev           | AP:           | 89.87 | 86.74 | 83.91 |
  | 3d            | AP:           | 85.95 | 76.30 | 69.63 |
  | aos           | AP:           | 90.62 | 88.49 | 86.08 |

The mAP's are calculated as the average of the metric values of the corresponding rows for each category. The different detection difficulties are defined as follows.

1. Easy: minimum bounding box height: 40 Px, maximum occlusion level: fully visible, maximum truncation rate: 15 %
2. Moderate. minimum bounding box height: 25 Px, maximum occlusion: partially occluded, maximum truncation rate: 30 %
3. Hard: minimum bounding box height: 25 Px, maximum occlusion: difficult to see, maximum cutoff rate: 50 %

## Infer and Export

### Infer

```shell
python ./tools/detection/infer.py --opt ./configs/pointpillars/car_xyres16.yaml
```
or
```shell
python ./tools/detection/infer.py --opt ./configs/pointpillars/ped_cycle_xyres16.yaml
```

### Export

```shell
python ./tools/detection/export.py --opt ./configs/pointpillars/car_xyres16.yaml
```
or
```shell
python ./tools/detection/export.py --opt ./configs/pointpillars/ped_cycle_xyres16.yaml
```