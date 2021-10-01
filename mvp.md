# Minimum Viable Product
## Road Maps from Satellite Images for Disaster Relief Networks


The goal of this project is to create a CNN-based encoder-decoder network to extract road maps from satellite images.

To do this, I am using data from the Road Extraction Challenge in [DeepGlobe 2018: A Challenge to Parse the Earth through Satellite Image](https://arxiv.org/pdf/1805.06561.pdf). There are ~6,200 satellite annotated images (i.e., _with_ road masks) for training and validation; images are captured over Thailand, Indonesia, and India, and each image is 1024 pixels &times; 1024 pixels &times; 3 color channels (red, green, blue), with a pixel resolution of 0.5 meters/pixel. There are an additional ~2,300 images (_without_ road masks) for testing.

In pre-processing the data, to save RAM, the images are reduced to size 256 pixels &times; 256 pixels &times; 3 color channels, and the annotated masks are reduced to size 256 pixels &times; 256 pixels.

The baseline model is built with a U-Net-like architecture. The model is composed of an encoder&mdash;which takes image inputs from the training set, and performs the convolution and pools/downsamples&mdash;and a decoder&mdash;which takes as input the pooled indices from the final encoder pooling layer, and deconvolves and unpools/upsamples&mdash;to predict pixel-wise class labels (here, background or road). The architecture of this network is detailed below, and follows the example laid out in this [keras documentation](https://keras.io/examples/vision/oxford_pets_image_segmentation/).

- Each block in the encoder consists of two convolutions (2D convolution, with batch normalization and the ReLU activation function), followed by a max pooling layer. At each block in the encoder the number of filters (i.e., the number of neurons) increases by a factor of 2, from 16 filters in the first block to 256 in the fifth block (the output of the encoder).

- Each block in the decoder consists of a two convolutions (2D transposed convolution, with batch normalization and the ReLU activation function), and an upsampling layer.  At each block in the decoder the number of filters decreases by a factor of 2, from 128 filters in the first block to 16 in the fourth block (the output of the decoder).

- The encoder-decoder framework is followed by an output layer consisting of a 2D convolution with 1 neuron and the sigmoid activation function.

- The baseline model uses the `adam` optimizer, binary cross-entropy as the loss function, and is scored based on the accuracy.

Currently, the model is scored on accuracy; however, I am in the process of converting the scoring metrics to F1 (standard metric for aerial image segmentation models) and/or mean Intersection over Union (mIOU, metric requested for the DeepGlobe Challenge). With only 5 training epochs, the model achieves an accuracy score of 0.9534 on the validation set.

Below are a sample of the predicted road maps from the baseline model:
<p float="left" align="center">
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/predicted_road_map_1347.png" width="800" />
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/predicted_road_map_3747.png" width="800" />
  <img src="https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/figures/predicted_road_map_5029.png" width="800" />
</p>

The annotated images contain ~4.5% road and ~95.5% background pixels, so it will be important to score the model on F1 rather than accuracy, because high accuracy can be achieved by simply assuming that all pixels are background.

After converting the scoring metric to the F1 score, I will continue to improve the model score by:
1. moving to Google Colab to run on a GPU,
2. adding dropout to avoid over fitting,
3. trying the ELU/LeakyReLU activation functions,
4. trying different optimizers (e.g., `RMSprop`, `SGD`),
5. training for more epochs with early stopping and reduced learning rate on plateau.

Given sufficient time, I will apply this network to images of disaster zones collected before and after the onset of major crisis events.
