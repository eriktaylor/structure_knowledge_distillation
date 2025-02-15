#  Structured Knowledge Distillation for Dense Prediction

This repository contains the source code of [Structured Knowledge Distillation for Dense Prediction](https://arxiv.org/pdf/1903.04197.pdf).

Re-writing this as a demonstration of the other tasks outined in the paper.

## Sample results

Coming soon.
 
## Structure of this repository
This repository is organized as:
* [libs](/libs/) This directory contains the inplaceABNSync modes.
* [dataset](/dataset/) This directory contains the dataloader for different datasets.
* [networks](/networks/) This directory contains a model zoo for network models.
* [utils](/utils/) This directory contains api for calculating the distillation loss.

## Pre-trained model and Performance on various tasks
Pretrain models for three tasks can be found here:

| Task |Dataset| Network |Method | Evaluation Metric|Link|
| -- | -- |-- | -- |-- |-- |
| Depth estimation |nyudv2| [VNL](https://github.com/YvanYin/VNL_Monocular_Depth_Prediction.git)|baseline|rel: 13.5 |-|
| Depth estimation | nyudv2|[VNL](https://github.com/YvanYin/VNL_Monocular_Depth_Prediction.git)|+ our distillation|rel: 13.0 |[link](https://cloudstor.aarnet.edu.au/plus/s/IXk0i0cJaibgJAr)|

Note: Other checkpoints can be obtained by email from original author: yifan.liu04@adelaide.edu.au if needed.


## Requirement
python3.5 

pytorch0.4.1 

ninja 

numpy 

cv2 

Pillow

We recommend to use [Anaconda](https://conda.io/docs/user-guide/install/linux.html).

We have tested our code on Ubuntu 16.04.

### Compiling

Some parts of InPlace-ABN have a native CUDA implementation, which must be compiled with the following commands:
```bash
cd libs
sh build.sh
python build.py
``` 
The `build.sh` script assumes that the `nvcc` compiler is available in the current system search path.
The CUDA kernels are compiled for `sm_50`, `sm_52` and `sm_61` by default.
To change this (_e.g._ if you are using a Kepler GPU), please edit the `CUDA_GENCODE` variable in `build.sh`.

More on this here: https://github.com/speedinghzl/pytorch-segmentation-toolbox

## Quick start to test the model
1. download the [Cityscape dataset](https://www.cityscapes-dataset.com/)
2. sh run_test.sh [you should change the data-dir to your own]. By using our distilled student model, which can be gotten in [ckpt], an mIoU of 73.05 is achieved on the Cityscape test set, and 75.3 on validation set.

| Model | Average | roda | sidewalk | building|	wall | fence | pole | trafficlight | trafficsign | vegetation | terrain | sky | person | rider | car | truck | bus | train | motorcycle | bicycle |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| IoU | 73.05 | 97.57 | 78.80 | 91.42 | 50.76 | 50.88 | 60.77 | 67.93 | 73.18 | 92.49 | 70.36 | 94.56 | 82.81 | 61.64 | 94.89 | 60.14 | 66.62 | 59.93 | 61.50 | 71.71 |

Note: Depth estimation task and object detection task can be test through the original projects of VNL and FCOS using our checkpoints.
## Train script
Download the pre-trained [teacher weight](https://cloudstor.aarnet.edu.au/plus/s/tFjYfBJiarVi0pG):

If you want to reproduce the ablation study in our paper, please modify is_pi_use/is_pa_use/is_ho_use in the run_train_eval.sh.
sh run_train_eval.sh

## Test script
If you want to test your method on the cityscape test set, please modify the data-dir and resume-from path to your own, then run the test.sh and submit your results to www.cityscapes-dataset.net/submit/ 
sh test.sh

## License
For academic use, this project is licensed under the 2-clause BSD License - see the LICENSE file for details. For commercial use, please contact [Yifan Liu](yifan.liu04@adelaide.edu.au) and [Chunhua Shen](chunhua.shen@adelaide.edu.au).
