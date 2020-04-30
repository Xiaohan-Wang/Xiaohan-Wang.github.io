---
layout:     post
title: DA dataset summary
subtitle:   
date:       2020-04-02
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Datasets
---

### Image classification
#### Numbers
##### Mnist
##### USPS
##### SVHN (street view house numbers)

#### Office
#### Office-31
It contains 4652 images organized in 31 classes from three different domains: Amazon (A), DSRL (D) and Webcam (W).
#### Office-Caltech
It selects the subset of 10 common categories in the Office31 and the Caltech256 datasets. It contains 2533 images of which about half belong to Caltech256. Each of Amazon (A), DSLR (D), Webcam (W) and Caltech256 (C) are regarded as separate domains.


### Image segmentation

#### GTA5 (synthetic dataset)
[homepage](https://download.visinf.tu-darmstadt.de/data/from_games/)

GTA is a synthetic, vehicle-egocentric image
dataset collected from the open world in the realistically rendered computer game Grand Theft Auto V (GTA, or GTA5). It contains 24,996 images, whose semantic segmentation annotations are fully compatible with the classes used in Cityscapes.

#### synthia (synthetic data)
[homepage](http://synthia-dataset.net/)

SYNTHIA  is a large dataset of synthetic images and provides a particular subset, called SYNTHIA-RANDCITYSCAPES, to pair with Cityscapes. This subset contains 9,400 images that are automatically annotated with 12 object categories, one void class, and some unnamed classes. Note that the virtual city used to generate the synthetic images does not correspond to any of the real cities covered by Cityscapes.

Note: usually consider the 16 common classes shared with Cityscapes: sky, building, road, sidewalk, fence, vegetation, pole, car, traffic sign, person, bicycle, motorcycle, traffic light, bus, wall, and rider.

#### Cityscapes  
[homepage](https://www.cityscapes-dataset.com/)

a real-world, vehicle-egocentric image dataset collected in 50 cities in Germany and nearby countries. It provides four disjoint subsets: 2,993 training images, 503 validation image, 1,531 test images, and 20,021 auxiliary images. All the training, validation, and test images are accurately annotated with per pixel category labels, while the auxiliary set is coarsely labeled. There are 34 distinct categories in the dataset.

Note: usually consider the 19 common classes shared with Cityscapes: bike, fence, wall, traffic sign, pole, motorcycle, traffic light, sky, bus, rider, vegetation, **terrain**, **train**, building, car, person, **truck**, sidewalk and road.

### multi-source domain adaptation
#### DomainNet
1. [homepage](http://ai.bu.edu/M3SDA/) 
2. Challenge: [VisDA-2019](http://ai.bu.edu/visda-2019/)


