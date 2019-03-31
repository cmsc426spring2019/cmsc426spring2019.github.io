---
layout: page
mathjax: true
title: Segmentation
permalink: /2019/proj/p3/
---

Table of Contents:
- [Deadline](#due)
- [Introduction](#intro)
- [Implementation Overview](#system_overview)
- [Submission Guidelines](#sub)
- [Collaboration Policy](#coll)

<a name='due'></a>
## Deadline 
11:59PM, Thursday, April 11, 2019

<a name='intro'></a>
## Introduction
In this project, we'll implement a graph-based segmentation algorithm, based on Mishra et al.'s
["Active Segmentation with Fixation"](https://ieeexplore.ieee.org/abstract/document/5459254).  You'll understand how segmentation can be framed as a min-cut on a graph, and explore how different image features can be used to assign weights to that graph.

This document just provides an overview of what you need to do.  For a full breakdown of how each step in the pipeline works, <b>see <a href="https://cmsc426spring2019.github.io/graphseg/">the course notes for this project</a></b>.

<a name='system_overview'></a>
## Implementation Overview:
In fixation-based graph-cut segmentation, the user provides a "fixation point" which identifies the
target object.  The image is considered to be a graph, where pixels are vertices, each connected to
its four adjacent neighbors.  Segmentation proceeds in two rounds: in the first round, we weight the
graph using only an edge probability map (for this project we've provided these for you, but they
can easily be found using an algorithm like gPb).  The second round refines this using image
features such as color, texture, and (for sequences) optical flow.  (For more details, see the course
notes.)

### What you need to do:
- **First segmentation** (binary weights): set up the maxflow graph based on the image and its
  boundary probability map (in "<imgName\>\_gPb.mat").  Edges are weighted based on the boundary map, _and_ the edge's distance from the fixation point.
    - (**EXTRA CREDIT**: refine the boundary probability map using the optical flow-based method described in section 3 of Mishra et al.)
    - result: rough initial segmentation of the object.
- **Generate texture response maps**: as described in the course notes, generate a "texture descriptor"
  for each pixel in the image.  (For this project, a simple filter bank using oriented derivative of gaussians is fine.)
    - (For sequences you must also generate optical flow, but this is just a function call.)
- **Second segmentation** (unary weights): reweight the graph using some combination of color, texture,
  and optical flow.  The process is very similar for all of them: 
   1. Use the rough segmentation from step one to identify foreground and background pixels (in the
      texture response map, the optical flow map, etc.).
   2. Train two separate GMMs: one to classify foreground pixels, and another to classify backround
      pixels.
   3. Use the GMM's to calculate the Log probability of each pixel being in the
      foreground/background.
   4. Weight the graph based on this probability map, and resegment.

### Point Distribution:
 - First segmentation: 30pts
    - (EXTRA CREDIT - Internal edge suppression: +20pts)
 - Texture response map: 15pts
 - 2nd segmentation (for single images) using color features: 35pts
 - 2nd segmentation (for single images) combining color AND texture features: 10pts
 - 2nd segmentation (for _sequences_) using optical flow AND color+texture: 10pts
 - (EXTRA CREDIT - custom images/sequences: +5pts)

## Project Files

Please download the starter code
[here](https://drive.google.com/open?id=1cHpODG8Vfgt9P8wH1jIK18QT-ahLjDIP).

Files to modify:

  - segment.m – main function, implementing segmentation
  - computeUnaryWeights.m – compute unary weights from flow/texture/color features.
  - getTextureResponses.m – generate an image’s texture response map.
  - segment_demo#.m – examples of using segment.m for segmenting single images and image sequences.

Utilities – modify at your peril:

  - imRegionHighlight.m, subplot_tight.m
  - img_utils/\* – helpful scripts for processing new videos/images, so they work with your code. Specifically: splits videos into individual frames, and then computes a gpb edge probability map for each frame.
  

Included libraries:

  - maxflow.zip - contains a library for max-flow/min-cut, and matlab bindings for it.
     - ([Library source](http://mouse.cs.uwaterloo.ca/code/maxflow-v3.01.zip), [bindings
       source](https://www.mathworks.com/matlabcentral/fileexchange/21310-maxflow).)


#### Making your own input images
If you'd like to try your code on other images/videos, you'll need to generate edge probability
maps for them.  Use [Berkeley's gPb library](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/BSR/BSR_code.tgz) to do so.  See `custom_img_utils/get_gpb_edges2.m` for an example of how to do this.  Additionally, you can use `custom_img_utils/get_video_frames.m` to extract the frames from a video.


#### Functions Allowed 

For calculating the texture response map:  you must generate the filters manually.  So, you **cannot** use `fspecial` or similar.  You may find `imrotate` useful for making different orientations of filter.  Of course, `conv2` and `imfilter` are allowed. 

For this project, you **are** allowed to use matlab's `fitgmdist` for your GMM's.  You may find
functions like `mvnpdf` useful as well.

You are encouraged to use Matlab's built-in optical flow functionality.  See
`custom_img_utils/get_video_frames.m` for an example.


#### Some Implementation Details

For an nxm image:
  -   Unary weights are represented as a nm x 2 matrix $$T\_$$ : for
      each pixel \[Foreground weight, background weight\].
  -   Binary weights are represented as a nm x nm matrix A: each
      pixel’s connection to every other pixel. This is a constraint of
      the maxflow library we’re using; we’re only considering each
      pixel’s connection to its neighbors, so A is mostly empty.

<a name='sub'></a>
## Submission Guidelines
<b> We will deduct points if your submission does not comply with the following guidelines.</b>

Please submit the project <b> once </b> for your group -- there's no need for each member to submit it.

### File tree and naming

Your submission on Canvas must be a zip file, following the naming convention **YourDirectoryID_proj3.zip**.  For example, xyz123_proj3.zip.  The file **must keep the same directory structure as the starter code.**  Include your report, **report.pdf**, in the same directory as your code.  Include any custom images in the Images/ folder.  Include a result video `Results/sequence#.avi` for each of the sequences (use Matlab's VideoWriter for this). 

### Report
**You will be graded primarily based on your report.**  We want you to demonstrate an understanding of the concepts involved in the project, and to show the output produced by your code.

Logistics and bookkeeping you **must** include at the top of your report (-5 points for each one that's missing):
 - The name of each group member. 
 - A brief (one paragraph or less) description of what each group member contributed to the project.

Your report should:

 - Explain briefly what you did at each step.  Assume that we're familiar with the project: don't repeat what's already in the course notes.  Instead, focus on any interesting problems you encountered and/or solutions you implemented.
 - Compare the initial edge-based segmentation to the second to the second, texture/color/flow-based segmentation.  Include images of both steps, for at least one of single images, and at least two frames from one of the sequences.
    - (If you did the extra credit, internal-edge suppression, include visualizations of the results of this, too.)
 - Include final results for all of the single images (from the training set and test set).
    - For each, include results testing using color and texture separately, and also using a weighted combination of both.
 - Include final results for all sequences (training and test sets):
    - For each sequence, include a sub-sequence of four frames in your report with detailed results:  testing using color, texture, and flow separately, and then using a weighted combination of all three.
    - Additionally, use Matlab’s videowriter to create videos of your results for the full sequences: Results/sequence1.avi and Results/sequence2.avi

As usual, your report must be full English sentences, **not** commented code. There is a word limit of 1500 words.


<a name='coll'></a>
## Collaboration Policy
We encourage you to work closely with your groupmates, including collaborating on writing code.  With students outside your group, you may discuss methods and ideas but may not share code.

For the full collaboration policy, including guidelines on citations and limitations on using online resources, see <a href="https://cmsc426spring2019.github.io/index.html">the course website</a>.

