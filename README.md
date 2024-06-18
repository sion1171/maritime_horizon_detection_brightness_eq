# Horizon Detection and Brightness Equalization in Maritime Situations
### Introduction

The rapid advancements in autonomous vehicle technologies have significantly impacted the development of autonomous ships, with enhancing situational awareness being a key challenge. This awareness relies heavily on integrating various sensors. Previous research developed image stitching technology to combine images from multiple cameras into a single, wide-view composite image. However, issues with pixel brightness variations and weak blending algorithms were identified. This study aims to equalize brightness across stitched images, improving the quality and reliability of the composite image and enhancing situational awareness for autonomous ships. As shown in the flowchart below, the Blending and Stitching Algorithm involves many steps. In this repository, I will focus on horizontal detection and brightness equalizing.

![Flowchart for Horizon detection and Brightness Equalization](../maritime_horizon_detection_brightness_eq/flowchart/flowchart_final.png)
### Hypothesis
Before performing image stitching and image blending, we identify the horizon to distinguish between the sky and the ocean. Then, we adjust the brightness of the sky and ocean parts separately. By doing this, we believe we can reduce the color brightness differences during the image stitching process.
### Horizon Detection
Steps to Horizon detection is as you can see on the bottom. 
![Horizon Detection](../maritime_horizon_detection_brightness_eq/flowchart/Horizon_detection_flowchart.png)
1. **Apply Median and Gaussian Blur**: To reduce noise from waves, use `cv2.medianBlur` and `cv2.GaussianBlur`.
2. **Define ROI (Region of Interest)**: Using ROI helps reduce the amount of information to be processed.
3. **Perform Edge Detection**: Apply Canny edge detection with `cv2.Canny` to find edges within the ROI.
4. **Execute Hough Line Transform**: Use `cv2.HoughLinesP` to identify lines from the Canny edge detection results and determine the longest line.
5. **Draw the Line**: Based on the longest line found, draw a line using its slope and endpoints.
### Brightness Equalization
Steps to Brightness Equalization is as you can see on the bottom.
![Brightness Equalization](../maritime_horizon_detection_brightness_eq/flowchart/Brightness_eq.png)
1. **Convert RGB to HSV**: Change the color scale from RGB to HSV using `cv2.cvtColor(image, cv2.COLOR_BGR2HSV)`.
2. **Adjust Brightness**: Calculate the average brightness of the top and bottom sections of the image and adjust the brightness accordingly.
3. **Convert HSV to RGB**: Switch back to the RGB color scale from HSV using `cv2.cvtColor(image, cv2.COLOR_HSV2BGR)`.
### Results
It effectively detects the horizon, and with brightness equalization, it is challenging to ascertain its effectiveness on real data. However, it appears to work well with the sample data. It is expected that this data cleansing process will prove effective during the stitching process. Future experiments will reveal if the data cleansing process was effective.
![alt text](../maritime_horizon_detection_brightness_eq/result/original_1.png)
![alt text](../maritime_horizon_detection_brightness_eq/result/result_1.png)
![alt text](../maritime_horizon_detection_brightness_eq/result/original_5.png)
![alt text](../maritime_horizon_detection_brightness_eq/result/result_5.png)


### Reference
[1] Jeong, Chi Yoon, et al. “Fast horizon detection in maritime images using region-of-interest.” International Journal of Distributed Sensor Networks, vol. 14, no. 7, July 2018, https://doi.org/10.1177/1550147718790753. 
