# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program 
```
import cv2
import matplotlib.pyplot as plt
import numpy as np
faceImage = cv2.imread('passport.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
![WhatsApp Image 2025-03-12 at 20 23 12_035fe97d](https://github.com/user-attachments/assets/360f546e-48c3-4974-b6a8-c5ca8af0b6c2)
```
glassPNG = cv2.imread('glasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
![WhatsApp Image 2025-03-12 at 20 23 39_fb5b9c17](https://github.com/user-attachments/assets/0c16b4cc-0ba0-4db1-b9a4-d137795c239c)
```
glassPNG = cv2.resize(glassPNG, (465,285))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![WhatsApp Image 2025-03-12 at 20 24 04_703607c7](https://github.com/user-attachments/assets/f36eeb81-e141-40a3-b7fb-3cab862aa2b2)
```
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[290:575, 405:870] = glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
```
![WhatsApp Image 2025-03-12 at 20 24 24_f69cbe74](https://github.com/user-attachments/assets/523bd895-93e3-4814-ade6-7059396b5d0e)
```
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))
glassMask = np.uint8(glassMask / 255) 

faceWithGlassesArithmetic = faceImage.copy()

eyeROI = faceWithGlassesArithmetic[290:575, 405:870]  
maskedEye = cv2.multiply(eyeROI, (1 - glassMask))  
maskedGlass = cv2.multiply(glassBGR, glassMask) 

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131); plt.imshow(maskedEye[..., ::-1]); plt.title("Masked Eye Region")
plt.subplot(132); plt.imshow(maskedGlass[..., ::-1]); plt.title("Masked Sunglass Region")
plt.subplot(133); plt
```
![WhatsApp Image 2025-03-12 at 20 25 26_fc3abf9f](https://github.com/user-attachments/assets/369ee9f9-eb1a-4531-979e-9f5d5c7522bc)
```
faceWithGlassesArithmetic[290:575, 405:870]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
![WhatsApp Image 2025-03-12 at 20 25 52_5d989179](https://github.com/user-attachments/assets/3b690bbf-1dc6-4e70-8ad5-4d584887ace4)

Feel free to fork, contribute, or customize this project for your creative needs!
