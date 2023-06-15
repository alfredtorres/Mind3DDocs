# Dataset Introduction

[ScanNet V2](:http://www.scan-net.org/):

* Size：about 3G
* Data format：.npy and .txt
* Download images [<a href="train_aug_120x120.zip</a>">ScanNet_V2 data</a>] and extract the zip file under the root folder.

# Data Preparation

* Download data and extract the zip file. 

* Extract these data under the repo root.

```shell
${root_dir}
	|--meta_data
		|--scannet_means.npz
		|--scannetv2_test.txt
		|--scannetv2_train.txt
		|--scannetv2_val.txt
	|--scannet_train_detection_data
		|--scene0000_00_bbox.npy
		|--scene0000_00_ins_label.npy
		|--scene0000_00_sem_label.npy
		|--scene0000_00_vert.npy
		|--...
	|--train_data.pkl
	|--val_data.pkl