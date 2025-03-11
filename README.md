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

##PROGRAM:

##NAME:SANDHIYA R
##REG NO:212223240146
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('photo 1.JPG')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
##OUTPUT
![image](https://github.com/user-attachments/assets/cf2e9a76-952e-42e6-8a08-80a4a2571ec5)
```
faceImage.shape
```
##OUTPUT
![image](https://github.com/user-attachments/assets/84766bc6-9ce9-485e-9d32-3215cbae9893)
```
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::]);plt.title("glassPNG")
```
##OUTPUT
![image](https://github.com/user-attachments/assets/032ad8d5-42db-4bce-9ece-141ad5563b0b)
```
glassPNG = cv2.resize(glassPNG,(300,100))
print("image Dimension ={}".format(glassPNG.shape))
```
##OUTPUT
![image](https://github.com/user-attachments/assets/927cea74-4730-49d3-8c4f-14cbdfdd2b4d)

```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
##OUTPUT
![Screenshot 2025-03-11 191354](https://github.com/user-attachments/assets/8df1f71b-8691-43ce-ad5b-456efd395996)

```
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[200:300,300:600]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
##OUTPUT
![image](https://github.com/user-attachments/assets/116b24e1-a7ab-4b7a-a917-f3854ffab20e)

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask / 255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI = faceWithGlassesArithmetic[200:300, 300:600]
maskedEye = cv2.multiply(eyeROI, (1 - glassMask))
maskedGlass = cv2.multiply(glassBGR, glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[10,10])
plt.subplot(131); plt.imshow(maskedEye[...,::-1]); plt.title("Masked Eye Region")
plt.subplot(132); plt.imshow(maskedGlass[...,::-1]); plt.title("Masked Sunglass Region")
plt.subplot(133); plt.imshow(eyeRoiFinal[...,::-1]); plt.title("Augmented Eye and Sunglass")

```
##OUTPUT
![image](https://github.com/user-attachments/assets/206de77b-4499-45d0-aaf3-8671cbc8e359)

```
faceWithGlassesArithmetic[200:300, 300:600] = eyeRoiFinal
plt.figure(figsize=[20,20])
plt.subplot(121); plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image")
plt.subplot(122); plt.imshow(faceWithGlassesArithmetic[:,:,::-1]); plt.title("With Sunglasses")

```
##OUTPUT
![image](https://github.com/user-attachments/assets/04e30178-4c15-4306-bfb5-2554b4645897)

Feel free to fork, contribute, or customize this project for your creative needs!
