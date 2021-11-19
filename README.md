# ICCV 2021 - Low Power Computer Vision Workshop

## Low-Power Computer Vision Challenge 2021 - Basic Information

  * **Sponsor** : Xilinx
  * **Competition** : August 1st 9:00 AM - August 31st 11:59 PM EST
  * **Task** : Object Detection
  * **Dataset** : COCO2017 test-dev
  * **Hardware** : Ultra96-V2 + Xilinx Deep Learning Processor Unit (DPU)
  * **Software** : DPU
  * **Evaluation** : 10^4 / Energy  * ReLU (mMAP – 0.2) * ReLU (fps – 5). Where mMAP is INT8 quantized accuracy

## Baseline Code : YOLOv4-tiny

> ### 1. CSPNet: A New Backbone that can Enhance Learning Capability of CNN

* CSP module의 idea 도입
* 아래 그림과 같이 한 Feature Map의 channel을 2개의 group으로 분리 (이 때 비율을 growth rate라고 한다. 1/2 is preferred)
* 한 group이 layer들을 통과하고 얻은 Feature map과 나머지 group을 concat시킨다. (아래 그림 참조)

![image](https://user-images.githubusercontent.com/77262389/142585860-ac505823-c5b4-48b2-ae6c-9964e781227b.png)

> ### 2. Computational block of YOLOv4-tiny using CSP module

* YOLOv4-tiny의 block에 CSP module을 적용
![image](https://user-images.githubusercontent.com/77262389/142585573-b11f05b8-f439-4f0e-ab4e-b181209962bd.png)

## Training & Validation Result

### 1. Convert COCO to YOLO format

- COCO dataset의 annotation은 좌상단의 좌표를 (x, y)로 하고 Bounding Box의 width와 height가 주어진다. (INT값)
- YOLO dataset의 annotation은 전체 영상에 대한 좌표의 비율으로 계산한다. (Floating Point)
  - 정가운데의 좌표를 (x, y)로 하고 Bounding Box의 width와 height를 각각 이미지의 width와 height에 대한 비율로 주어진다 (Float 값)
- 따라서 COCO dataset의 annotation을 YOLO의 annotation으로 바꿔준다. 변환하는 코드는 _coco_annotation.py_ 참조

### 2. Training Loss & Validation Accuracy Graph

> 중간에 학습이 끊겨서 초반부 학습 Graph가 없어졌다.. 😰

- **Validation Accuracy 34%**

![chart_yolov4-tiny_hyunwoo](https://user-images.githubusercontent.com/77262389/142588356-78c3ea45-6722-4aa9-ad96-118ba989716d.png)

### 3. Prediction sample

![predictions](https://user-images.githubusercontent.com/77262389/142588796-4c879e8e-b73d-4fbb-b9de-4db92dd94968.jpg)


# Docker Images Are here
https://hub.docker.com/r/ekfmsrj4/lpcv
