# **Finding Lane Lines on the Road**


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/challenge.jpg "challenge"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I applied a Gaussian blur and followed by a Canny transformation. I created a 4-sided polygon to exclude those regions that doesn't contain lane lines. Then I drew line segments according to Hough transformation. Finally, I overlaid the lane line segments on the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first find out the average slope of left/right lanes, and then drew the extrapolated lane lines. Sometimes, shadow patches on the road or car trunk lines are noises that could potentially distort lane line slope. So I only processed these slopes that falls in the range of [0.4, 0.7]. After applied this filter, it gave me an acceptable result for "challenge.mp4".
![alt text][image1]

### 2. Identify potential shortcomings with your current pipeline

One shortcoming is I used 4 global variables to calculate the average slope and center points.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to eliminate global variables.

Another possible improvement would be to try a better average calculation. I kept a slope list that takes in only 20 entries, and dumped the oldest ones in the next process.
