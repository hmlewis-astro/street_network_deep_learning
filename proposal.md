# Project Proposal
## Road Maps from Satellite Images for Disaster Relief Networks

### Question & Background:
<!--_While traditional TV viewing has been dropping over the course of the coronavirus pandemic, video streaming via Netflix, Hulu, Prime Video, Disney+, YouTube, etc. has increased by more than 60% (Nielsen via [Variety](https://variety.com/2020/digital/news/coronavirus-quarantine-life-media-consumption-data-increase-1203535472/)). With (nearly) the entire Disney movie catalog available on Disney+, it has become much easier to binge-watch your favorite classic Disney animated films, Pixar, and Marvel movies. However, choosing a movie to watch becomes a much more difficult task when the opinions of two (or more!) people are involved._-->

In this project, I aim to **create a deep neural network to extract road maps from satellite images**.


### Data description:
These data come from the Road Extraction Challenge in [DeepGlobe 2018: A Challenge to Parse the Earth through Satellite Image](https://arxiv.org/pdf/1805.06561.pdf). The data are composed of ~6,200 satellite images _with_ available road masks for training, and an additional ~2,300 images (no road masks) for validation and testing, all of which are sampled from the [DigitalGlobe +Vivid Images](https://dg-cms-uploads-production.s3.amazonaws.com/uploads/document/file/2/DG_Basemap_Vivid_DS_1.pdf) dataset. Images are captured over Thailand, Indonesia, and India, and each image is 1024 pixels &times; 1024 pixels &times; 3 color channels (red, green, blue), with a pixel resolution of 0.5 m/pixel.

The images sample uniformly over rural and urban areas, different types of road surfaces (unpaved, paved, dirt roads), etc. and illumination conditions, the road density, and the structure of the street networks are diverse. The dataset was created by GIS experts, and the pixel-wise road segmentation masks were created by professional annotators.

<!--We formulate the task of road extraction from satellite images as a binary classification problem. Each input is a satellite image. The solution is expected to predict a mask for the input (i.e., a binary image of the same height and width as the input with road and non-road pixel labels). (Demir et al. 2018)-->

<!--We use the pixel-wise Intersection over Union (IoU) score as our evaluation metric for each image, defined as Eqn. (1).
IoU_i = TP_i / (TP_i + FP_i + FN_i)
where TP_i is the number of pixels that are correctly predicted as road pixel, FP_i is the number of pixels that are wrongly predicted as road pixel, and FN_i is the number of pixels that are wrongly predicted as non-road pixel for image i. Assuming there are n images, the final score is defined as the average IoU among all images (Eqn. (2)).
mIoU = 1 / n SUM_i=1_n IoU_i-->


### Tools:
The neural network will be built, tested, and evaluated using the `tensorflow.keras` library in Python. Because the training data (i.e., satellite images _with_ available road masks) are composed of ~6,200 satellite images (each with size 1024 pixels &times; 1024 pixels &times; 3 color channels) training with a GPU will likely be necessary; Google Colab will be used for this purpose.

Visualizations of the original satellite images and the resulting, extracted road masks will be created with the `matplotlib` package in Python.

### MVP:

<!--The minimal viable product (MVP) for this project will be...-->
