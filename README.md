## Advanced Lane Finding

This project contains code and media related to the "Advanced Lane Finding" project for Udacity Self Driving Car NanoDegree.

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

Contents:

* /camera_cal - contains images used for camera calibration
* /test_images - images provided for pipeline testing for project
* /output_video - video of lane finding results for "project_video" and "harder_challenge_video"
* /examples - contains images used in writeup
* video_pipeline.py - complete pipeline for identifying lanes in video format
* Project Notebook.ipnyb - Jupyter notebook that contains steps taken towards completion of the project including the pipeline
* writeup.md - contains project pipeline summary and reflections on the project outcome
* var.pkl - pickle file containing camera calibration calculations
