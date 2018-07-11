## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./examples/undistort_output.png "Undistorted"
[image2]: ./examples/undistort_test_image.png "Road Transformed"
[image3]: ./examples/grad_color_threshold3.png "Binary Example"
[image4]: ./examples/persp_transform2.png "Warp Example"
[image5]: ./examples/color_fit_lines.jpg "Fit Visual"
[image6]: ./examples/plot_output.png "Output"
[video1]: ./output_video/project_output.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Writeup / README

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

Calibration is carried out in the second and third cells of the notebook "Project Notebook.ipynb". In the second cell, corners of the chess board are identified on each calibration image. The in the third cell distortion and matrix coefficients are calculated with OpenCV calibrateCamera function using the identified corner indices.

In the following cells I save the calculated coefficients in a pickle file for later use, and create an example undistortion using these parameters and OpenCV's undistort function.


![alt text][image1]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![alt text][image2]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I have experimented with various sobel and color threshold combinations which can be seen under Color & Gradient Threshold section of the notebook. In the end I decided that a combination of  L and S color channels, and absolute sobel gradient with x orientation is the combination that provided the best results.

Thresholds are applied within the "process_img" function in my pipeline, using "abs_sobel_thresh" and "hls_thresh" functions.

![alt text][image3]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

My pipeline uses "warp_p" function to warp binary image. Through experimentation I have identified the optimal source and destination coordinate and hard coded them within the function:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 580, 450      | 350, 0        | 
| 180, 720      | 350, 720      |
| 1120, 720     | 900, 720      |
| 700, 450      | 900, 0        |

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![alt text][image4]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Then I did some other stuff and fit my lane lines with a 2nd order polynomial kinda like this:

![alt text][image5]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

Radius and vehicle offset calculations are done within function "calc_radius". Function takes in a road image together with x coordinate indices for left and right lane lines, then first fits a second order polynomial function to these values and uses the coefficients to calculate the radius of the curvature for each line.

For offset calculation, the function uses the polynomial function to get the x intercept values for left and right lines. Then it averages these values to approximate the center of the lane. On the other hand the car position is simply calculated as the center of the image. Finally the vehicle offset is calculated by subtracting lane center value from the car position.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

Pipeline uses "draw_lanelines" function to plot the lane, radius and vehicle offset values on to the image.

![alt text][image6]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./output_video/project_output.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
