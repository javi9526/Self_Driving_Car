**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/gray_solidWhiteCurve.jpg "Grayscale"
[image2]: ./test_images_output/blur_gray_solidWhiteCurve.jpg "Blurred grayscale"
[image3]: ./test_images_output/edges_solidWhiteCurve.jpg "Edges"
[image4]: ./test_images_output/ROI_edges_solidWhiteCurve.jpg "ROI edges"
[image5]: ./test_images_output/lines_img_solidWhiteCurve.jpg "Lane lines"
[image6]: ./test_images_output/lane_lines_img_solidWhiteCurve.jpg "Image with lane
lines"
[image7]: ./examples/laneLines_thirdPass.jpg "Image with unified lane lines"
---

### Reflection

### 1. Pipeline description and draw_lines() modification.

My pipeline consisted of 6 steps for each image or video photogram::

1- Converting to grayscale.

![alt text][image1]

2- Applying gaussian blur in order to smooth and make the edges more clear.

![alt text][image2]

3- Using Canny transform to extract the edges.

![alt text][image3]

4- Selecting the ROI  where the Lane Lines are located.

![alt text][image4]

5- Searching the lane lines with the Hough algorithm for lines and obtaining the
lane lines image.

![alt text][image5]

6- Combining the initial image/photogram and the lane lines image to see if they are
correct.

![alt text][image6]



In order to draw a single line on the left and right lanes, I modified the draw_lines()
function. Now, the pipeline follows these steps:

1-  A for loop filters and classifies the lines obtained from Hugh's
transform attending to their slopes. Only some slopes ranges are valid when
considering lines as part of lane lines. These lines are defined by their ends points
coordinates.

2- A 1d-polynomial least squares fitting for each lane line using the classified coordinates.
This is carried out with de numpy.polyfit() function, which returns a vector with the coefficients
of the polynomial function (f(x)=mx + b, where the coefficients are m and b).

3- Extracting the desired points of these functions to obtain the single lane
image. It's done with de numpy.polyval() function.

This functionality is encapsuled in a try except block in order to avoid
errors when lines cannot be identified by Hough's algorithm.

The result is as follows.

![alt text][image7]


### 2. Potential shortcomings with the current pipeline.


One potential shortcoming would be what would happen when lane lines are erased and
hough can't even recognize one of them. In this case what we do is not to represent
the lines in that case, but in a real situation, there should be another way
to keep the path.

Another shortcoming could be the brightness and color changing throughout the day, or
even when going through a tunnel. As the parameters are fixed, the behaviour
wouldn't be reliable.


### 3. Possible improvements to the pipeline.

A possible improvement would be to approximate missing lane lines taking the
last valid line and changing the direction proportionally to how the opposite
line does.

Another potential improvement could be to make Canny and Hough parameters
variable depending on brightness sensors values or deep learning methods.

Another improvement could be to select the ROI before applying gaussian blur
and obtaining the edges image with Cannys algorithm. This could decrease the
computational cost.
