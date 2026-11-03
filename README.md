# EXP NO: 04-Record-Image Transformations
## NAME : Dhanappriya S
## REG NO :212224230056

# Aim
To perform various foundational Image Transformations (Translation, Scaling, Shearing, Reflection, Rotation, and Cropping) on a given image using Python and OpenCV (cv2).
# ProcedureImport 
### Required Libraries:
Import OpenCV (cv2), NumPy (np), and Matplotlib (plt) to handle image processing and plotting.
### Step 1:
Load and Display the Original ImageRead the image from file using cv2.imread().Convert the color format from BGR to RGB using cv2.cvtColor() for correct rendering, and display it using plt.imshow().
### Step 2: 
Image TranslationDefine horizontal ($tx$) and vertical ($ty$) shift factors.Create a translation matrix and apply it using cv2.warpAffine() to shift the image position.
### Step 3:
Image ScalingDefine scaling factors ($fx$, $fy$) for width and height.Resize the image using cv2.resize() with bilinear interpolation (cv2.INTER_LINEAR).
### Step 4: 
Image ShearingDefine a shearing matrix to skew the image along the horizontal and/or vertical axes.Apply the transformation using cv2.warpAffine().
### Step 5:
Image Reflection (Flipping)Flip the image horizontally, vertically, or across both axes using cv2.flip().
### Step 6:
Image RotationDetermine the image center and define a rotation angle in degrees.Generate the rotation matrix using cv2.getRotationMatrix2D() and apply it using cv2.warpAffine().
### Step 7: 
Image CroppingDefine the bounding box coordinates (top-left corner $x, y$ along with width $w$ and height $h$).Crop the image by slicing the NumPy array: image[y:y+h, x:x+w].
# Code:
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
# Step 1: Load the image
image = cv2.imread('photo.jpg')  # Load the image from file
# Display the original image
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Convert BGR to RGB for correct display
plt.title("Original Image")  
plt.axis('off')
# Step 2: Image Translation
tx, ty = 100, 50  # Translation factors (shift by 100 pixels horizontally and 50 vertically)
M_translation = np.float32([[1, 0, tx], [0, 1, ty]])  # Translation matrix: 
# [1, 0, tx] - Horizontal shift by tx
# [0, 1, ty] - Vertical shift by ty
translated_image = cv2.warpAffine(image, M_translation, (image.shape[1], image.shape[0]))
plt.imshow(cv2.cvtColor(translated_image, cv2.COLOR_BGR2RGB))  # Display the translated image
plt.title("Translated Image")  
plt.axis('off')
# Step 3: Image Scaling
fx, fy = 5.0, 2.0  # Scaling factors (1.5x scaling for both width and height)
scaled_image = cv2.resize(image, None, fx=fx, fy=fy, interpolation=cv2.INTER_LINEAR)
# resize: Resize the image by scaling factors fx, fy
# INTER_LINEAR: Uses bilinear interpolation for resizing
plt.imshow(cv2.cvtColor(scaled_image, cv2.COLOR_BGR2RGB))  # Display the scaled image
plt.title("Scaled Image")  # Set title
plt.axis('off')
# Step 4: Image Shearing
shear_matrix = np.float32([[1, 0.5, 0], [0.5, 1, 0]])  # Shearing matrix
# The matrix shears the image by a factor of 0.5 in both x and y directions
# [1, 0.5, 0] - Shear along the x-axis (horizontal)
# [0.5, 1, 0] - Shear along the y-axis (vertical)
sheared_image = cv2.warpAffine(image, shear_matrix, (image.shape[1], image.shape[0]))
plt.imshow(cv2.cvtColor(sheared_image, cv2.COLOR_BGR2RGB))  # Display the sheared image
plt.title("Sheared Image")  # Set title
plt.axis('off')
# Step 5: Image Reflection
reflected_image = cv2.flip(image, 2)  # Flip the image horizontally (1 means horizontal flip)
# flip: 1 means horizontal flip, 0 would be vertical flip, -1 would flip both axes
plt.imshow(cv2.cvtColor(reflected_image, cv2.COLOR_BGR2RGB))  # Display the reflected image
plt.title("Reflected Image")  # Set title
plt.axis('off')
# Step 6: Image Rotation
(height, width) = image.shape[:2]  # Get the image height and width
angle = 45  # Rotation angle in degrees (rotate by 45 degrees)
center = (width // 2, height // 2)  # Set the center of rotation to the image center
M_rotation = cv2.getRotationMatrix2D(center, angle, 1)  # Get the rotation matrix
# getRotationMatrix2D: Takes the center of rotation, angle, and scale factor (1 means no scaling)
rotated_image = cv2.warpAffine(image, M_rotation, (width, height))  # Apply rotation
plt.imshow(cv2.cvtColor(rotated_image, cv2.COLOR_BGR2RGB))  # Display the rotated image
plt.title("Rotated Image")  # Set title
plt.axis('off')
# Step 7: Image Cropping
x, y, w, h = 100, 100, 200, 150  # Define the top-left corner (x, y) and the width (w) and height (h) of the crop
# Cropping the image from coordinates (x, y) to (x+w, y+h)
cropped_image = image[y:y+h, x:x+w]
# The crop is performed by slicing the image array in the y and x directions
plt.imshow(cv2.cvtColor(cropped_image, cv2.COLOR_BGR2RGB))  # Display the cropped image
plt.title("Cropped Image")  # Set title
plt.axis('off')
```
# Output:
<img width="1487" height="581" alt="image" src="https://github.com/user-attachments/assets/4cb72a70-1591-40a6-8824-e4c98a653e5f" />
<img width="1480" height="568" alt="image" src="https://github.com/user-attachments/assets/8f552d11-fc3f-426e-b98d-7e9dd15c6857" />
<img width="1476" height="437" alt="image" src="https://github.com/user-attachments/assets/afb99212-5672-45d4-907e-80760c3ad695" />
<img width="1480" height="552" alt="image" src="https://github.com/user-attachments/assets/0be100fc-8f91-40ed-bbe2-83c61a7ac7b8" />
<img width="1497" height="550" alt="image" src="https://github.com/user-attachments/assets/e7401b42-8d67-4cc1-9c04-055c88137469" />
<img width="1492" height="591" alt="image" src="https://github.com/user-attachments/assets/ade0ace5-5578-4dae-81e1-4b8ca78d7b4f" />
<img width="1472" height="565" alt="image" src="https://github.com/user-attachments/assets/07cc147d-20e4-49bb-8944-c324d3bde500" />

# Result:
Thus to perform various foundational Image Transformations (Translation, Scaling, Shearing, Reflection, Rotation, and Cropping) on a given image using Python and OpenCV (cv2) was verified successfully.

