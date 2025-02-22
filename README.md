## Linear Gaussian Bounding Box Representation and Ring-Shaped Rotated Convolution for Oriented Object Detection
<p align="justify">
In oriented object detection, current representations of oriented bounding boxes (OBBs) often suffer from the boundary discontinuity problem. Methods of designing continuous regression losses do not essentially solve this problem. Although Gaussian bounding box (GBB) representation avoids this problem, directly regressing GBB is susceptible to numerical instability. We propose linear GBB (LGBB), a novel OBB representation. By linearly transforming the elements of GBB, LGBB avoids the boundary discontinuity problem and has high numerical stability. In addition, existing convolution-based rotation-sensitive feature extraction methods only have local receptive fields, resulting in slow feature aggregation. We propose ring-shaped rotated convolution (RRC), which adaptively rotates feature maps to arbitrary orientations to extract rotation-sensitive features under a ring-shaped receptive field, rapidly aggregating features and contextual information. Experimental results demonstrate that LGBB and RRC achieve state-of-the-art performance. Furthermore, integrating LGBB and RRC into various models effectively improves detection accuracy.
</p>

## Realted Work
1. Comparison with Current OBB Representations
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/OBB_Representation.png" width="800px">
</div>

2. Comparison with Current Convolution-Based Rotation-Sensitive Feature Extraction Methods
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/Orientation_Sensitive_Feature_Extraction.png" width="350px">
</div>

## Methods
1. Overview
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/Overview.png" width="700px">
</div>

2. LGBB
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/LGBB.png" width="350px">
</div>

3. RRC
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/RRC.png" width="700px">
</div>

## Experiments
1. Comparison with Current OBB Representations
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/OBB_Comparison.png" width="500px">
</div>

2. Comparison with Current Convolution-Based Rotation-Sensitive Feature Extraction Methods
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/Vis_RRC.png" width="600px">
      
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/RRC_Comparison.png" width="500px">
</div>

3. Comparison with Current Oriented Object Detectors
<div align=center>
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/Experiments_Comparison.png" width="900px">
      
<img src="https://github.com/zhen6618/RotaYolo/blob/main/figure/Vis_Comparison.png" width="650px">
</div>

## Installation
Refer to both [yolov7](https://github.com/WongKinYiu/yolov7) and [mmrotate](https://github.com/open-mmlab/mmrotate)

## Prepare Your Dataset
[DOTA](https://captain-whu.github.io/DOTA/index.html)  
[HRSC2016](https://sites.google.com/site/hrsc2016/)


## Training
```
# Single GPU training
python train.py --workers 8 --device 0 --batch-size 2 --data data/dota.yaml --img 1024 1024 --cfg cfg/training/RotaYolo_RotaConv.yaml --weights '' --hyp data/hyp.scratch.dota.yaml

# Multiple GPU training
python -m torch.distributed.launch --nproc_per_node 4 --master_port 9527 train.py --workers 8 --device 0,1,2,3 --sync-bn --batch-size 8 --data data/dota.yaml --img 1024 1024 --cfg cfg/training/RotaYolo_RotaConv.yaml --weights '' --hyp data/hyp.scratch.dota.yaml
```

## Detecting
```
python detect.py --weights 'weights/best.pt' --source 'datasets/DOTA/demo.png' --img-size 1024 --conf-thres 0.5 --iou-thres 0.2 --device 0
```

## Citation
```
@article{ZHOU2024110677,
      title = {Linear Gaussian bounding box representation and ring-shaped rotated convolution for oriented object detection},
      journal = {Pattern Recognition},
      volume = {155},
      pages = {110677},
      year = {2024},
      author = {Zhen Zhou and Yunkai Ma and Junfeng Fan and Zhaoyang Liu and Fengshui Jing and Min Tan},
}
```

## Acknowledgement
[mmrotate](https://github.com/open-mmlab/mmrotate)

[yolov7](https://github.com/WongKinYiu/yolov7)

