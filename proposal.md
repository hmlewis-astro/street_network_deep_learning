# Project Proposal
## Road Maps from Satellite Images for Disaster Relief Networks

### Question & Background:
<!--_While traditional TV viewing has been dropping over the course of the coronavirus pandemic, video streaming via Netflix, Hulu, Prime Video, Disney+, YouTube, etc. has increased by more than 60% (Nielsen via [Variety](https://variety.com/2020/digital/news/coronavirus-quarantine-life-media-consumption-data-increase-1203535472/)). With (nearly) the entire Disney movie catalog available on Disney+, it has become much easier to binge-watch your favorite classic Disney animated films, Pixar, and Marvel movies. However, choosing a movie to watch becomes a much more difficult task when the opinions of two (or more!) people are involved._-->

In this project, I aim to **create a deep neural network to extract road maps from satellite images**.


### Data description:
<!--_Summaries&mdash;generally including a brief plot overview, award highlights, character names, and actor credits (longer than 100 words, on average)&mdash;for every movie produced and released by Walt Disney Pictures will be scraped from [Disney A to Z](https://d23.com/disney-a-to-z/). The scraped data consist of over 2100 movie titles and summaries._

_This website was last updated in March 2020 (around the start of the coronavirus pandemic); movies that have been released since then (e.g., Soul, Cruella, Luca) are not included in the scraped data. Note, television shows (e.g., shows on ABC, which is a Disney company) are also not included in the scraped data._-->


### Tools:
The neural network will be built, tested, and evaluated using the `tensorflow.keras` library in Python. Because the training data (i.e., satellite images _with_ available road masks) are composed of ~6,200 satellite images (each with size 1024 pixels &times; 1024 pixels &times; 3 color channels) training with a GPU will likely be necessary; Google Colab will be used for this purpose.

Visualizations of the original satellite images and the resulting, extracted road masks will be created with the `matplotlib` package in Python.

### MVP:

<!--The minimal viable product (MVP) for this project will be...-->
