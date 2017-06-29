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

[pipeline]: ./test_images_output/anim/pipeline.png "Pipeline"

---

### Reflection

### 1. The pipeline 

Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

#### The steps

##### Step 0 : Read the image
Reading the raw image that has been feed to the system. The pixel values are converted into an array shaped based on the dimensions of the image and the color channel

##### Step 1 : Convert to Grayscale
Using Open CV library we convert the image to a grayscale image. We do this since we are only interested in detecting the lines of the lane and any other extra information would be just a distraction for the algorithm

##### Step 2 : Canny edge detection
We run the gray image through a Canny edge detection with a tuned low and high threshold parameters. The output from this step is an image that contains a lot of edges

##### Step 3 : Gaussian blur
Not all edges are interesting for us. Edge detection could produce a lot of noise and we want to reduce them. Running through a Gaussian function blurs the image and only prominent edges stay alive

##### Step 4 : Trimming
Now we define a region of interest on the image as a polygon. Only edges that fall within its area gets selected and rest gets rejected.
The Polygon acts as a filter

##### Step 5 : Hough Transform
Using Hough transformation we detect the lines from edges within the region of image that we have trimmed. By varying the rho, theta, threshold, minimum line length and maximum line gap we find the best parameters to detect our lane lines. We use draw_lines() internally in this function to imprint the lines onto the image

##### Step 6 : Superimpose result
Using cv2's addWeighted function we superimpose the Hough lines onto the original image. This lets us visualize the lanes

#### Modification to draw_lines() function
The original draw_lines() function simply loops through all the detect lines from Hough transform and draw them on the image. This could look noisy since it doesn't elliminate the lines that are really not lanes.
Simply by computing the slope of each line m = (y2-y1)/(x2-x1) helps us detect if the line is representative of the left lane or right lane. 
We simply ignore the lines that have a zero slope or if its value falls in a range that is unlikely representation of the lane.
Using the extreme 'Y' axis points we find out the corresponding x-coordinate at those extreme points. We use these points to draw the left and right lane. Once we draw the lanes we break the loop. This method potentially reduces the number of times the loop has to execute. We break the main loop when both the lines are drawn.

![Pipeline Figure][pipeline]



### 2. Potential Shortcomings
The pipeline fails when the terrain is even a little unpredictable. The algorithm completely relies on only the 2D image that lacks the steroscopic vision capability of a human eye. The algorithm assumes the camera mount and its angle of detection. Any change in the perspective would distort the detection. Another major shortcoming is the pipeline parameters has been trained with only the dataset that is available here.
#### Things that could cause the pipline to fail
- Rain/Snow
- Changing brightness/Shadows
- Night time
- Physical damage that could offset the camera's position
- Inclination/Declination
- Switching lanes
- Bumpy road
- Poorly marked lanes
- Lanes that got painted back
- Reflection of sunlight on the lane marking

### 3. Possible improvements

Divide the lane line detection problem. Try to detect the left line of the lane separately and right line of the lane separately.
Constructing a polygon that trims out the left and right line of the lane could provide better result than trying to have one polygon region to cover both. Once the trimming is done separately the Hough transform function could be run on the individual image to identify the lines. Using numpy(or any other library) one could merge the two images with individual lane lines.

### 4. Possible applications

Other than the most obvious application of trying to build a fully autonomous car there are certain low hanging fruits that could be covered.
- Detecting and warning the driver when swerving away from the lane. Could be done using a simple mobile phone detecting the lane real-time and using the car indicator noise to know if the lane switch was intentional or distraction
- Car insurance companies could base their insurance premium for the drivers based on their driver behavior detected directly through their mobile phone. Using the camera sensor and running a light weight detection algorithm like this could provide a game changing benefit
- Using AR to show the turns directly on the lanes
- Obstacle detection on the driving lane. Detecting any mechanical part that might have fallen on the road

