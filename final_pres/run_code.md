# How To:
### Running the code in this repo

The code for this analysis is broken into multiple pieces to avoid re-running pieces that take a significant amount of time. To produce the results presented here, run the code in the following order:

- `pkl_data.ipynb` &mdash; [this notebook](https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/pkl_data.ipynb) downloads the DeepGlobe 2018: Road Extraction Challenge data from Kaggle; reduces the image size to size 256 pixels &times; 256 pixels &times; 3 color channels
- `unet_base_model.ipynb` or `unet_base_model_colab.ipynb` &mdash; [this notebook](https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/unet_base_model_colab.ipynb) establishes the baseline UNet model (i.e., without dropout, standard ReLU activation function, no testing of optimizer, loss function, etc. combinations); some sample predictions from the model are saved to the `figures` folder (`figures/predicted_road_map_base_model_*.png`)
- `unet_tuned_model.ipynb` &mdash; the final model is presented in [this notebook](https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/unet_tuned_model.ipynb); the model uses the `ReduceLROnPlateau` and `EarlyStopping` callbacks to train the model, and the `ModelCheckpoint` callback to write the best weights to a file (`satellite_segmentation.h5`); some sample predictions from the final model are saved to the `figures` folder (`figures/predicted_road_map_final_model_*.png`)
- `model_metrics_plot.ipynb` &mdash; [this notebook](https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/model_metrics_plots.ipynb) plots the model metrics&mdash;loss, F1 score, accuracy, recall, precision)&mdash;as a function of training epoch
- `final_model_predictions.ipynb` &mdash; the model is applied to satellite images taken pre- and post-disaster (Hurricane Ida, New Orleans, August 2021) in [this notebook](https://github.com/hmlewis-astro/street_network_deep_learning/blob/main/final_model_predictions.ipynb) to identify accessible roads