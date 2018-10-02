# Pose Flow

Official implementation of [Pose Flow: Efficient Online Pose Tracking ](https://arxiv.org/abs/1802.00977).

<p align='center'>
    <img src="posetrack.gif", width="360">
</p>

Results on PoseTrack Challenge validation set:

1. Task2: Multi-Person Pose Estimation (mAP)
<center>

| Method | Head mAP | Shoulder mAP | Elbow mAP | Wrist mAP | Hip mAP | Knee mAP | Ankle mAP | Total mAP |
|:-------|:-----:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| Detect-and-Track(FAIR) | **67.5** | 70.2 | 62 | 51.7 | 60.7 | 58.7 | 49.8 | 60.6 |
| **AlphaPose+PoseFlow** | 66.7 | **73.3** | **68.3** | **61.1** | **67.5** | **67.0** | **61.3** | **66.5** |

</center>

2. Task3: Pose Tracking (MOTA)
<center>

| Method | Head MOTA | Shoulder MOTA | Elbow MOTA | Wrist MOTA | Hip MOTA | Knee MOTA | Ankle MOTA | Total MOTA | Total MOTP|
|:-------|:-----:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| Detect-and-Track(FAIR) | **61.7** | 65.5 | 57.3 | 45.7 | 54.3 | 53.1 | 45.7 | 55.2 | 61.5 |
| **AlphaPose+PoseFlow** | 59.8 | **67.0** | **59.8** | **51.6** | **60.0** | **58.4** | **50.5** | **58.3** | **67.8**|

</center>

## Requirements

- Python 2.7.13
- OpenCV(contains OpenCV-contrib) 3.4.2.16

## Installation

1. Download PoseTrack Dataset from [PoseTrack](https://posetrack.net/) to `AlphaPose/PoseFlow/posetrack_data/`
2. (Optional) Use [DeepMatching](http://lear.inrialpes.fr/src/deepmatching/) to extract dense correspondences between adjcent frames in every video, Please refer to [DeepMatching Compile Error](http://xiuyuliang.cn/2014/12/05/deepmatching/) to compile DeepMatching correctly

```shell
pip install -r requirements.txt

---DeepMatching Version---
cd deepmatching
make clean all
make
cd ..
python matching.py # default using DeepMatching (More Robust but Slower)

---Orb Version---
python matching.py --orb=True # using ORB Matching (Faster but Less Robust)

```
## Quick Start

Firstly, using [AlphaPose](https://github.com/MVIG-SJTU/AlphaPose) to generate multi-person pose estimation results on videos, please see `alpha-pose-results-sample.json` to know json format.

Run pose tracking
```shell
python tracker.py --dataset=val/test  --orb=True/False
```
## Evaluation

Original [poseval](https://github.com/leonid-pishchulin/poseval) has some instructions on how to convert annotation files from MAT to JSON.

Evaluate pose tracking results on validation dataset:

```shell
git clone https://github.com/leonid-pishchulin/poseval.git --recursive
cd poseval/py && export PYTHONPATH=$PWD/../py-motmetrics:$PYTHONPATH
cd ../../
python poseval/py/evaluate.py --groundTruth=./posetrack_data/annotations/val \
                    --predictions=./${track_result_dir}/ \
                    --evalPoseTracking --evalPoseEstimation
```
## Citation

Please cite these papers in your publications if it helps your research:

    @inproceedings{xiu2018poseflow,
      author = {Xiu, Yuliang and Li, Jiefeng and Wang, Haoyu and Fang, Yinghong and Lu, Cewu},
      title = {{Pose Flow}: Efficient Online Pose Tracking},
      booktitle={BMVC},
      year = {2018}
    }





