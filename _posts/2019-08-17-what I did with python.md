---
author: Henry
topic: Geek
comments: true
hide: true
---

A collection of programs I wrote in python.

Python is so handy, I would like to document the things I did with python so that I can find patterns here.

## Projects

1. lshape

   I was developing shape estimation from point cloud and tracking. python helps in quick prototyping.

2. pycar

   A simulation tools that includes the structure of reading map, global planning, local planning, control, vehicle dynamics simulation, logging and matplotlib visualization. It was built for control simulation.

3. 


## scripts

1. new_year

   a script that takes in an image of handwriting, binarizing it and extract the character shape. And build a point cloud demo with that. For happy new year.

2. secret

   Converts a string to ascii binary representation, encode and decode it.

3. hugefiles

   Generate huge files to fill the disk.

4. generate_notes

   Generate notes from source files lines with # NOTE tag.

## python used in class

1. ECE 276A

   1. barrel detection and classification
      
      - label and classificiation the pixel
      - estimate if it is a barrel or not.

   2. SLAM using 2D laser scanner
      
      - Particle filter

   3. Visual Odometry using camera and IMU
      
      - camera model
      - EKF

2. ECE 276B
   
   1. rock-scissor-paper
      
      - maximum likelihood.
      - Markov Decision Process.

   2. 3D path planning using search-based methods and sample-based methods.
      
      - A*
      - RRT
      - Bidirectional RRT

   3. Optimal decision and Reinforcement learning.
      
      - Mountain car problem using reinforcement learning.
      - Inverted pendulum modeling and control.

3. ECE 271C

   - KNN network implementation.
   - single layer network back propagation using numpy.
   - multi layer network back propagation using numpy.
   - deep network training, fine-tuning using pytorch.


## learning and testing

1. tensorflow

   learning google machine learning crash course and tensorflow keras.

2. python_tutorial

   learning official tutorial in python documentation.
  
3. python_testing

   pytest, unitest, doctest from pythontesting.net.

4. mp

   test of multi-processing.

## patterns

1. profiling
2. multi-processing
3. testing
4. 3D display
5. numpy operations
6. vectorization
7. file reading
8. object saving and loading
9. argument parsing