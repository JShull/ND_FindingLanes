# **Finding Lane Lines on the Road** 

## Writeup By John Shull
**Finding Lane Lines on the Road**

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
I followed similar steps used in the examples prior to the project.
I established a set of variables that were related to ratios of the image size (this way if the image resolution changed the pipeline would still function correctly)
These variables were then used in the following manner.
1. Gray Scale Image
2. Blur the Gray Scale Image
3. Edge Detection through the canny edge detecting process
4. Mask the edges using some of the variables outlined above.
5. Hough transformation
6. Generalize a left and right line through a fitted line equation by evaluating slope and position of line relative to screen
7. Combine the original image with the results
See some of the test image results below
![Image1](/test_images_output/modified-solidWhiteCurve.jpg?raw=true "White Curve")

![Image2](/test_images_output/modified-solidWhiteRight.jpg?raw=true "Yellow Curve")

![Image3](/test_images_output/modified-solidYellowCurve.jpg?raw=true "Yellow Curve")
### 2. Identify potential shortcomings with your current pipeline

This method works okay within the scope of the assignment but internal to my modified line drawing function I have loops that I could probably optimize more efficiently within one loop. I am also storing items in multiple arrays due to my lack of knowledge regarding python numpy. I also didn't tailor the pipeline to work with the last video file - the last video file has a lot more noise regarding the hood of the vehicle. If this noise were removed the current pipeline would be sufficient for this video, but still not fully correct as the road markings have larger curvature than previous image data.

### 3. Suggest possible improvements to your pipeline
A few improvements would be to separate sections of the image to understand if we are turning right or turning left. (If we had additional sensor data we wouldn't need to do this optically) This could be done by splitting the image into two sections through separate masks. The lower mask would be roughly the same pipeline as mentioned above, but the secondary mask would only look at the upper portion of road and it would apply a higher degree polynomial for a higher fit function seeking curves. Then the reconstruction of the line could visually be done using a Bezier curve function with the parameter for curvature being represented by the top mask fitted equation. In addressing the extra challenge video, as mentioned in section 2, if the hood of the vehicle was removed from processing my current pipeline wouldn't deliver such varying lines. Another fix would be to hold the previous frames line in memory and compare the next frames line to this to determine if there is a significant change. 
