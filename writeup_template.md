# **Finding Lane Lines on the Road** 

## Writeup Report


**Project Overview**

The goal of this project is using computer vision techniques implemented by OpenCV to make pipeline which gets an image as the input and finds the lane lines on the road. At the end of project, this pipeline is utilize to draw the lane lines on the video recording of real-world driving situation.


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Lane Line Detection Pipeline Overview 

My pipeline consisted of six steps illustrated in the following image. 

#### 1. Color Selection

In this stage, since the lane lines are white and yellow in this project, the yellow and white colored pixels are filtered; this is done by defining two masks: one for white range of RGB and another for yellow range of the RGB. The final filter is obtained by performing the bitwise OR operation on these masks. Finally, the input image is masked by this filter by performing the bitwise AND operation between the mask and the initial image.
The purpose of this stage is to divert the focus of the pipeline on the interesting areas of the image whick is the lane lines. Altough in this project the lane lines are all yellow and white, in the real-world they can be of any color. Therefore, I suppose this stage just suits this project images and videos not the real-life situations.

#### 2. Gray-Scale Coversion

The image is converted to gray scale in this stage, so it can be used as the input to the canny-edge detection stage.

#### 3. Gaussian Blurring

This is done to remove the noises on image which give us strong gradients at the canny edge detection stage. The guassian kernel size is the only parameter here, and the tuning method of this parameter is described in the next stage.

#### 4. Canny Edge Detection

The Canny edge detection method basically performs the gradient over the gray-scale image to bring out where the pixels are shifting color. these edges can be used to distiguish between different objects in the image. there are three parameters here: the low threshold, high threshold, and the gaussian kernel size from the previous stage. if the pixel after the gradient has the value below the low threshold it is not an edge, if the value is greater than the high threshold, it is an edge, and if it is between the low and high threshold, it can be an edge if it neighbors an edge. the [GUI helper tool](https://github.com/maunesh/opencv-gui-helper-tool) is used to tune these parameter. I started with the kernel size 3, low threshold 10 , high threshold 50. first, I increased kernel size until all small edges were gone and lane lines were intact. then, i increased the low threshold until the lane lines started to disapear, then i increased the high threshold until i got lane lines clear on the output.

#### 5. Masking the Region of Interest

To focus to where lane lines are more likely are located, this stage masks the image with a quadrilateral. the quadrilateral's height and top and bottom edges length and position are the parameters here, and they should be expressed with respect to the image size. these are chosen to get the most of the lane lines visible in the images. 

#### 6. Hough Transform

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are stains with the same color and orientation of the lane lines on the road. in this case, those stains are also taken into account in the linear least-square regression, making the lane line incorrectly drawn on the screen.

Another shortcoming could be the region of interest, color filters, canny and hough parameters are hard coded in the pipeline. this is the problem when this pipeline is applied on the different set of images and videos.

Moreover, the drawn lines on the videos are a bit flickery and unsteady.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add memory to the function which processes the video frames. this would help in the situations like the challenge video where the image of the road is too noisy to detect any lane lines. with this technique, i suppose we can focuse on the region where the lane lines had been detected before and ignore the noise and other changes on the road.

Another potential improvement could be to ...
