# **Finding Lane Lines on the Road**
---
## Pipeline Description
My pipeline consisted of 4 steps:
1. Convert color image to gray scale
2. Crop the region of interests which may include the lane lines
3. Draw two lane lines with solid straight lines by modifying draw_lines()
    * Find lines segments with hough_lines()
    * Separate lines segments into left and right according to their slopes
    * For left slope line segments:
        * Find the slope and center of each segment, and then average them to get the left lane line slope and center
        * Find the intersect end points inside the region of interests for the left lane line defined by above slope and center point
        * Draw the left lane line with the end points
    * Similar operation on right slope line segments, draw the right lane line
4. Combine the lane lines with the original color image
---
## Improvements of current pipeline for optional challenge
Challenges of the optional video include:
* Camera positions too low, that the video includes car hook at the bottom, which lead to mis-identify of many horizontal line segments of the car hook.
* Lane lines are quite curly in some section.

Improvements to the existing pipeline:
* Redefine the region of interests with bottom line moved up.
* Adjust the slope limit for classifying left and right slope, to exclude too flat or too vertical lines from car hook or surroundings. Lane lines slopes usually fall in between.
* Set the center of each line segment to be biased to the bottom side, then lines drawn for curly road can be more stable.
* Need to be cautious with above 3 improvements implementations. Parameters should be carefully tuned, otherwise the hough_lines() will not find any line segment on given frame.
---
## Shortcomings with my current pipeline
Potential shortcomings would be:
1. Not able to capture large curvature of the lane Lines
2. When the lane lines are worn out in some road section, or when the light is too strong or too weak, or covered by snow or rain, the lane lines will be less visible from the camera
3. The lane lines will stop at cross-sections.
---
## Possible improvements

Possible improvements would be:
* For shortcoming #1, use a more sophisticated algorithm to find curves in addition to straight lines, and connect the curve points together.
* For shortcoming #2, when the lane lines are less visible, we may need to use reinforcement technique to bring more contrast to the lane lines before converting it to greyscale. Or use better quality camera.
* For shortcoming #3, in addition to lane detection stops, include cross-section detection to make combined decision. Cross-section may be detected with other pairs of lane lines not along or opposite of current one, or with traffic lights / stop signs etc.
