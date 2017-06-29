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

### 4. Possible applications

Other than the most obvious application of trying to build a fully autonomous car there are certain low hanging fruits that could be covered.
- Detecting and warning the driver when swerving away from the lane. Could be done using a simple mobile phone detecting the lane real-time and using the car indicator noise to know if the lane switch was intentional or distraction
- Car insurance companies could base their insurance premium for the drivers based on their driver behavior detected directly through their mobile phone. Using the camera sensor and running a light weight detection algorithm like this could provide a game changing benefit
- Using AR to show the turns directly on the lanes
- Obstacle detection on the driving lane. Detecting any mechanical part that might have fallen on the road

