# UAY-INVECAS-IITH

This repo contains all the work done at LFOVIA, IIT Hyderabad as part of UAY project titled "Low Cost Design & Manufacture of Indigenous 24 GHz and 77 GHz Retrofittable Automotive Radar for Road Safety and Monitoring Driving Behaviour".

## Abstract

Autonomous and semi-autonomous navigation systems use multiple sensors for perception. Amongst all the sensors, the most prominently used are camera, lidar and radar. Camera and lidar are comparatively more expensive than radar. Also, camera and lidar fail to operate smoothly in adverse weather conditions. Radar, on the other hand, can operate in a wide range of temperature and weather conditions. Given radar's capabilities and recent advancements in deep learning, can a low-cost and robust perception solution be achieved? To address this, we make the following contributions via this work. We present a novel 77 GHz automotive radar dataset composed of both static and moving objects combined with a detailed analysis of the proposed dataset. We also propose using a novel $7 \times 5$ object representation framework for automotive radar data based object classification. We design a lightweight CNN architecture to classify objects present in the automotive radar scene and demonstrate that the proposed CNN delivers strong performance on our dataset. Additionally, we also experiment with the convLSTM architecture to exploit temporal characteristics present in the radar data. Further, we evaluate the performance of standard machine learning algorithms on the proposed dataset. Furthermore, we show that our CNN can also perform well on an open-source automotive radar dataset.

## Table of Contents
 - Dataset : The Dataset is present in the Radar_Dataset folder.
 | Object            | Sequences| Frames/seq | Arrays/seq |
 | -----------------:|:--------:|:----------:|:----------:|
 | Car Vertical      |    64    |    614     |    5895    |
 | Car Horizontal    |    22    |    441     |    3758    |
 |     Bike          |    13    |    951     |    8792    |
 |     Human         |    21    |    388     |    2688    |
 |  Human-moving     |    17    |    992     |    9457    |

## Results 

 // Add frames of radar data (128x64)
 
 
## Installation and dependencies

## Usage





