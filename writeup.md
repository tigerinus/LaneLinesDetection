# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[image1]: ./test_images_output/1_grayscale.jpg
[image2]: ./test_images_output/2_blurred.jpg
[image3]: ./test_images_output/3_edges.jpg
[image4]: ./test_images_output/4_masked.jpg
[image5]: ./test_images_output/5_lines.jpg
[image6]: ./test_images_output/6_overlayed.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps when processing an image.

Step 1 - Convert the image to grayscale.

![image1]

Step 2 - Blur the grayscale image to get rid of any noise.

![image2]

Step 3 - Use Canny edge detection to find the all edges in the blurred image.

![image3]

Step 4 - Mask the detected edges that are not in the region of interest.

![image4]

Step 5 - Use Hough line detection to convert the edges into lines.

![image5]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function such that, 1) it categorizes each line into left lines and right lines based on the slope and the top start position of it, 2) averages each group of left and right lines into a single left line and a single right lane, 3) extend the left and right lines based on their slopes.

Step 6 - Overlay the detected left and right lanes on top of the original image.

![image6]

### 2. Identify potential shortcomings with your current pipeline

Obviously the pipeline works only when the lane is straight. It won't work when the lane is being curved.

By running the pipeline against the video from optional challenge section, it turns out occasionally there is a big offset of the detected lanes. Potential causes can be:

* Shadow of the surrounding objects can be disturbing.
* Curbs at left side got mistaken as the lane line.
* When the color of the lane lines are close to the road color (due to sunlight effect), edges can be hardly deteted.

### 3. Suggest possible improvements to your pipeline

Possible improvements can be,

* Instead of detecting edges on grayscaled image, it should detect edges in each color channel of the image, i.e. RGB. In theory, grayscaled image contains less information than full color image.
* Setup a threshold n such that only inner n edges are considered as lane lines, to avoid mistaking curbs as lane lines.
* Extend every detected line, then ignore any extended line getting cut at the left/right side of the image boundary, instead of getting cut at the bottom of the image.
* Slope of left and right lines should be symmetry. Based on this theory, any line whose slope is not symmetry to the other side should be ignored.