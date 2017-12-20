# **Finding Lane Lines on the Road** 

The goal of this project:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./test_images_output/one_channel_3.jpg "Yellow lane one channel image"
[image2]: ./test_images_output/blur_gray_3.jpg "Yellow lane gaussian smoothing"
[image3]: ./test_images_output/canny_3.jpg "Yellow lane after canny transform"
[image4]: ./test_images_output/masked_edges_3.jpg "Yellow lane after selecting a region"
[image5]: ./test_images_output/hough_lines_3.jpg "Yellow lane after hough tranform"
[image6]: ./test_images_output/final_image_3.jpg "Yellow lane final image"
[image7]: ./test_images_output/one_channel_0.jpg "White lane one channel image"
[image8]: ./test_images_output/blur_gray_0.jpg "White lane gaussian smoothing"
[image9]: ./test_images_output/canny_0.jpg "White lane after canny transform"
[image10]: ./test_images_output/masked_edges_0.jpg "White lane after selecting a region"
[image11]: ./test_images_output/hough_lines_0.jpg "White lane after hough tranform"
[image12]: ./test_images_output/final_image_0.jpg "White lane final image"
[image13]: ./examples/line-segments-example.jpg "Line segments example"
[image14]: ./examples/regression_formulas.jpg "Regression formulas"

---

### Reflection

### 1. Lane detection pipeline.

The proposed pipeline consisted of 5 steps.

a. First, select just one color channel of the image by converting the RGB space to gray:

![alt text][image1]
![alt text][image7]

b. Second, apply Gaussian smoothing to reduce image noise and spurious gradients before applying the Canny transform

![alt text][image2]
![alt text][image8]

c. Next, apply Canny transform to detect the edges in the image (i.e the lanes) by finding gradients in the image where pixels intensity changes rapidly

![alt text][image3]
![alt text][image9]

d. Select a region of interest, in this case a four side polygon in which the lane lines are contained:

![alt text][image4]
![alt text][image10]

e. Apply Hough transform to get our lane lines.

Hough transform is able to identify lines in the input image, but in this case just line segments as shown:

![alt text][image13]

But the final goal is to have a complete line per road lane, meaning that the hough lines should be extrapolated to get one single lane line. In order to draw a single line on the left and right lanes, the function draw_lines() should be modified, to use a regression method that in this case I applied the least squares regression method; which has the following formulas to find the line of best fit (y=mx+b):

![alt text][image14]

So we need to find the slope and intersect of the line of best fit. The first thing that is needed before applying the least squares methods, is to identify which lines correspond to the left lane and which ones to the right. Since Hough transform provide us lines with the starting and ending points [x1, y1, x2, y2], we can calculate the slope of the line (y2-y1)/(x2-x1) and clasify them by negative slopes and positive slopes.

Once all x,y points of the lines are classified, we can just apply the formulas shown in the previous image. One of the disadvantages of this methods is that it is sensible to outliers, meaning that if a point is found but it is not a real point of the lane, then the final extrapolated line will be incorrect. For that reason, I decided to discard invalid point which there slopes vary considerably from the lane slope range.

After applying Hough tranform and extrapolating the lines, we get a black image with a couple of red lines on top which correspond to the lanes:

![alt text][image5]
![alt text][image11]

Finally, the lane lines are drawn on top of the original image:

![alt text][image6]
![alt text][image12]

### 2. Shortcomings


One potential shortcoming is when there are shadows and curves on the roads, which produces that the lanes are not found or are not detected fine in the final image. The best example is the challenge video, I applied my pipeline to that video and I see wrong lane detection around the middle of it, after analyzing why, I noticed that there are some shadows on the road so it is difficult for the algorithm to find the lanes. I tried to adjust the function parameters but I was not able to get a stable solution, in my case around the middle of the video, there are some moments where the lanes are not drawn because no valid lane segments were found


### 3. Possible improvements

A possible improvement would be to look for a better method to use in curves and also when there are shadows.

Another possible improvement is to look for a library that already provides the regression computation.
