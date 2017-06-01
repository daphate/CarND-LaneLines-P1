# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

First, I desided to use grayscale as it was prompted by cource, but later i've added HSV conversion and masking routine.
I subsecuently use hsv masking, gaussian blur with kernel of 3, canny with thresholds of 50 and 150.
These transformations are done by image_preprocess_hsv function.

I've created helper class Line, which computes slope and intercept, x coord by y and vice versa and can update line coords 
for future use when adopting lane lines to vanishing point.

I've created the first pipeline for checking on images, which finds hough lines and draws it in some kind of thumbnail.

Then i've created a smarter pipeline, which inits lines as instances of Line class and filters almost horisontal and
almost vertical outliers, computes median slopes and intercepts for all candidates to be segments of the lane line,
and computes left and right lane lines. Then it finds the vanishing point as inersection of left and right lane lines
and updates their coordinates respectively to appear lower than the vanishing point.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be because my knowledge of python doesn't allow me to use buffers to 
compare new candidate lane lines to previously found, so for now it cannot filter lane line candidates that are too far from
previously computed lane lines. So the filter works ok on very simple scenes, but will fail on challenge.

Another shortcoming is that the preprocessing will for sure fail on different lighting and wheather and road painting color 
conditions because it only can mask yellow and white lines.

Also it won't work well on curvy lane lines, it cannot predict changes of lane line curvature, will fail if we'll try to switch the lane
and many more.


### 3. Suggest possible improvements to your pipeline

As far as I understood the focus of this task, it's intended to learn how to use image filters, pipelines, and so on.
I'm short of time, but surely I'd add lane lines history to make new lane line candidate detection and adoption smoother.
My code is pretty dirty, so it can be refactored and simplified.
The visualisation is not much informative yet, but i've learned how to use some of cv2, create thumbnails, use different filters
and learned some python.

