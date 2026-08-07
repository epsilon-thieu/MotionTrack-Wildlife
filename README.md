## Introduction

This repository provides the training and benchmarking pipeline for evaluating
[MotionTrack](https://github.com/lzq11/MotionTrack) — a multi-object tracker
built on a YOLOv7 detector — on a custom wildlife dataset, in addition to the
standard COCO-pretrained setup.

Specifically, this repo covers:

- **Dataset reformatting** — converting the
  [Wildlife dataset](https://data.bris.ac.uk/data/dataset/ewnuoroebuae20vei0cu6zu69)
  into the annotation and directory format required by the MotionTrack
  tracker and YOLOv7 detector (MOT-style `gt.txt`, `seqinfo.ini`, frame
  sequences).
- **Detector fine-tuning** — fine-tuning the YOLOv7 detector weights on the
  reformatted wildlife dataset for improved detection accuracy on
  wildlife-specific classes (elephant, zebra, giraffe).
- **Benchmarking** — running and evaluating MotionTrack with both the
  original COCO-pretrained weights and the fine-tuned wildlife weights, for
  direct performance comparison.

![Tracking demo](figure/demo.gif)

## Data Preparation
### Original wildlife dataset structure
wildlife_dataset/
|---sequence_name1/
    |---frames/
    |   |---frame_0.jpg
    |   |---frame_1.jpg ...
    |---boxid/
        |---frame_0.jpg
        |---frame_1.jpg ...

### Structure required by the MotionTrack detector (YOLOv7)
        JMT2022
        |——————images
        |        └——————train
        |                   └——————img_file(*.jpg)
        |        └——————test1
        |——————labels
        |        └——————train
        |                   └——————label_file(*.txt)
        |        └——————test1

### Structure required by the MotionTrack tracker
        jmt2022/
        └── dataset/
                ├── test/
                ├── seq_001/
                │   ├── seqinfo.ini
                │   ├── seq_001/
                │   │   ├── 000001.jpg
                │   │   ├── 000002.jpg
                │   │   └── ...
                │   └── det/
                │       └── det.txt
                ├── seq_002/
                └── ...

### Why this repo exists

Since the original wildlife dataset layout differs from what the MotionTrack
detector and tracker each expect, this repo integrates conversion scripts
that automatically transform the original wildlife structure into the
format required by MotionTrack — **no manual restructuring needed** on
your end.

To use these scripts, place the wildlife dataset in the following layout:
\`\`\`
MotionTrack-Wildlife/
└── wildlife_dataset/
        ├── datawildlife_train/
        ├── datawildlife_val/
        └── datawildlife_test/
\`\`\`







Data preparation

bởi vì wildlife dataset có cấu trúc

wildlife dataset
     |---sequence_name1
           |---frames
                |---frame_0.jpg
                |---frame_1.jpg ...
           |---boxid
                |---frame_0.jpg
                |---frame_1.jpg ...

cấu trúc mỗi seq phần detector yolov7 của motiontrack cần

JMT2022
   |——————images
   |        └——————train
   |                   └——————img_file(*.jpg)
   |        └——————test1
   |——————labels
   |        └——————train
   |                   └——————label_file(*.txt)
   |        └——————test1
Cấu trúc phần tracker của motiontrack cần 
jmt2022/
└── dataset/
    ├── test/
       ├── seq_001/
       │   ├── seqinfo.ini
       │   ├── seq_001/
       │   │   ├── 000001.jpg
       │   │   ├── 000002.jpg
       │   │   └── ...
       │   └── det/
       │       └── det.txt
       ├── seq_002/
       └── ...
bởi vì phần cấu trúc có sự khác nhau nên tôi đã tích hợp/ thêm để có thể tự transform cấu trúc gốc của wildlife sang cấu trúc mà motiontrack cần mà bạn không cần chỉnh sửa gì thêm. Yêu cầu bạn đặt cấu trúc dataset của wildlife theo cấu trúc
MotionTrack-Wildlife/
└── wildlife_dataset/
    ├── datawildlife_train/
    ├── datawildlife_val/
    ├── datawildlife_test/
    