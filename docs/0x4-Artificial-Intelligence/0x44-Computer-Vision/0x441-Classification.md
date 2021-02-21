# 0x441 Classification

- [1. Classification](#1-classification)
- [2. Detection](#2-detection)
    - [2.1. R-CNN (Region-Based CNN)](#21-r-cnn-region-based-cnn)
    - [2.2. Fast R-CNN](#22-fast-r-cnn)
    - [2.3. Faster R-CNN](#23-faster-r-cnn)
- [3. Reference](#3-reference)

## 1. Classification

## 2. Detection

**Task (Object Detection)** The task of object detection is as follows:

*   input: an RGB image
*   output: A set of detected objects, for each object we have an category label (from fixed, known set of categories) and Bounding box (x, y, width, height)

The challenges of the object detection task is

*   **multiple outputs**: need to output variable numbers of objects per image
*   **multiple output types**: need to predict what and where
*   **large images**: need a higher resolution for detection often ~800x600 (classification task: 224x224)

A simple approach is to use the **sliding window**: apply a CNN to many different crops of images to classify for each crop. However, this would generate too many boxes therefore not feasible.

**Metric (IoU Intersection Over Union)** compute the overlap between the ground truth box and the prediction box. IoU > 0.5 is "decent", 0.7 is "pretty good", 0.9 is "almost perfect"

$$\frac{\text{Area of Intersection}}{\text{Area of Union}}$$

**Metric (mAP: Mean Average Precision)** compute AP (area under precision recall area), for each category and take mean. In COCO MAP, repeat this for different IoU threshold

### 2.1. R-CNN (Region-Based CNN)

Step 1: find region proposals (maybe from some external algorithms)

**Region proposal** is to find a small set of boxes that are likely to cover all objects. For example, Selective Search gives 2000 regions

Step 2: wrap image regions into 224x224 and run convolutional net to predict class dsitributions and transformation of bounding box $(t_x, t_y, t_h, t_w)$

$$b_x = p_x + p_w t_x$$

$$b_w = p_w \exp(t_w)$$

Note that weight and height are transformed in exp scale

One problem arises here is that object detctors might output many overlapping detections. The solution is to postprocess raw detections using **Non-Max Suppression**, it is to greedily pickup the highest scoring box and delete box whose overlap with it is high enough. This still has some open issues that it may eliminate good boxes.

### 2.2. Fast R-CNN

One issue with R-CNN is its very slow (running full CNN for 2000 proposals). Fast R-CNN split the full CNN into two CNN, where the first CNN (backbone network) is shared by all proposals. Most computation happens here so it is fast.

The proposed region is to take shared output from the first backbone CNN and forward through the second small CNN.

### 2.3. Faster R-CNN

With Fast R-CNN, most computational costs are from the region proposals, to further make it faster, Faster R-CNN uses the **Region Proposal Network (RPN)** to predict proposals from features

## 3. Reference

[1] EECS 498-007 [Deep Learning for Computer Vision](https://web.eecs.umich.edu/~justincj/teaching/eecs498/FA2020/)

[2] Girshick, Ross, et al. "Rich feature hierarchies for accurate object detection and semantic segmentation." _Proceedings of the IEEE conference on computer vision and pattern recognition_. 2014.