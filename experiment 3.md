import cv2
import numpy as np
import matplotlib.pyplot as plt
from operator import add
from functools import reduce

# Read image (correct filename)
img = cv2.imread("image.png")
if img is None:
    raise FileNotFoundError("image.png not found. Check upload/path.")

# Convert BGR (OpenCV default) to RGB for matplotlib
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

def split4(image):
    half_split = np.array_split(image, 2, axis=0)
    res = map(lambda x: np.array_split(x, 2, axis=1), half_split)
    return reduce(add, res)

# Split image into 4 parts
split_img = split4(img)

# Check shapes
print(split_img[0].shape, split_img[1].shape)

# Display split images
fig, axs = plt.subplots(2, 2)
axs[0, 0].imshow(split_img[0])
axs[0, 1].imshow(split_img[1])
axs[1, 0].imshow(split_img[2])
axs[1, 1].imshow(split_img[3])

for ax in axs.flat:
    ax.axis("off")

def concatenate4(north_west, north_east, south_west, south_east):
    top = np.concatenate((north_west, north_east), axis=1)
    bottom = np.concatenate((south_west, south_east), axis=1)
    return np.concatenate((top, bottom), axis=0)

# Reconstruct full image
full_img = concatenate4(
    split_img[0],
    split_img[1],
    split_img[2],
    split_img[3]
)

plt.figure()
plt.imshow(full_img)
plt.axis("off")
plt.show()<img width="515" height="372" alt="image (1)" src="https://github.com/user-attachments/assets/a7690a3f-6915-45e5-87a1-2e632a05e414" />
<img width="515" height="350" alt="image" src="https://github.com/user-attachments/assets/e80c6f21-657b-4c08-9369-a8acdd265bfc" />
