---
layout: page
mathjax: true
title: Deep Learning
permalink: /2019/proj/p4/
---

## UNDER CONSTRUCTION.

Table of Contents:
- [Deadline](#due)
- [Introduction](#intro)
- [Implementation Overview](#system_overview)
- [Submission Guidelines](#sub)
- [Collaboration Policy](#coll)

<a name='due'></a>
## Deadline 
11:59 PM, May 17, 2019

<a name='intro'></a>
## Introduction
In this project you will implement a convolutional neural network (CNN). You will be building a supervised classifier to classify MNIST digits dataset.  

Supervised classification is a computer vision task of categorizing unlabeled images to different categories or classes. This follows the training using labeled images of the same categories. You will be provided with a data set of images of MNIST digits. All of these images will be specifically labeled as a specific digit. You would use these labeled images as training data set to train a convolutional neural network. Once the CNN is trained you would test an unlabeled image and classify it as one of the ten digits. This task can be visualized in Figure 1.

<div class="fig fighighlight">
  <img src="/assets/proj4/mnist.png" width="100%">
  <div class="figcaption">
  </div>
  <div style="clear:both;"></div>
</div>

## Architecture
Your training and test step would contain the pipeline shown in Figure 2

<div class="fig fighighlight">
  <img src="/assets/proj4/architecture.png" width="100%">
  <div class="figcaption">
  </div>
  <div style="clear:both;"></div>
</div>
You are provided a framework for a single convolution layer (convolution + subsampling), a fully connected neural network with Sigmoid activation function, and a cross-entropy softmax layer with ten outputs.  Next few sections present a description of each of these components of this network. 

## Fully Connected Layer
In a fully connected layer each neuron is connected to every neuron of the previous layer as shown in Figure 3
<div class="fig fighighlight">
  <img src="/assets/proj4/fullyconnected.jpg" width="40%">
  <div class="figcaption">
  </div>
  <div style="clear:both;"></div>
</div>

Each of these arrows (inputs) between the layers is associated with a weight. All these input weights can be represent by a 2-dimensional weight matrix, <b>W</b>. If the number of neurons in this layer is n<sub>c</sub> and the number of neurons in the previous layer is n<sub>p</sub>, then the dimensionality of the weight matrix <b>W</b> will be n<sub>c</sub> x n<sub>p</sub>. There is also a bias associated with each layer. For the current layer we will represent it by a vector, \textbf{b},  with a size of n<sub>c</sub> x 1. Therefore, for a given input, <b>X</b>, the output, <b>Z</b>, of a fully connected layer is given by the equation:

Z = WX + b

## Convolutional layer
We will begin with a brief description of cross-correlation and convolution which are fundamental to a convolutional layer. Cross-correlation is a similarity measure between two signals when one has a time lag, represented in the continuous domain as

<img src="/assets/proj4/crossCorrEq.jpg" width="40%">

Convolution is similar, although one signal is reversed

<img src="/assets/proj4/conv.jpg" width="25%">

They have two key  features, shift invariance and linearity. Shift invariance means that the same operation is performed at every point in the image and linearity means that every pixel is replaced with a linear combination of its neighbors.

In a convolutional layer an image is convolved with a filter. For example a 3 x 3 filter can be represented as

<img src="/assets/proj4/filter.jpg" width="25%">

Each number in this filter is referred to as a weight. The weights provided in this filter are example weights. Our goal is to learn the exact weights from the data during convolution. For each convolution layer a set of filters is learned. Use of convolution layer has many features but two stand out:
<ul>
<li> Reduction in parameters<br>
  In a fully connected neural network the number of parameters is much larger than a convolution network. Consider an image of size 5 x 5 to be convolved with a filter of size, 3 x 3. The number of weights we would have to learn would be the total number of weights in the filter, which is, 9. On the contrary for the same image, using a fully connected layer would require us to learn 225 weights. This is demonstrated in below Figure
  
  <img src="/assets/proj4/params.jpg" width="100%">
  </li>
  <li> Exploitation of spatial structure <br>
  Our images are in two-dimensions. In order to use them as an input to a fully connected layer, we need to unroll it into a vector and feed it as an input. This leads to the increase in the number of parameters to be learned as shown in the previous section and loss of the original 2D spatial structure. On the contrary, in convolution layer we can directly convolve a 2D image with a 2D filter thereby preserving the original spatial structure and also reducing the number of parameters to be learned.
  </li>
  </ul>

<a name='system_overview'></a>
## Implementation Overview
Convolution involves multiplying each pixel in an image by the filter at each position, then summing them up and adding a
bias. The figure below shows a single step of convolving an image with a filter. Each convolution will return a 2D matrix output for each input channel.

<img src="/assets/proj4/convolution.jpg" width="60%">

### Code

<a name='sub'></a>
## Submission Guidelines
<b> We will deduct points if your submission does not comply with the following guidelines.</b>

Please submit the project <b> once </b> for your group -- there's no need for each member to submit it.

### File tree and naming

### Report

<a name='coll'></a>
## Collaboration Policy
We encourage you to work closely with your groupmates, including collaborating on writing code.  With students outside your group, you may discuss methods and ideas but may not share code.  

For the full collaboration policy, including guidelines on citations and limitations on using online resources, see <a href="http://prg.cs.umd.edu/cmsc426">the course website</a>.
