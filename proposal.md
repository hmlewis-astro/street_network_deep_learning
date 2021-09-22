# Project Proposal
## Road Maps from Satellite Images for Disaster Relief Networks

### Question & Background:
Remote satellite images are an extremely valuable resource in disaster zones, where maps and accessibility information are crucial for emergency response networks to delivery aid. Rather than relying on ground-based efforts to determine areas in most dire need of immediate aid, high-resolution satellite imagery can be used to identify impacted areas. However, disaster zones may span large land areas; meticulously searching satellite images by-hand can be time consuming and delay the dispatching of life-saving aid.

In these cases, deep learning can play an important role. Specifically, a neural net trained to extract road maps from satellite images can be applied to images taken before and after a disaster to identify roads that have become inaccessible following a disaster.

In this project, I aim to **create a deep neural network to extract road maps from satellite images**. Given sufficient time, I will apply this neural network to images of disaster zones collected before and after the onset of major crisis events.


### Data description:
These data come from the Road Extraction Challenge in [DeepGlobe 2018: A Challenge to Parse the Earth through Satellite Image](https://arxiv.org/pdf/1805.06561.pdf). The data are composed of ~6,200 satellite images _with_ available road masks for training and validation, and an additional ~2,300 images (no road masks) for testing, all of which are sampled from the [DigitalGlobe +Vivid Images](https://dg-cms-uploads-production.s3.amazonaws.com/uploads/document/file/2/DG_Basemap_Vivid_DS_1.pdf) dataset. Images are captured over Thailand, Indonesia, and India, and each image is 1024 pixels &times; 1024 pixels &times; 3 color channels (red, green, blue), with a pixel resolution of 0.5 meters/pixel.

The images sample uniformly over rural and urban areas, different types of road surfaces (unpaved, paved, dirt roads), etc. and illumination conditions, the road density, and the structure of the street networks are diverse. The dataset was created by GIS experts, and the pixel-wise road segmentation masks were created by professional annotators.

Given sufficient time, I will apply this neural network to images released by [Maxar's Open Data program](https://www.maxar.com/open-data/) from e.g., Hurricane Ida in New Orleans (Aug. 2021), the Oregon&ndash;Washington Fires (Sept. 2020), or the Beirut Explosion (Aug. 2020). The Maxar data provides archived images of each location prior to disaster, as well as up-to-date imagery of disaster zones collected soon after the onset of each event.

<!--We formulate the task of road extraction from satellite images as a binary classification problem. Each input is a satellite image. The solution is expected to predict a mask for the input (i.e., a binary image of the same height and width as the input with road and non-road pixel labels). (Demir et al. 2018)-->

<!--We use the pixel-wise Intersection over Union (IoU) score as our evaluation metric for each image, defined as Eqn. (1).
IoU_i = TP_i / (TP_i + FP_i + FN_i)
where TP_i is the number of pixels that are correctly predicted as road pixel, FP_i is the number of pixels that are wrongly predicted as road pixel, and FN_i is the number of pixels that are wrongly predicted as non-road pixel for image i. Assuming there are n images, the final score is defined as the average IoU among all images (Eqn. (2)).
mIoU = 1 / n SUM_i=1_n IoU_i-->


### Tools:
The neural network will be built, tested, and evaluated using the `tensorflow.keras` library in Python. Because the training data (i.e., satellite images _with_ available road masks) are composed of ~6,200 satellite images (each with size 1024 pixels &times; 1024 pixels &times; 3 color channels) training with a GPU will likely be necessary; Google Colab will be used for this purpose.

Visualizations of the original satellite images and the resulting, extracted road masks will be created with the `matplotlib` package in Python.

### MVP:

The minimal viable product (MVP) for this project will be a baseline neural network that incorporates transfer learning (i.e., pretrained on ImageNet). This baseline model will be scored&mdash;likely using F1, the typical metric for aerial image segmentation models&mdash;and future iterations of the model will aim to improve this score by adding/removing nodes or layers, using dropout, tuning the decision threshold, etc.
