# **Finding Lane Lines on the Road**

## Writeup

### This is a reflection on the observation based on the attempt to find lanes
##

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/anim/flow.gif "Grayscale"

---

### Reflection

### 1. The pipeline 

Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I ....

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image:

[Pipeline]: ./test_images_output/anim/pipeline.png

[Flow]: ./test_images_output/anim/flow.gif

![alt text][image1]


### 2. Potential Shortcomings
- Rain/Snow/
- Changing brightness/Shadows
- Night time
- Physical damage that could offset the camera's position
- Inclination/Declination
- Switching lanes
- Overfit to the dataset that has been used here

One potential shortcoming would be what would happen when ...

Another shortcoming could be ...


### 3. Possible improvements

Divide the lane line detection problem. Try to detect the left line of the lane separately and right line of the lane separately.
Constructing a polygon that trims out the left and right line of the lane could provide better result than trying to have one polygon region to cover both. Once the trimming is done separately the Hough transform function could be run on the individual image to identify the lines. Using numpy(or any other library) one could merge the two images with individual lane lines.

