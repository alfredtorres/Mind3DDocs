# Dataset Introduction

[300W-LP](https://drive.google.com/file/d/1YVBRcXmCeO1t5Bepv67KVr_QKcOur3Yy/view?usp=sharing):

* Size：about 10G
* Data format：.npy and .jpg
* Download images [<a href="https://github.com/cleardusk/3DDFA">train_aug_120x120.zip</a>] and extract the zip file under the root folder (Containing about 680K images).

[AFLW2000-3D](https://drive.google.com/file/d/1SQsMhvAmpD1O8Hm0yEGom0C0rXtA0qs8/view?usp=sharing):
* Size：about 15M
* Data format：.npy and .jpg

These data are processed from [<a href="https://github.com/cleardusk/3DDFA">3DDFA</a>] and [<a href="https://github.com/shamangary/FSA-Net">FSA-Net</a>].

# Data Preparation

* Download data and extract the zip file. 

* Extract these data under the repo root.

```shell
 ${root_dir}
 |--3dmm_data #training dataset
    |--train_aug_120x120
       |--AFWFlip_AFW_1051618982_1_0_1.jpg
       |--...
    |--BFM_UV.npy
    |--u_exp.npy
    |--...    
 |--aflw2000_data #testing dataset
    |--AFLW2000-3D_crop
        |--image00002.jpg
        |--...
    |--eval
        |--AFLW2000-3D.pose.npy
        |--...
    |--AFLW2000-3D_crop.list
```