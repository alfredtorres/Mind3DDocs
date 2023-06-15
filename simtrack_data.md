# Dataset Descrption

## NuScenes

You can download the dataset through the official website [here](https://www.nuscenes.org/nuscenes#overview)

## Introduction

In March 2019 we released the full nuScenes dataset with 1000 scenes. Due to the huge size of the dataset, we provide the mini, trainval and test splits separately. Mini (10 scenes) is a subset of trainval used to explore the data without having to download the entire dataset. Trainval (700+150 scenes) is packaged into 10 different archives that each contain 85 scenes. Test (150 scenes) is used for challenges and does not come with object annotations. Alternatively, it is also possible to download only selected modalities (camera, lidar, radar) or only keyframes. The meta data is provided separately and includes the annotations, ego vehicle poses, calibration, maps and log information.

```trainval
850 scenes, 700 train, 150 val. Metadata is for all 850 scenes, sensor file blobs are split into 10 subsets that each contains 85 scenes. If you want to download only a subset of the data, you can choose between different sensor modalities (lidar, radar and camera) or keyframes only.

Metadata  [US, Asia]                         0.43 GB (461179800 Bytes)    md5: 3eee698806fcf52330faa2e682b9f3a1

File blobs of 85 scenes, part 1  [US, Asia]  29.41 GB (31574298075 Bytes) md5: 8b5eaecef969aea173a5317be153ca63

File blobs of 85 scenes, part 2  [US, Asia]  28.06 GB (30128325054 Bytes) md5: 116085f49ec4c60958f9d49b2bd6bfdd

File blobs of 85 scenes, part 3  [US, Asia]  27.81 GB (29862707349 Bytes) md5: 9de7f2a72864d6f9ef5ce0b74e84d311

File blobs of 85 scenes, part 4  [US, Asia]  29.87 GB (32070725354 Bytes) md5: 4d0bec5cc581672bb557c777cd0f0556

File blobs of 85 scenes, part 5  [US, Asia]  26.25 GB (28181092231 Bytes) md5: 3747bb98cdfeb60f29b236a61b95d66a

File blobs of 85 scenes, part 6  [US, Asia]  25.61 GB (27503837689 Bytes) md5: 9f6948a19b1104385c30ad58ab64dabb

File blobs of 85 scenes, part 7  [US, Asia]  27.50 GB (29523743832 Bytes) md5: d92529729f5506f5f0cc15cc82070c1b

File blobs of 85 scenes, part 8  [US, Asia]  28.19 GB (30268612637 Bytes) md5: 90897e7b58ea38634555c2b9583f4ada

File blobs of 85 scenes, part 9  [US, Asia]  31.21 GB (33513836703 Bytes) md5: 7cf0ac8b8d9925edbb6f23b96c0cd1cb

File blobs of 85 scenes, part 10  [US, Asia] 38.87 GB (41740937939 Bytes) md5: fedf0df4e82630abb2d3d517be12ef9d

```

## Other Data Preparation

Other necessary data can be generated by using script:

```
python ./utils/sim_create_data.py
```