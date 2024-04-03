---
title: State of the Art in Online Mapping
date: 2024-04-02
description: Continously Updating papers on online mapping
author: Henry
categories:
    - Autonomous Vehicles
tags:
    - Online Mapping
# image: 
comments: true
---

## Online Mapping and Topology Reasoning

1. LaneGraph2Seq: Lane Topology Extraction with Language Model via Vertex-Edge Encoding and Connectivity Enhancement \[[arXiv](https://arxiv.org/abs/2401.17609)\]\[[Github](https://github.com/fudan-zvg/RoadNet)\]
- Using Language model for output decoding.
- Pros: Better connectivity and consistency
- Cons: Discretization leads to low accuracy
2. LANESEGNET: MAP LEARNING WITH LANE SEGMENT PERCEPTION FOR AUTONOMOUS DRIVING \[[arXiv](https://arxiv.org/abs/2312.16108)\]\[[Github](https://github.com/OpenDriveLab/LaneSegNet)\]
- Joint learning of lane boundaries and centerline formulation.
3. Translating Images to Road Network: A Non-Autoregressive Sequence-to-Sequence Approach \[[arXiv](https://arxiv.org/abs/2402.08207)\]
4. TopoMLP
5. TopoNet
6. MapTRv2
7. MapTR
8. STSU
9. VectorMapNet
10. HDMapNet

## Leveraging SD maps

1. Neural Map Prior for Autonomous Driving [arXiv](https://arxiv.org/abs/2304.08481)

## Downstream tasks for Joint Learning

1. VAD

## Building Blocks 

### View Transform Module

1. LSS
2. BEVFormer
3. BEVFusion

### Decoder

1. Deformable DETR
2. Language Models

### Representation Learning

1. V-JEPA \[[Paper](https://ai.meta.com/research/publications/revisiting-feature-prediction-for-learning-visual-representations-from-video/)\]
2. CLIP \[[arXiv](https://arxiv.org/abs/2103.00020)\]\[[Blog](https://openai.com/research/clip)\]


## Scene Reconstruction

1. REAL-TIME PHOTOREALISTIC DYNAMIC SCENE REPRESENTATION AND RENDERING WITH 4D GAUSSIAN SPLATTING \[[arXiv](https://arxiv.org/abs/2310.10642)\]\[[Github](https://github.com/fudan-zvg/4d-gaussian-splatting)\]

## Labs

1. [Marco Pavone](https://stanfordasl.github.io/publications/)
2. [Hang Zhao](https://hangzhaomit.github.io/)
3. [Xingang Wang](https://xwcv.github.io/pubs.htm)
4. [Li Zhang](https://lzrobots.github.io/)


