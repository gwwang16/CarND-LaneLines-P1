# **Finding Lane Lines on the Road** 

## Writeup Template

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # "Image References"

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./doc_images/output_initial_pipeline.png
[image3]: ./doc_images/output_final_pipeline.png
---


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My initial pipeline consisted of 5 steps.
- Convert the images to grayscale
- Smooth images using Gaussian blur function
- Detect edges using canny operator
- Find lane  lines using  hough transform in  region of interest (RIO)
- Combine line image and original image

Here is the output of  my initial pipeline: 
![alt text][image2]

To  extrapolate these lane lines segments and draw them onto the image, I implemented an advanced pipeline function followed by above initial pipeline.
- Calculate slopes of  lines from `hough_lines()`, remove all lines with abosulte slope <  0.5, define lines with positive slope as left lane lines and others are right lane lines.
- Calculate average values of the 5 longest lines to be the final lane lines  slopes
- Draw two lane lines

Here is the output of my final pipeline:
![alt text][image3]

As for the challenge video, there are `NaN` values sometimes, which makes the proposed pipeline cannot work. I added a simple conditional statement `if not any(np.isnan(values)) is True:` to avoid this error.

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be the curve lane lines detection. The proposed pipeline works for straight lines only.

Another shortcoming is the `NaN` values for the conditions like challenge video,  if statement is expedient, hope I can learn more advanced method to cope with this problem.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be using higher order curve  to fit lane lines.
