# Satellite-imgae-segmentation
2023_SW_AI_Competition 7th <br>
해설본 : https://187cm.tistory.com/68 <br>
---
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/654f59ab-547e-4367-9d09-9c75aae7c519)
---

# Pre-processing
- we divide the images of size 1024x1024 into smaller segments, either into 16 images of size 256x256 or into 36 images of size 192x192, allowing for overlapping areas.
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/036efa48-fe3b-44d7-8831-6b8c3776d191)

# Configuring the Train/Valid/Test dataset.
- In a manner akin to the medical research process, which lacks predefined validation/test data, we create our own test dataset to facilitate our experiments.
- Our task involves dealing with 114,240 training images and 60,640 test images.
- To adapt to this setting, we partition the training images into a 2:1 ratio to form separate training and test datasets.
- Moreover, we divide the training dataset using a 2:1 ratio to make a validation dataset.
- When we submit the csv results of test images, we employ an 8:2 ratio for the respectively training and validation datasets.
- Lastly, we implement the ensemble method to enhance the results.
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/de232327-495d-432f-b6cc-c6a24fa4360d)

# Model, Augmentation, Loss function.
- 
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/91f5d0e5-e8ef-4ed5-9137-1c79a81b47f1)
