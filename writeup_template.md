# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps. 

   1. convert the image to grayscale
   2. use Gaussian to get read off noise
   3. use Canny to detect edges on the image
   4. set up the region in which we are interested in
   5. define the Hough transform parameters and get hough lines
   6. and finaly to get weighted the image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by getting the coordinates of longest left and right lines that were detected by hough_lines method, then I calculated right and left slopes using the formula (y2-y1)/(x2-x1). During the next step I calculated extrapolated lines' coordinates using these slopes, "longest lines" coordinates and line limits for Y coordanates ( max Y equals image height and min Y was found by experiments and almost equals a half of image height). Finally, I added these 2 lines on the  image.

I would like to add that I tried several methods of getting extrapolated lines. One of them was
   1. getting top and bottom lines for left and rirht that were detected by hough_lines method
   2. use its coordinates to get a long "line fragment" from top to bottom 
   3. and then calculeting slopes and extrapolated lines base on these aproximated long lines
I'm still testing this method trying to the reasoning why it doesn't work so well as I expected.


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when a camera mounted on the car change its possition. In this case lines can appear in different region and my "region of interest" will not fit these conditions. Also shortcoming related to the "region of interest" could be a situation when a car is changing the lane which will cause of changing the regions in which road lanes appears in the moment when the car is between 2 road lines.

Another shortcoming could be weather, light and road conditions that can cause problems of detecting lines by hough_lines method.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to set 2 or more region of interests for detecting left and right lines. I'm doing this for challenge problem, but still don't have stabe results for it.

Another potential improvement could be to try to get road, weather and light conditions 'on the fly' and change paramenters for Canny and hough_lines methods, but it will require additional time to make a calculation.
