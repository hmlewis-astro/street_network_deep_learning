# Minimum Viable Product
## Road Maps from Satellite Images for Disaster Relief Networks


The goal of this project is to create a CNN-based encoder-decoder network to extract road maps from satellite images.

To do this, I am using data from the Road Extraction Challenge in [DeepGlobe 2018: A Challenge to Parse the Earth through Satellite Image](https://arxiv.org/pdf/1805.06561.pdf). There are ~6,200 satellite annotated images (i.e., _with_ road masks) for training and validation; images are captured over Thailand, Indonesia, and India, and each image is 1024 pixels &times; 1024 pixels &times; 3 color channels (red, green, blue), with a pixel resolution of 0.5 meters/pixel. There are an additional ~2,300 images (_without_ road masks) for testing.

In pre-processing the data, to save RAM, the images are reduced to size 256 pixels &times; 256 pixels &times; 3 color channels, and the annotated masks are reduced to size 256 pixels &times; 256 pixels.


To begin building a baseline model, ...


I have opted to ...


With only minimal tuning of the anchor strength, the model achieves ...


I will continue to tune ... and test ...

Given sufficient time, I will apply this network to images of disaster zones collected before and after the onset of major crisis events.
