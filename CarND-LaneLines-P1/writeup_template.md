# **Finding Lane Lines on the Road**

## Writeup Template

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Pipeline description. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:

1- Converting images to grayscale.

![alt text][image1]

2- Applying gaussian blur in order to smooth and make the edges more clear.

![alt text][image1]

3- Using Canny transform to extract the edges.

![alt text][image1]

4- Selecting the ROI in the image where the Lane Lines are located.

![alt text][image1]

5- Searching the lane lines with the Hough algorithm for lines and obtaining the
lane lines image.

![alt text][image1]

6- Combining the initial image and the lane lines image to see if they are
correct.

![alt text][image1]



In order to draw a single line on the left and right lanes, I modified the draw_lines()
function. Now, the pipeline follows these steps.

1-  A for loop filters and classifies the lines obtained from Hugh's
transform attending to their slopes. Only some slopes ranges are valid when
considering lines as lane lines. These lines are defined by their ends points
coordinates.

2- A 1d-polynomial least squares fitting for each lane line using the classified coordinates.
This is carried out with de numpy.polyfit() function, which returns a vector with the coefficients
of the polynomial function (f(x)=mx + b, where the coefficients are m and b).

3- Extracting the desired points of these functions to obtain the single lane
image.


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ...

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
