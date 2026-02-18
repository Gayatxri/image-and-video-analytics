# STEP 1: Install OpenCV
!pip install opencv-python-headless

# STEP 2: Import libraries
import cv2
from google.colab.patches import cv2_imshow
from google.colab import files

# STEP 3: Upload image
uploaded = files.upload()

# STEP 4: Read image
image = cv2.imread("sunset.jpg")


if image is None:
    raise Exception("Image not loaded. Please upload img.jpg")

# Display original image
print("Original Image")
cv2_imshow(image)

# STEP 5: Zoom In (Scaling Up)
zoom_in = cv2.resize(image, None, fx=1.5, fy=1.5)
print("Zoom In Image")
cv2_imshow(zoom_in)

# STEP 6: Zoom Out (Scaling Down)
zoom_out = cv2.resize(image, None, fx=0.5, fy=0.5)
print("Zoom Out Image")
cv2_imshow(zoom_out)<img width="1600" height="900" alt="image (2)" src="https://github.com/user-attachments/assets/ad457866-8b57-4c33-bcf4-930e7fbb9a94" />
