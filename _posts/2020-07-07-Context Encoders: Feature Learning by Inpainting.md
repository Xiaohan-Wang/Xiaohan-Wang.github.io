---
layout:     post
title: Context Encoders:_Feature Learning by Inpainting
subtitle:   CVPR 2016
date:       2020-7-7
author:     Xiaohan
header-img: img/ice.jpg
catalog: true
tags:
    - Self-supervision
---

[Paper link](https://arxiv.org/pdf/1604.07379.pdf) and [website](http://people.eecs.berkeley.edu/~pathak/context_encoder/)

[//]: #(<img src="" width="100%" height="100%">)

#### Take away message
1. Image inpainting: 
    * to fill in large missing areas of the image, it can’t get “hints” from nearby pixels
    * a model needs to both understand the content of an image, as well as produce a plausible hypothesis for the missing parts
2. **a standard pixel-wise reconstruction loss**: only the reconstruction loss produces blurry results
3. **an adversarial loss**: adding the adversarial loss results in much sharper predictions

#### Model
1. Encoder-decoder pipeline:
    * encoder: produces a latent feature representation of that image
    * decoder: takes this feature representation and produces the missing image content
        * a series of five up-convolutional layers (upsampling followed by convolution)
    * **channel-wise fully-connected layer**: connect the encoder and the decoder
        * directly propagate information from one corner of the feature map to another corner (so that we can better capture global semantic information)
        * essentially a fully-connected layer with groups: only propagates information within feature maps, but it has no parameters connecting different feature maps
2. Loss function:
    * reconstruction (L2) loss: 
        <img src="/img/15942152334674.jpg" width="50%" height="100%">
        * capturing the overall structure of the missing region and coherence with regards to its context, but prefer a blurry solution (because the expectation of all possible values minimizes the mean squared pixel-wise error)
    * adversarial loss: 
        <img src="/img/15942164552075.jpg" width="55%" height="100%">
        * tries to make prediction look real, and has the effect of picking a particular mode from the distribution
        
3. Region masks
    <img src="/img/15942173051541.jpg" width="60%" height="100%">

    * central region
    * random block
    * random region (recommended)
    
    Random block and random region produce a similarly general feature, while significantly outperforming the central region features.
    
#### Experiments
##### Implementation detail
Pool-free encoders: replacing all pooling layers with convolutions of the same kernel size and stride. (Intuitively, there is no reason to use pooling for reconstruction based networks.)

##### Evaluation
1. Semantic Inpainting
<img src="/img/15942140401143.jpg" width="90%" height="100%">
    * The encoder and discriminator architecture is similar to that of discriminator in [1], and decoder is similar to generator in [1].
1. Feature Learning
    <img src="/img/15942140603053.jpg" width="90%" height="100%">
    * For consistency with prior work, this paper use AlexNet as its encoder in this part.
    * The authors did not manage to make the adversarial loss converge with AlexNet, so they used just the reconstruction loss.
    
    ![-w892](/img/15942180841172.jpg)


#### Further reference 
1. A. Radford, L. Metz, and S. Chintala. Unsupervised representation learning with deep convolutional generative adversarial networks. ICLR, 2016.