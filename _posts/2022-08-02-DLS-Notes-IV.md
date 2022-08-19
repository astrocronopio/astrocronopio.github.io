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


## Case Studies

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




## What you should remember:

* MobileNetV2's unique features are:
    * Depthwise separable convolutions that provide lightweight feature filtering and creation
    * Input and output bottlenecks that preserve important information on either end of the block
    * Depthwise separable convolutions deal with both spatial and depth (number of channels) dimensions

    *  From the network:
    ```
    base_model = tf.keras.applications.MobileNetV2(input_shape=None,
                              include_top=None, # <== Important!!!!
                              weights=None) # From imageNet
    ```

## What you should remember:

* To adapt the classifier to new data: Delete the top layer, add a new classification layer, and train only on that layer
* When freezing layers, avoid keeping track of statistics (like in the batch normalization layer)
* Fine-tune the final layers of your model to capture high-level details near the end of the network and potentially improve accuracy


## Object Localization
* There is a object/background flag in the output, the probability that there is an object, probability of detection
* Landmarks detection: points must be consisted among output/samples
* Sliding window is a method that output 1/0 if an object is there. This can be done with a convnet to check all windows in one sweep.
* YOLO is amazing, the output is a tensor of the data for a section of the input image grid.
* The dimensions of the box is relative to its place inside the grid, i.e 0.75 the width and 1.1 the height, these values can be over 1 but they can't be negative.
* Metric: Intersection over Union
    ![Beautiful](/media/posts/iou.png)
* Non-Max Supression:
    * Suppresses the boxes with high probability of dectection around the highest probability.
    * The chance is non negligible over 0.6
    * Calculate the IOU to measure the overlap between the boxes, then discard the boxes with IoU over 0.5.
    * Repeat for every object.
* Anchor Box Algorith: Overlapping objects
    * The output target is larger as it fits now two sets of boxes.
    * e.g. Anchor box 1 is a vertical box and 2 is  horizontal
    * There are two objects in the same grid cell. 
    * It helps to specialize in detecting 
* Semantic Segmantatio U-Net
    * Transpose Convolution: Remember once you read about Anime Girl GAN? It's a way to "un-do" the convolution. It uses padding, strides and filter similar to a simple convolution, except you take a value from the input, multiple by the whole filter going from a 1x1 to fxf.
    * The first part of the network compresses the input.
    * The second part uses transpose convolution to return to the original dimensions, but it has skipped connections from the early layers to the last layers for the details.


## What you should remember:

- Semantic image segmentation predicts a label for every single pixel in an image
- U-Net uses an equal number of convolutional blocks and transposed convolutions for downsampling and upsampling
- Skip connections are used to prevent border pixel information loss and overfitting in U-Net


    <!-- * The YOLO algorithm:
    * Input
    *  -->