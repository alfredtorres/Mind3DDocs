# SynergyNet

### Introduction
[<a href="https://arxiv.org/abs/2110.09772">paper</a>] [<a href="https://youtu.be/i1Y8U2Z20ko">video</a>]

Title: Synergy between 3DMM and 3D Landmarks for Accurate 3D Facial Geometry

Authors: Cho-Ying Wu, Qiangeng Xu, Ulrich Neumann, CGIT Lab at University of Souther California

Abstract: This work studies learning from a synergy process of 3D Morphable Models (3DMM) and 3D facial landmarks to predict complete 3D facial geometry, including 3D alignment, face orientation, and 3D face modeling. Our synergy process leverages a representation cycle for 3DMM parameters and 3D landmarks. 3D landmarks can be extracted and refined from face meshes built by 3DMM parameters. We next reverse the representation direction and show that predicting 3DMM parameters from sparse 3D landmarks improves the information flow. Together we create a synergy process that utilizes the relation between 3D landmarks and 3DMM parameters, and they collaboratively contribute to better performance. We extensively validate our contribution on full tasks of facial geometry prediction and show our superior and robust performance on these tasks for various scenarios. Particularly, we adopt only simple and widely-used network operations to attain fast and accurate facial geometry prediction.

## Running 

### Evaluation

- The following configuration for eval.

  ```shell
  python tools/facereconstruction/eval.py -opt ./configs/synergy_net/synergynet.yaml
  ```


### Training

- The following configuration for train.

  ```shell
  python tools/facereconstruction/train.py -opt ./configs/synergy_net/synergynet.yaml
  ```

Note that we just provide these hyper parameter ranges for reference only, and we can not guarantee that they are the optimal range of this model.

### Infer

- The following configuration for infer.

  ```shell
  python tools/facereconstruction/infer.py -opt ./configs/synergy_net/synergynet.yaml
  ```

### Model export

- The following configuration for exporting model.

  ```shell
  python tools/facereconstruction/export.py -opt ./configs/synergy_net/synergynet.yaml
  ```
