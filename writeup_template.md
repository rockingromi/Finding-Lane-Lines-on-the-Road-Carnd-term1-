# **Finding Lane Lines on the Road** 
---

## 1: Soln. Pipeline for the problem

i. **draw_lane_image** method is defined which take the help of helper function provided as the part of the assignment to draw the raw lines(lines after the canny edge detection and hough transform)
ii. **draw_lane_image** takes raw image as input and coverts it to gray scale image and calls canny edge detection on Gaussian blurred version of this image to find the edge 	and the edges which fall under the region of interest defined by the vertices of the polygon are passed to hough_lines (which I have modified to return the line image along with the coordinates of the Hough lines)to determine the line coordinates and draw the lines on the blank image and return the coordinates of the line and image with lines on it
iii. **weighted_img** method is called to combine the line image with the actual image 
iv. Output of the above method on **"test_images"** can be found in **"test_images_output"**  directory of the projcet
v. **draw_lane_image** is called as a function call within **process_image** function to draw the raw line on the video (sequence of images :))
vi. Raw output on the **"test_videos"** can be found in **"test_videos_output\without extrapolation"** directory of the projcet
vii. **draw_lines_updated**  defined to find the extrapolation of the lines for the video and images 
viii. **process_image** function first calls the **draw_lane_image** method  to determine the coordinates of the hough lines within the region of interest defined by the bounding polygon and this line coordinates are used by **draw_lines_updated** to find the extrapolated lines.

### Improvement of draw_line function and extrapolation of the lines  

ix.  **draw_lines_updated**  is the main function which draw the extrapolated (continuous lines)as follows
&nbsp;&nbsp;&nbsp; a. takes the coordinates of the hough lies returned by the **draw_lane_image** method and calculates the slope and intercept of each line
&nbsp;&nbsp;&nbsp;b. For left lane if slope is below some threshold say **-0.6(<-30 degree)** then only we will consider the line to be a possible edge of the left lane (assuming that lane will not have angle greater than **-30 degree** for left lane
&nbsp;&nbsp;&nbsp;c. If the slope condition is satisfied the previous value  of slope for the lane stored in the variable is update as weighted sum of current slope (40% weight) and previous valid slope (60% weight).same thing is done for intercept. If no valid slope is found in the current frame previous value is maintained for that frame.  Weighted sum is taken so as to avoid high frequency noise(i.e. outliers which may appear now and then as on an average the slope and intercept will not change drastically between the frames and will be very close to previous value
&nbsp;&nbsp;&nbsp;d. Similar strategy is applied for the right lane only the slope is taken more than **+30 degree**.
&nbsp;&nbsp;&nbsp;e. once the average value of the slope and intercept for both left and right lane is found for the current fame then intersection coordinate of both the lines are found and line is drown from the bottom of the fame to the few pixels before the intersection point with the with slope and intercept obtained by the above procedure mentioned in point no c.
&nbsp;&nbsp;&nbsp;f. extrapolate method is called to find the coordinate of the end of line defined by the bottom of the frame (max vale of the y axis and the y coordinate of the point of intersection of two lanes plus the offset by some pixels(I have chosen 5 pixels)  
&nbsp;&nbsp;&nbsp;g. Then draw_line function is used to draw the line with the coordinates given by **extrapolate**  method.
&nbsp;&nbsp;&nbsp;h. Line image is added as weighted function of input image and the line image by calling the weighted_img method
&nbsp;&nbsp;&nbsp;i. Weighted image is returned. 
&nbsp;&nbsp;&nbsp;j. Output can be found in  **"test_videos_output\with weighted sum and extraplation"** directory of the project

## 2. Potential shortcomings with your current pipeline

i. Lanes are considered to be straight which is incorrect. Rather than fitting a line fitting a polygon will give better estimate of the lane position on the road
ii. While making the weighted sum of the slope and intercept it is assumed noisy edges will exist for very short time.
iii. Bounding polygon is manually determined looking at the image manually and identifying the correct coordinates to avoid other unnecessary edges which will not work for real time as this information will not be available beforehand.
iv. Minimum slope of the lane as seen by the camera is assumed to be greater than abs(30 degree) which may not be always true.
v. Color information of the lane is not taken into account.

## 3. Possible improvements to the given pipeline

i. Rather than using a line fitting, polynomial fitting will be more accurate.
ii. Dependency on choosing the region of interest to avoid unnecessary edges should be avoided to make it more generic
iii. Dependency on the slope to avoid unnecessary lines should be avoided.
iv. The method which we have used here is very highly dependent on choosing the right parameters of canny and Hough transforms. More generic method which is less dependent on parameters should be chosen to find the lanes.
v. While determining the lanes , color information of the lanes is not used to improve the edge detection

