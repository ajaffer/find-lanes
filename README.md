# **Finding Lane Lines on the Road** 
[//]: # (Image References)

[image1]: ./test_image_hough_lines/solidWhiteCurve.jpg "HoughLines"
[image2]: ./test_image_out/solidWhiteCurve.jpg "ExtraPolatedLines"


### Pipeline
The pipeline consists the following steps:
 
1) Applies the Grayscale transform
2) Applies a Gaussian Noise kernel
3) Applies the Canny transform
4) Draws hough-lines

Hough-Lines can be see in the following image: ![alt text][image1]

#### I then modified the draw_lines() function to do these extra steps:

1) separates out lines into left/right based on slope
2) removes lines that are too flat or too vertical
3) finds the vanishing point
4) filter out noisy lines, using the vanishing point
5) calculates average slopes for right/left lane lines
6) filter out noisy lines, that are too far away from the average
7) draws lines based on average slopes and the vanishing point and keeps a running avg of the right/left slopes 

The extrapolated lines look like the following image: ![alt text][image2]  

### 2. Shortcomings with current pipeline
* This implementation of the pipeline keeps a running average of the lines encountered. This approach is going to make the detected line react slowly to any fast changing conditions, which can be less than ideal at best and life threatening in worse situations.
* The extrapolated lines are not aligning properly with the lane lines, this is due to noisy data. 
* The pipeline does not execute well in the challenge video, due to lot of noisy data in the region of interest. 

### 3. Possible improvements to current pipeline
* Filter out the noise lines, which is causing the extrapolated lane lines to have a different angle than the actual lane lines.
* Instead of keeping running average, use a superior numerical analysis techniques.
* Step away from using a fixed region of interest, but instead rely on the features of road that can help identify the lane lines, e.g., the color of lines.

#### Notes
The pipeline function has the following signature: `pipeline(image, simple=False)` 

* When the second parameter is True, it will draw the hough-lines.
* When the second parameter is False, it will draw the extrapolated lines

The following output folders have been included:

* `test_image_hough_lines` - contains images with hough-lines
* `test_image_out` - contains images with extrapolated lines
* `test_videos_hough_output` - contains videos with hough-lines
* `test_videos_output` - contains videos with extrapolated lines

The python source is included in the file: `Project1.ipynb`
