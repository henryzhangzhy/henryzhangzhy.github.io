---
title: Probabilistic Semantic Mapping for Autonomous Driving Applications
date: 2020-03-23
description: Building a semantic map with camera and LiDAR.
author: Henry
categories:
    - Autonomous Vehicles
tags:
    - Semantic Mapping
    - Sensor Fusion
image: semantic_map_2020_zoom.png
comments: true
---

This is a work we submitted to IROS2020, co-authored by David Paz, Qinru Li, and Hao Xiang. We applied state-of-the-art semantic segmentation network to build a local map with semantic information such as roads, lanes and crosswalks based on vision and lidar data.

## Motivation

Autonomous driving today still strongly rely on high-definition maps, which often encodes the road, lane, traffic light, crosswalk information and so forth. High-definition map often requires large amount of human labeling. Part of the time-consuming step is to extract the semantic information [1]. Thus our work aims at moving a step closer to HD map automation by automatic semantic annotation.

## Method

### Semantic Segmentation

A network trained with DeepLabV3Plus [2] architecture on the Mapillary Vistas dataset [3]. The network trained with publicly available dataset achieves great generalization. We directly applied it to our scenario without fine-tuning.

### Semantic Association

How to associate the semantic labels in 2D image with the map? Methods assuming a flat road and fixed camera are subject to nosie. Since our vehicle is localized with respect to the local point cloud map, we project a segment of the map into the image and retrieve the semantic labels.

### Semantic Mapping

The local point cloud with semnatic label is good at visualization, but not for information retrieval. Also, it is hard to maintain temporal consistency on the point cloud map. Instead, we use a probabilistic map to reprensent the local information. for each cell, we encode the log odds of the cell being each class. For each semantic point cloud, we project the semantic label on the map cell and update the corresponding log odds.

## Experiments

See [arXiv](https://arxiv.org/abs/2006.04894)

## Observations

Semantic segmentation network trained on publicly available dataset generalized well. It performs better for close range. For this architecture on our image, the speed is about 4fps. It is the bottle neck of the entire system. Mapping runs super fast, often within 0.05s. 
Probabilistic map is very robust to noise. Although semantic segmentation make mistakes when the objects are far away, it will correct it overtime.

## Reference

[1] J. Jiao. Machine learning assisted high-definition map creation. In 2018 IEEE 42nd Annual Computer Software and Applications Conference (COMPSAC), volume 01, pages 367–373, July 2018.

[2] Liang-Chieh Chen, Yukun Zhu, George Papandreou, Florian Schroff, and Hartwig Adam. Encoder-decoder with atrous separable convolution for semantic image segmentation. Lecture Notes in Computer Science, page 833–851, 2018.

[3] Gerhard Neuhold, Tobias Ollmann, Samuel Rota Bulò, and Peter Kontschieder. The mapillary vistas dataset for semantic understanding of street scenes. In International Conference on Computer Vision (ICCV), 2017. 