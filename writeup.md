# **Finding Lane Lines on the Road** 

## Project Writeup

---

**Finding Lane Lines on the Road**


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline implemented is as follows:

1. Covert to greyscale 
2. Canny Edge detection
3. Mask off the regions of the image that we are interested in. This is a polygon reflecting the road directly in front of the car
4. Hough transform - to move use into line space 


### 2. Identify potential shortcomings with your current pipeline

The pipeline has a few points that could be improved to make it more efficient. At present the structure reflects one where each step has been implemented in such a way as to ensure it is performing its actions appropriately. Having completely this, a small amount of refactoring could give more performance and memory efficiency.

In addition to this, there are some hard coded values in the pipeline that reflect the specific example and should be parameterised in order to produce a more robust implementation. This became slightly apparent with the optional challenge where the source video file was a different resolution to the previous two meaning that the region of interested had to be normalized appropriately. The code for this is functional but not very elegant.

In terms of accuracy, the pipeline stages were initially configured for the sample images. These gave a very good accuracy and the resulting video demonstrates pretty good tracking. Moving onto the second video example however, the accuracy seems to be somewhat deminished. On closer investigation it seems that was, in part, due to the presence of a faint horizontal reflection near the bottom of the screen which was sometimes being detected. It is likely that further refinement of the parameters would better focus the line detection although at this point, a slightly more crude approach was adopted for speed in which any near-horizontal lines were omitted from the averaging in the draw_lines_extrap( ) function.

Finally the last short coming which is identifiable in the optional challenge is that the CANNY edge detection is not ideal with just a grayscale input. See section below for further refinements.


### 3. Suggest possible improvements to your pipeline

Potential improvements that could be made, apart from the refactoring for performance would include spending more time with the additional examples to further tune the accuracy. This would give some small benefits in these limited cases but may not be quite so robust in the general case. 

During development there were also a few frames where no lines were detected in the second case. While this is not desirable it may happen and, given that with a video we are dealing with a stream of frames, using information from previous frames may be advantagous in reducing the likelihood of this having a catastrophic error. In the submission provided any frames where no lane lines are detected just draws no fit line to demonstrate the lost of tracking, rather than holding the previous fit. 

As previously mentioned there was a slight improvement made to ignore horizontal lines which seemed to be a subtle artifact of the second video. 

It is also likely that futher improvements could be made with better colour space processing. At present the colour image is converted to grayscale which works acceptably on the first example and reasonably on the second example. By the final example, the accuracy has reached an unacceptable level. Here it is likely that a move from RGB colour space to a HLS (Hue, Lightness, Saturation) space would probably be beneficial. 


