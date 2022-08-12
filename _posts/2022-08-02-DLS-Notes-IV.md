---
layout: post
title: (Google ML Bootcamp) Notes on DLS Coursera - IV
categories: [coding, ML]
---


# Course 4 - Convolutional Neural Networks

* $n \times n$, $f \times f$ filter, using stride=1
    * Any padding p: n -> n+2f-f +1
    * Same: Output is the same size as the input 
    * Valid: No padding, $n - f +1 \times n - f + 1$
    * f is usually odd due to the padding, also it's nice to have a central pixel in the filter.
* Using the stride s: n -> $\frac{n + 2p - f}{s} + 1$
* Usually layers are layers that have weights, maxpool for example is not counted towards the number of layer in the CNN


#### Case Studies

* Usually the width and height goes down and the features number goes up (by 2 as VGG for reference)
* ResNets: Residual Network as a solution for vanishing gradient.
    * We learn the identity + first approximation, so  we add these L and L+1 layers is doesn't hurt performance.
    * Layer L+1: $a^{[L]} \rightarrow z^{[L+1]} = g^{[L]}(W^{[L+1]} a^{[L]} + b^{[L+1]}) $
    * Layer L+2:  $a^{[L+1]} \rightarrow z^{[L+2]} = g^{[L]}(W^{[L+2]} a^{[L+1]} + b^{[L+2]} + a^{[L]})$
    * If there is a mismatch between $a^{[L]]}$ and $a^{[L+1]]}$, we could have  $a^{[L+1]} \rightarrow z^{[L+2]} = g^{[L]}(W^{[L+2]} a^{[L+1]} + b^{[L+2]} + W_s a^{[L]})$ where $W_s$ can be fixed or learned.

* 1x1 Convolutions: 
    * We are applying a FC layer to each pixel and their channels.
    * We can shrink the number of channels.
    * As the number of channel it's also the channel size of the filter, if the number of filters is big and also the number of channel, the computational cost can go up dramatically. 

* Inception Network:
    *  Concatenate different filters in the same layer.  
    * It takes the previous activation values and then computes different 1x1 convs with differents channels as a previous step for the filter. We could put a maxpool too. Then we concatenate the outputs of each set of filters.
    * It has different sidebranches, it takes a middle layer and uses it as an output layer, it calculates the backprop from them and adds them the the "main" backpropr from the real output.
    * In a CNN (such as Google's Inception network), bottleneck layers are added to reduce the number of feature maps (aka channels) in the network, which, otherwise, tend to increase in each layer. This is achieved by using 1x1 convolutions with fewer output channels than input channels. (from SO)

* MobileNet:
    * It uses a depthwise and pointwise convolution to reduce the number of calculations it performs. It loses information between the pixel in different channel directly. It retrives this "lateral channel" information only for a single pixel and its channels.
    * v2: It has a residual conection as well as two sets of 1x1 filters, expansion and projection. The first enlarges the input value, then it goes throught by the depthwise conv and then the projection 1x1 convolution does the same as the pointwise in reducing the depthwise dimensions.

* EfficientNet:
    * Most DLNs can be roughly described as 3 parameters: input resolution (r), layers vertical width (w) e.g. kernel size and network depth (d). There is a tradeoff between these characterictics for an efficient use of resources.

## State of Computer Vision
* I need to study more about engineering.
