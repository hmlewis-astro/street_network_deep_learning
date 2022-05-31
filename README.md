# Project Write-Up
## Road Maps from Satellite Images for Disaster Relief Networks


### Abstract

The goal of this project was to create a deep neural network to extract road maps from satellite images, with the ultimate objective of applying this network to images of disaster zones collected before and after the onset of major crisis events (e.g., earthquakes, floods, etc.) to identify accessible roads. I utilized data from the Road Extraction Challenge in [DeepGlobe 2018 (Demir et al. 2018)](https://arxiv.org/pdf/1805.06561.pdf) to build an image segmentation convolutional neural net with a U-Net-like architecture; the model is tuned to optimize the F1-score, and attains F1 = 0.690. After finalizing the optimum model weights, I applied the model to images of New Orleans, Louisiana collected before and after the impact of Hurricane Ida in August 2021 to identify roads that remained accessible (i.e., not flooded).


### Design

Remote satellite images are an extremely valuable resource in disaster zones, where maps and accessibility information are crucial for emergency response networks to delivery aid. Rather than relying on ground-based efforts to determine areas in most dire need of immediate aid, high-resolution satellite imagery can be used to identify impacted areas. However, disaster zones may span large land areas; meticulously searching satellite images by-hand can be time consuming and delay the dispatching of life-saving aid. In these cases, deep learning can play an important role. Specifically, a neural net trained to extract road maps from satellite images can be applied to images taken before and after a disaster to identify roads that have become inaccessible following a disaster.

In this project, I seek to create a deep neural network to extract road maps from satellite images, and to apply this neural network to images of disaster zones collected before and after the onset of major crisis events.

### Data

The DeepGlobe 2018 Road Extraction Challenge provide ~6,200 satellite images _with_ available hand-annotated road masks captured over Thailand, Indonesia, and India. Each image is 1024 pixels &times; 1024 pixels &times; 3 color channels (red, green, blue), with a pixel resolution of 0.5 meters/pixel. The images sample rural and urban areas, different types of road surfaces (unpaved, paved, dirt roads), etc., illumination conditions, and road densities.

In pre-processing the data, to save RAM, the images are reduced to size 256 pixels &times; 256 pixels &times; 3 color channels, and the annotated masks are reduced to size 256 pixels &times; 256 pixels. In future iterations of this work, images will _not_ be reduced in size, and, instead, will be loaded in batches into RAM.

I also apply this neural network to images released by [Maxar's Open Data program](https://www.maxar.com/open-data/) collected before and after Hurricane Ida hit New Orleans in August 2021. Though these images are not a standard size (i.e., not all are 1024 pixels &times; 1024 pixels), each image has the same 3 color channels (red, green, blue) and pixel resolution.


### Algorithms

The baseline model is built with a U-Net-like architecture, following the example laid out in the [keras documentation](https://keras.io/examples/vision/oxford_pets_image_segmentation/). The model is composed of an encoder&mdash;which takes image inputs from the training set, and performs the convolution and pools/downsamples&mdash;and a decoder&mdash;which takes as input the pooled indices from the final encoder pooling layer, and deconvolves and unpools/upsamples&mdash;to predict pixel-wise class labels (here, background or road). The ReLU activation function is applied in all layers. The encoder-decoder framework is followed by an output layer consisting of a 2D convolution with 1 neuron and the sigmoid activation function. The baseline model used the `adam` optimizer, binary cross-entropy as the loss function, and was scored based on the accuracy (95.34%); however, because the annotated images contain ~5% road and ~95% background pixels, high accuracy can be achieved by a baseline model by simply assuming that all pixels are background. For this reason, all future iterations of the model were scored on F1 (the standard metric for aerial image segmentation models).

After testing various combinations of optimizers, loss functions, dropout amounts, etc., the final model includes dropout layers between each convolutional block, and `RMSprop` optimizer is used with the binary cross-entropy loss function. The architecture of the final model can be found [here](https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/unet_final_model_architecture.png). The final model achieves an F1 = 0.690, and performs well on rural and urban landscapes, and varying road surfaces and densities.

Below are a sample of the predicted road maps from the final model, with the satellite image on the left, the hand-annotated road map in the center, and the predicted road map on the right:
<p float="left" align="center">
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/predicted_road_map_final_model_3448.png" width="700" />
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/predicted_road_map_final_model_2066.png" width="700" />
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/predicted_road_map_final_model_5161.png" width="700" />
</p>


#### Application & Visualization

I also applied the model to images released by Maxar showing the impact of Hurricane Ida on New Orleans in August 2021. Though only a handful of images are publicly available currently, they show some of the areas most impacted by this event, with significant flooding covering almost all visible land area after the hurricane hit, as shown by the figure below. The model does not identify many (if any) roads in the post-event images, as expected, given that the available images generally show the areas with the worst outcomes from the hurricane.

Below are satellite images taken before and after the impact of Hurricane Ida, along with the predicted road maps from the model presented here. In the first set of figures, after the impact of the hurricane, no accessible roads are identified by the model; in the second set of figures, the only accessible road identified by the model is a raised bridge.

<p float="left" align="center">
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/hurricane_ida_predicted_road_map_final_model_0.png" width="700" />
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/hurricane_ida_predicted_road_map_final_model_1.png" width="700" />
</p>


### Tools
- Pandas and Numpy for data analysis and exploration
- Tensorflow and Keras for building, tuning, training, and testing the various baseline and final models
- Google Colab (with GPU) for computing
- OpenCV for image processing
- Matplotlib and visualkeras for plotting and visualizations

### Communication

In addition to the slides and visuals presented here, this write-up and included visuals will be included in a forthcoming blog post.
