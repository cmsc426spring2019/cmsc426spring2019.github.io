---
layout: page
mathjax: true
title: Image Classification Using Bag of Features and Support Vector Machines
permalink: /2019/hw/hw3/
---



Table of Contents:
- [Due Date](#due)
- [Introduction](#intro)
- [Part 1: Implementation](#part1)
- [Part 2: What to submit](#part2)
- [Submission Guidelines](#sub)
- [Collaboration Policy](#coll)

<a name='due'></a>
## Due Date 
11:59 PM, Saturday, April 27, 2019

<a name='intro'></a>
## Introduction
In this homework you will implement an image classifier.You will be building Support Vector Machine (SVM)
classifier to classify images of MNIST digits dataset.
Supervised classification is a computer vision task of categorizing unlabeled images to different categories or
classes. This follows the training using labeled images of the same categories. You will be provided with a data
set of MNIST digits. All of these images will be specifically labeled as being one of the 10 digits, 0-9. You would
use these labeled images as training data set to train SVM classifier. The classification would be one-vs-all, where
you would specifically consider one digit at a time to classify and consider it as a positive example and all other
digits’ images as negative examples. Once the classifier is trained you would test an unlabeled image and classify
it as one of the 10 digits. This task can be visualized in Figure 1

<div class="fig fighighlight">
  <img src="/assets/hwk3/hwk-steps.png" width="100%">
  <div class="figcaption">
  </div>
  <div style="clear:both;"></div>
</div>


<a name='part1'></a>
## Part 1: Implementation (50 pts)


There are three steps to this approach.

## Visual Vocabulary

Use Speeded up robust features (SURF) to find a feature descriptor followed by K-means to obtain a visual
vocabulary. The number of k-means clusters is the size of our visual vocabulary and the size of our features. Go
over the slides to understand SURF, K-Means algorithm and bag of features. For a detailed description of SURF
read the the paper, “SURF: Speeded Up Robust Features" by Bay et al. See bagOfFeatures command in Matlab.

## SVM Classifier Training

Train SVM on the resulting histograms (each histogram is a feature vector, with a label) obtained as a visual vocabulary in the previous step. For a thorough understanding of SVM, refer to the heavily cited paper, “A Tutorial on
Support Vector Machines for Pattern Recognition", by Christopher Burges. You can also look at this medium article
<a href="https://medium.com/machine-learning-101/chapter-2-svm-support-vector-machine-theory-f0812effc72"> https://medium.com/machine-learning-101/chapter-2-svm-support-vector-machine-theory-f0812effc72</a>.

You would need to train the classifier as a one vs. all. 
See Matlab commands, multisvm and trainImageCategoryClassifier.

## Test your model

Apply the trained classifier to the test image. Here you would test it the following two ways:

- Extract the bag of features for the test image and then pass it as an input to the model you created during
training, and,
- Pass the test image directly to the SVM model without any feature extraction.

See Matlab command predict.


<a name='part2'></a>
## Part 2: - What to submit (50 points)

1. Show a 10 × 10 confusion matrix with digits from 0-9 as its rows and columns. It is used to determine the
accuracy of your classifier. In this matrix the rows are the actual digit label and the columns are the predicted
label. Each cell in this matrix will contain the prediction count. Ideally, we would like all the off-diagonal
numbers in this matrix to be 0’s, however, that is not always possible. For example in the matrix below with
100 images of each of the three digits, 0, 1, 2,
<div class="fig fighighlight">
  <img src="/assets/hwk3/table.png" width="50%">
  <div class="figcaption">
  </div>
  <div style="clear:both;"></div>
</div>
the confusion matrix can be read as, digit 0 was correctly classified as a 0, 93 times, and wrongly classified as
1 and 2, two times and five times, respectively. Similarly, digit 1 was correctly classified 98 out of 100 times
and digit 2 was also correctly classified 98% of the time.

2. A plot showing the histogram of the visual vocabulary during the training phase. You can pick any digit you
like.

3. Explain in one or two paragraphs your observations about the prediction of a test image, with and without
extraction of the bag of features.


<a name='sub'></a>
## Submission Guidelines

File tree and naming
Your submission on Canvas must be a zip file, following the naming convention YourDirectoryID_hw3.zip. For
example, xyz123_hw3.zip. The file must have the following directory structure, based on the starter files
- mysvm.m
- report.pdf


### Report

Please include the plot and confusion matrix as mentioned in part 2. Also include your observations about the
prediction of test image.
As usual, your report must be full English sentences,not commented code

<a name='coll'></a>
## Collaboration Policy
You are encouraged to discuss the ideas with your peers. However, the code should be your own, and should be the result of you exercising your own understanding of it. If you reference anyone else's code in writing your project, you must properly cite it in your code (in comments) and your writeup.  For the full honor code refer to the CMSC426 Spring 2019 website
