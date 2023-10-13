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

# Model, Augmentation and Loss function.
- We utilize the segmentation PyTorch library (SMP) for our experiments.
- The se_resnext50_32x4d encoder model is adapted, based on the Unet++ decoder architecture.
- We combine two loss functions: Dice loss and another loss chosen for various experiments (refer to the images below).
- Simple/weak augmentation methods, such as Random Cropping (previously mentioned), Flip, and RandomRotate90, are applied.
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/91f5d0e5-e8ef-4ed5-9137-1c79a81b47f1)

# Proposed 4 Kinds of Solutions for Task Recognition
1. Issue with small departments being unrecognized by our model.
2. Observed instances of departments having numerous holes in the image.
3. Unclear boundaries.
4. Patchifying the image, like converting 1024x1024 to 224x224 through 16 images, diminishes background properties.
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/d4442998-eeb9-4175-a123-d5b42b186dda)

# How we can solved it? (Resolution Strategies)
1. Addressing the Small Department Size Issue:
- We postulate that our model might overlook small departments, as they are also challenging to discern with the human eye.
- **To alleviate this, we were inspired by the DINO architecture, a prominent self-supervised learning approach.**
- Similar to DINO, we crop the image and input it into our model. The SMP library allows the injection of different image sizes, negating the need to enlarge cropped images.
- Moreover, to infuse a generalization effect, we employ an augmentation method different from the original, called as “small size augmentation.”
- Two loss functions are fused equally: one from the Big-size image and the other from the small-size.
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/d78a0e66-93e3-4736-977b-1499b8365542)

2, 3. Addressing Output Holes and Unclear Boundaries:
- First, we adapted a simple morphology method to interpolate the holes. However, it increased the overall department size. After interpolation, we applied the morphology erosion method.
- Second, we looked to the winner of "Cityscape", a segmentation dataset, which introduces a straightforward Encoder-Decoder Network to enhance boundary clarity.
  - we embody the BPN network (Boundary Patch NeuralNet) to recommend the original paper. 
- Moreover, it could interpolate output holes. Thus, we omitted the morphology method due to the power of the BPN (Boundary Patch Neural) network
- The specific learning process aimed at clearer boundary development is observable.
- Unfortunately, the result wasn’t as amendable as desired. However it increase the accuracy!!
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/2e861ddc-0835-442e-9c79-d6b8e28432fa)

4. Addressing the Loss of Background Information in Patchified Images:
- We attempted to instill background information by using the Masked Autoencoder (proposed by Kamming He in 2022), a new spotligted self-supervised learning approach in ViT architectures.
- It seemed analogous to patchifying the input image, and given our substantial image dataset, learning background information seemed plausible and feasible.
- However, in our task, attention-based models exhibited poorer performance compared to CNN-based models.
- Thus, we utilized 1024x1024 pre-trained model architectures and subsequently fine-tuned the 256x256 or 224x224-sized images.

# Result.
![image](https://github.com/younghoonNa/Satellite-image-segmentation/assets/38518648/f6ffc67d-2ee6-4624-9dfc-cb8a58455f1d)
