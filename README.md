# EX. No: 7 – Lane Detection Using OpenCV
## Developed by:
## Name: DAKSHA SUBBAIAN
## Register number:212223230036
## Aim
To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

## Learning Objectives
- Understand each stage of image processing.
- Learn how to build a complete computer vision pipeline.
- Practice writing code in guided sections.

## Software Used
- Anaconda – Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (`cv2`)
- NumPy
- Matplotlib

## Algorithm and Explanation

### Step 1: Import Libraries
Import the required libraries for image processing and visualization.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### Step 2: Read Image
Read the input road image using OpenCV.

```python
img = cv2.imread("lan_img1.jpg")
```

### Step 3: Convert to Grayscale
Convert the original image into grayscale to simplify image processing.

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

### Step 4: Display Images
Display the original image and grayscale image.

```python
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")

plt.show()
```

### Step 5: Thresholding
Apply binary thresholding to separate relevant pixels based on intensity.

```python
ret, threshold = cv2.threshold(
    gray,
    127,
    255,
    cv2.THRESH_BINARY
)
```

### Step 6: Region of Interest (ROI) Masking
Create a mask to focus on the road region where lane markings are expected. Apply the mask to the thresholded image.

### Step 7: Edge Detection (Canny)
Detect edges in the ROI-masked image using the Canny edge detection algorithm.

```python
edges = cv2.Canny(roi, 100, 200)
```

### Step 8: Gaussian Blur
Apply Gaussian Blur to smooth the detected edges and reduce noise.

```python
canny_blur = cv2.GaussianBlur(edges, (5, 5), 0)
```

### Step 9: Hough Transform
Use the Probabilistic Hough Transform to detect straight lines in the image.

```python
rho = 1
theta = np.pi / 180
threshold = 20
min_line_length = 20
max_line_gap = 300

lines = cv2.HoughLinesP(
    canny_blur,
    rho,
    theta,
    threshold,
    np.array([]),
    minLineLength=min_line_length,
    maxLineGap=max_line_gap
)
```

### Step 10: Lane Detection Logic
Separate the detected lines into left and right lane lines. Calculate average slopes and intercepts, extrapolate the lane lines, and draw them on the original image.

## OUTPUT:
<img width="330" height="507" alt="image" src="https://github.com/user-attachments/assets/b76f001e-f1da-456c-bab1-15fe00a7b4cc" />

<img width="327" height="511" alt="image" src="https://github.com/user-attachments/assets/42e2bd8f-13ce-4d73-a868-13da2ff5aea0" />

<img width="330" height="507" alt="image" src="https://github.com/user-attachments/assets/6133841b-12c4-495d-b64b-db2ce6982fcc" />

<img width="437" height="672" alt="image" src="https://github.com/user-attachments/assets/01a0474e-c258-4e21-a9af-63f35549af0d" />

<img width="446" height="697" alt="image" src="https://github.com/user-attachments/assets/f53f6cde-0041-4126-9b6f-afdc11ccafc0" />

## Result

The lane detection pipeline is successfully implemented using OpenCV. The input road image is processed through grayscale conversion, thresholding, ROI masking, edge detection, Gaussian smoothing, and Hough Line Transformation to identify and display the lane lines.
