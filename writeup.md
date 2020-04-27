# **Finding Lane Lines on the Road** 

## Project Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline implemented is as follows:

1. Covert to greyscale 
2. Canny Edge detection
3. Mask off the regions of the image that we are interested in. This is a polygon reflecting the road directly in front of the car
4. Hough transform - to move use into line space 


### 2. Identify potential shortcomings with your current pipeline

The pipeline has a few points that could be improved to make it more efficient. At present the structure reflects one where each step has been implemented in such a way as to ensure it is performing its actions appropriately. Having completely this, a small amount of refactoring could give more performance and memory efficiency.

In addition to this, there are some hard coded values in the pipeline that reflect the specific example and should be parameterised in order to produce a more robust implementation.

In terms of accuracy, the pipeline stages were initially configured for the sample images. These gave a very good accuracy and the resulting video demonstrates pretty good tracking. Moving onto the second video example however, the accuracy seems to be somewhat less. It is likely that further refinement of the parameters to the various pipeline stages may help.

### 3. Suggest possible improvements to your pipeline

Potential improvements that could be made, apart from the refactoring for performance would include spending more time with the additional examples to further tune the accuracy. This would give some small benefits in these limited cases but may not be quite so robust in the general case. 

During development there were also a few frames where no lines were detected in the second case. While this is not desirable it may happen and, given that with a video we are dealing with a stream of frames, using information from previous frames may be advantagous in reducing the likelihood of this having a catastrophic error. In the submission provided any frames where no lane lines are detected just draws no fit line to demonstrate the lost of tracking, rather than holding the previous fit. 


It is also likely that futher improvements could be made with better colour space processing. At present the colour image is converted to grayscale which works acceptably on the first example and reasonably on the second example. By the final example, the yellow line seems to be nearly completely missed. 


