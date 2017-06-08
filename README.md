# Finding Lane Lines on the Road
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project we will detect lane lines in images using Python and OpenCV. 

## List of files as part of project submission
1. P1.ipynb : This file contains the code for lane finding
2. writeup_template.md : write-up for the P1.ipynb explaining the pipeline followed for the soln. and shortcomings of the soln. and the necessary improvements

# List of folders
1. **test_images** : it contains the test images on which lane finding algorithm is to be verified
2. **test_images_output** : it contains the output of lane finding algorithm on the test images . Output is without extrapolation i.e. the edges obtained after Canny edge detection and Hough transform
3. **test_videos** : it contains the video on which pipeline is to  tested to check the validity of the soln.
4. **test_videos_output** : contains two subfolder
    i. **without extrapolation** : it contains the output of pipeline on the **test_videos** without extrapolation
    ii. **with weighted sum and extrapolation** : it contains the output of pipeline on the **test_videos** with extrapolation

## Instruction for using the P1.ipynb
1. Install all the necessary packages and library mentioned in the [CarND-Term1-Starter-Kit-Test](https://github.com/udacity/CarND-Term1-Starter-Kit)
2. Run each cell in the sequence (shift+enter) .
3. **draw_lane_image** method is defined which take the help of helper function provided as the part of the assignment to draw the raw lines(lines after the canny edge detection and hough transform) on the input image. Output can be found in the  **"test_images_output"** directory of the project folder
4. To draw only the raw lines  (Without extrapolation) on video sequence ,call only **draw_lane_image** in **process_image** method. Output can be found in the  **"test_videos_output/without extrapolation"** directory of the project 
5. To draw the extrapolated lane lines , call the **draw_lane_image** followed by **draw_lines_updated** in the **process_image** , this will return an image with extrapolated lines for the lanes .Output can be found in the **"test_videos_output/without extrapolation"** directory of the project
6. When using the code , make sure the right value for the vertices (variable name **vertices** in the code) of polygon (to choose the region of interest) should be chosen
7. for 540x960 video, value of the apex coordinates ((455, 320), (505, 320)are different from that of 720x1280 video((600, 450), (700, 450)). keep the correct value while running for the particular frame size  video.
    
# Disclaimer 
This project is submitted as an assignment for **Self-Driving Car Nanodegree Program offered by Udacity**. 

