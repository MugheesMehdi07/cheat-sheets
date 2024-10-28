

## 1. Image Handling

**Approach**:  
Computer Vision starts with handling and manipulating images. Libraries like **OpenCV** and **Pillow** allow reading, displaying, and manipulating image data.

- **OpenCV**: Optimized for speed and efficiency in image processing.
- **Pillow (PIL)**: A more Pythonic library for basic image operations.
- **Matplotlib**: Used for displaying images within notebooks.

#### Code:
```python
import cv2
from PIL import Image
from matplotlib import pyplot as plt

# Read and display an image using OpenCV
img = cv2.imread('image.jpg')
cv2.imshow('Image', img)
cv2.waitKey(0)
cv2.destroyAllWindows()

# Display image with Matplotlib (requires RGB conversion)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
plt.show()
```

---

## 2. Image Preprocessing

**Approach**:  
Preprocessing helps prepare images by reducing noise or enhancing edges. **Blurring** and **thresholding** techniques are crucial for extracting relevant features.

- **Gaussian Blurring**: Uses a Gaussian filter to smooth images and reduce noise.
- **Canny Edge Detection**: Detects edges by looking for gradients in pixel intensity.
- **Thresholding**: Converts images into binary format based on pixel intensity.

#### Code:
```python
# Apply Gaussian blur
blurred_img = cv2.GaussianBlur(img, (5, 5), 0)

# Canny Edge Detection
edges = cv2.Canny(img, 100, 200)
plt.imshow(edges, cmap='gray')
plt.show()

# Thresholding
gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
_, thresh_img = cv2.threshold(gray_img, 127, 255, cv2.THRESH_BINARY)
plt.imshow(thresh_img, cmap='gray')
plt.show()
```

---

## 3. Geometric Transformations

**Approach**:  
These transformations help manipulate images spatially. **Rotation** and **translation** are two common operations. These operations are often used for data augmentation and aligning images.

#### Code:
```python
# Rotate image by 45 degrees
rows, cols = img.shape[:2]
rotation_matrix = cv2.getRotationMatrix2D((cols/2, rows/2), 45, 1)
rotated_img = cv2.warpAffine(img, rotation_matrix, (cols, rows))

# Translate image (shift right by 50px and down by 100px)
translation_matrix = np.float32([[1, 0, 50], [0, 1, 100]])
translated_img = cv2.warpAffine(img, translation_matrix, (cols, rows))

# Display the rotated image
plt.imshow(cv2.cvtColor(rotated_img, cv2.COLOR_BGR2RGB))
plt.show()
```

---

## 4. Object Detection and Recognition

**Approach**:  
Object detection models localize and identify objects within an image. **Haar Cascade classifiers** use pre-trained models for detecting faces, while **YOLO** is a deep-learning-based real-time object detection model.

### Haar Cascade Classifier  
Uses a cascade of simple features for fast object detection. It works well for faces and other well-defined objects.

#### Code:
```python
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')
gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
faces = face_cascade.detectMultiScale(gray_img, 1.3, 5)

for (x, y, w, h) in faces:
    cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.show()
```

### YOLO (You Only Look Once)  
A state-of-the-art real-time object detection system that divides the image into a grid and detects multiple objects in one pass.

#### Code:
```python
import torch

# Load YOLOv5 model
model = torch.hub.load('ultralytics/yolov5', 'yolov5s', pretrained=True)
results = model('image.jpg')  # Perform detection
results.show()  # Display results
```

---

## 5. Image Segmentation

**Approach**:  
Image segmentation separates different parts of an image. **Contours** detect shapes, while **GrabCut** separates foreground from background.

#### Code:
```python
# Contour Detection
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
contours, _ = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
cv2.drawContours(img, contours, -1, (0, 255, 0), 2)

# Display image with contours
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.show()

# GrabCut for Foreground Extraction
mask = np.zeros(img.shape[:2], np.uint8)
bgd_model = np.zeros((1, 65), np.float64)
fgd_model = np.zeros((1, 65), np.float64)
rect = (50, 50, 450, 290)
cv2.grabCut(img, mask, rect, bgd_model, fgd_model, 5, cv2.GC_INIT_WITH_RECT)
mask_2 = np.where((mask == 2) | (mask == 0), 0, 1).astype('uint8')
img = img * mask_2[:, :, np.newaxis]

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.show()
```

---

## 6. Working with Pre-trained Models

**Approach**:  
Pre-trained models like **VGG16** allow using pre-built architectures trained on large datasets. These are useful for image classification without training a model from scratch.

#### Code:
```python
from tensorflow.keras.applications.vgg16 import VGG16, preprocess_input, decode_predictions
from PIL import Image
import numpy as np

# Load VGG16 model pre-trained on ImageNet
model = VGG16(weights='imagenet')

# Preprocess and predict
img = Image.open('image.jpg').resize((224, 224))
img_array = np.array(img)
img_array = preprocess_input(np.expand_dims(img_array, axis=0))
predictions = model.predict(img_array)
print(decode_predictions(predictions, top=3)[0])
```

---

## 7. Augmentation for Deep Learning

**Approach**:  
Data augmentation increases the diversity of the training dataset by applying random transformations, such as flips or rotations, to the original data. This prevents overfitting.

#### Code:
```python
from torchvision import transforms
from PIL import Image

# Define transformations
transform = transforms.Compose([
    transforms.RandomHorizontalFlip(),
    transforms.RandomRotation(30),
    transforms.ToTensor()
])

# Apply transformation
img = Image.open('image.jpg')
augmented_img = transform(img)
```

---

## 8. Model Evaluation

**Approach**:  
Evaluation metrics such as **confusion matrices** help understand the performance of classification models by visualizing predictions and ground truth.

#### Code:
```python
from sklearn.metrics import confusion_matrix

# Example predictions and ground truth
y_true = [0, 1, 1, 0]
y_pred = [0, 1, 0, 0]

# Create confusion matrix
cm = confusion_matrix(y_true, y_pred)
print(cm)
```

---

## 9. Computer Vision Libraries Overview

- **OpenCV**: Efficient library for image processing and object detection.
- **Pillow (PIL)**: Simplifies basic image manipulation like resizing.
- **scikit-image**: Advanced image analysis with algorithms for segmentation and filtering.
- **PyTorch**: Deep learning library used for building and deploying CV models (e.g., YOLO).

---

