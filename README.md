# Project 1: Finding Lane Lines
Tyler Zamjahn

Pipeline Description

My pipeline consists of 8 steps. Initially, the image is converted to grayscale for computational efficiency. Then a Gaussian blur is performed with a kernel size of 5 to eliminate smaller color changes that would otherwise have large gradient values. Next, Canny edges are detected in the image. The picture ins then masked to filter out any edges not located in a trapezoidal region of interest (ROI). Lines in the image are then found using a Hough transform of the Canny edges detected in the ROI. In order to eliminate unwanted lines that may have been detected, the resulting lines in the image are then converted to greyscale and undergo a second Hough transform, hough_lines2(). The second Hough transform has more stringent criteria for length and allows for larger gaps between connecting lines to connect dashed lines in a uniform direction. During this second Hough transform, a different draw_lines() function is used, draw_lines2(). This function differs from the original in that it only draws two lines for either lane in the image. The function organizes the points so that all lines are being drawn in the same direction, from the bottom of the image to the top, and then averages the end point locations of each lane line. This average location is then used to extend each lane from the upper mean location to the bottom of the image through the lower mean location. These two resulting lines, one for the left lane and the other for the right, are then plotted on the image using the weighted_img() function. An example output is shown below in output0.

 ![Image 0]
(https://github.com/tzamjahn/Project_1-Finding_Lane_Lines/blob/master/test_images_output/output0.jpg)


Potential Shortcomings

Potential shortcomings of the pipeline are that it plots a single lane line for each side using the mean of the lines detected. This means that if the lane curves drastically a single line will not accurately represent the lines. Additionally, because it is a mean, the line will not always lie perfectly on the lanes as can be seen in output4 below. The current pipeline also has some horizontal variations from frame to frame that occasionally jumps because of perpendicular lines in the image. While the pipeline eliminates most unwanted edges using multiple Hough transforms, road lines that are perpendicular to the lane and are long enough to make it through the transforms will cause a large shift in the mean of the lane line.

 
./test_images_output/output0.jpg “output0”

Possible Improvements 

A possible improvement would be to use color to further eliminate unwanted edge detections in the ROI so that only lanes would be detected in the frames, making the outputs more accurate.

Another potential improvement could be to incorporate a standard deviation calculation to the draw_lines2() function so that outliers could be eliminated from the mean lines. This would eliminate the noise from frame to frame caused by unwanted edges.

