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

My pipeline consisted of 5 steps. 

For demonstrating my pipeline of this project.I get a illustration example,this below image is a raw image.

![raw_image](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_raw.jpg) 

First, I converted the images to grayscale.That means the channel of the image transfers from three channels to one channel.
![gray_image](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_gray.jpg) 

then I used the gaussian_blur method to the gray scale image,and got a blured gray image.
![blured_gray](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_blur_gray.jpg) 
At the third step,I used the canny detection transform to the blured gray image and got some edges on the image.
![edges_image](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_edges.jpg) 
The forth step is using a region mask to the result.I choose a  trapezoid shape in the center of the image as my musk.after this step,I get my concerning region's edges.
![newedges_image](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_newedges.jpg) 
The fifth step is using hough transforming method to the concerning region edge image and after this step I got some lines which are denoted by two points,the end points of the lines.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function. 

I classified the lines' points into two groups by x coordinates of the points.when x is less than half of the image width(480),it was classified to the first group (left line),x is bigger than 480, it was classified to the second group (right line).After that,I used the numpy's polyfit function to fit the two straight lines(left and right lines) by linear function.
![](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_lines.jpg) 
the last step is using the weighted_img()  fuction to add the two line to the raw image to get the output.
![](/home/kju512/mygit/CarND-LaneLines-P1/test_images/myexample_new.jpg) 
### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that the right line changes to a wrong place when the real lane line is very unclear and short. 

Another shortcoming could be that the two lines(left and right) sometimes looks like not having the same length. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be that when the real lane line is very unclear and short,we can use the output of the last frame to balance the current frame error.Maybe just replace the output from the last frame's output.

Another potential improvement could be decreasing and accurating the region of interest ,maybe i can get a better output.
