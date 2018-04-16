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

So far all videos/images I have tested with have clear lane marks. If situation occurs that current pipeline doesn't distinguish one lane line for a few seconds, it won't work as expected. It'll be a nice improvement if it could extrapolate the line according to the other lane line.

The slope filter I employed is kind of a hack since it's a fixed range based on empirical observation. When an abrupt turn on the road happens, it simply can not capture the correct lane lines. An adaptive filter has to be considered.

The current pipeline utilizes four-sided polygon which I think it covers too much areas. This brings more noises or unnecessary pixels to process. One possible way to improve it might define a narrower ROI or better, define a specific ROI for left/right lane separately.
