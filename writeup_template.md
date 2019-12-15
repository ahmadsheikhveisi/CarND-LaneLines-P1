# **Finding Lane Lines on the Road** 

## Writeup Report


**Project Overview**

The goal of this project is using computer vision techniques implemented by OpenCV to make pipeline which gets an image as the input and finds the lane lines on the road. At the end of project, this pipeline is utilize to draw the lane lines on the video recording of real-world driving situation.


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of six steps illustrated in the following image. 

#### 1. Color Selection

In this stage, since the lane lines are white and yellow in this project, the yellow and white colored pixels are filtered; this is done by defining two masks: one for white range of RGB and another for yellow range of the RGB. The final filter is obtained by performing the bitwise OR operation on these masks. Finally, the input image is masked by this filter by performing the bitwise AND operation between the mask and the initial image.
The purpose of this stage is to divert the focus of the pipeline on the interesting areas of the image whick is the lane lines. Altough in this project the lane lines are all yellow and white, in the real-world they can be of any color. Therefore, I suppose this stage just suits this project images and videos not the real-life situations.

#### 2. Gray Scale Coversion

The image is converted to gray scale in this stage, so it can be used as the input to the canny-edge detection stage.

#### 3. Gaussian Blur

This is done to remove the noises on image which give us strong gradients at the canny edge detection stage. The guassian kernel size is the only parameter here, and the tuning method of this parameter is described in the next stage.

#### 4. Canny Edge Detection

The 

#### 5. Masking the Region of Interest

#### 6. Hough Transform

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
