# **Finding Lane Lines on the Road** 
In this project I have implmented a image processing pipeline to detect lanes on given mono-vision video captured from a vehicle.
This algorithm detects the following types of lines on the road.
1. Dotted Yellow
2. Solid  Yellow 
3. Dotted White 
4. Solid white

### The pipeline immplmented is divided into the following stages .
## 1. RGB to gray scale conversion
 During this stage the RGB image is converted into the Gray scaled image
### input:
<img src="https://github.com/raghu467/Finding_Lanes_P1/blob/master/test_images/whiteCarLaneSwitch.jpg" alt="input" width=432 height=288>

### Output:
![alt tag](https://github.com/raghu467/Finding_Lanes_P1/blob/master/Write_up_attachments/image_gray1.png)

## 2.Apply gaussian_blur
 During this stage Gaussian blur is applied to the output of stage 1 using a kernel of size 7
### Output:
![alt tag](https://github.com/raghu467/Finding_Lanes_P1/blob/master/Write_up_attachments/image_gray_blur2.png)


## 3.Canny Edge Detection
 During this stage Canny edge detection is applied on to the blurred gray image.
 Threshold used for canny edge detection are 50 and 150
### Output:
![alt tag](https://github.com/raghu467/Finding_Lanes_P1/blob/master/Write_up_attachments/image_canny3.png)

## 4.Applying ROI 
 In this stage the region of interest is applied and the unwanted top portion of the image is clipped.
### Output:
![alt tag](https://github.com/raghu467/Finding_Lanes_P1/blob/master/Write_up_attachments/image_ROI4.png)

## 5.Hough Transform
 In this stage we find the hough transform for all the points on the collection of lines.
 These lines are then filtered based on slope to eleminate lines with small slope.
 Now we segregate this filtered lines into left and right lines based on the slope(Negative or Positive)
 Now that we have left and right lines. we use these poits as input to the linear-regression and find the m and b(y=mx+b) for the lines representing left and right lines.once we have the line equations for the left and right lanes, we also know the range cut off limit for the Y co-ordinates(from bottom of the screen to ROI- coordinate) using this values we find the x co-odrinates(lx1,lx2,rx1,rx2) to define the left and right lanes.
 
 #ROI Y coordinates Limits
    y1 = img.shape[0]
    y2 = 320
    
    # (lx1,y1)----Left Line----(lx2,y2)
    # (rx1,y1)---Right Line----(rx2,y2)
    
    
 . The output of the hough transform are then 
 super imposed on to the lines.
### Output:
![alt tag](https://github.com/raghu467/Finding_Lanes_P1/blob/master/Write_up_attachments/image_houg_lines5.png)

## 6.Adding the weighted images
 During this stage we Add the input RGB image with the output of stage 5 to get the redlines super imposed on the Actual lanes in the 
 image.
### Output:
![alt tag](https://github.com/raghu467/Finding_Lanes_P1/blob/master/Write_up_attachments/image_Weighted6.png)

Shortcommings and scope for improvement:
This algorithm uses Gray sacle based edge detection Which makes it difficult to detect lanes on a beaten-up road surface.
This algorithm can be improved by using HSV based segmentation. The ROI based hough transfrom implmentation currently used in this algorithm can be further improved so that the lanes with curves can be better Identified. Even the drawing function currently used draws straight lines, this can be improved to be able to draw curved lines aswell.




