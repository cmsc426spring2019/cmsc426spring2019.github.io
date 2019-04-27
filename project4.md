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

<a name='system_overview'></a>
## Implementation Overview

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
