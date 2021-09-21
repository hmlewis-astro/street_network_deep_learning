# Project Proposal
## Road Maps from Satellite Images for Disaster Relief Networks

### Question & Background:
_While traditional TV viewing has been dropping over the course of the coronavirus pandemic, video streaming via Netflix, Hulu, Prime Video, Disney+, YouTube, etc. has increased by more than 60% (Nielsen via [Variety](https://variety.com/2020/digital/news/coronavirus-quarantine-life-media-consumption-data-increase-1203535472/)). With (nearly) the entire Disney movie catalog available on Disney+, it has become much easier to binge-watch your favorite classic Disney animated films, Pixar, and Marvel movies. However, choosing a movie to watch becomes a much more difficult task when the opinions of two (or more!) people are involved._

In this project, I aim to **create a deep neural network to extract road maps from satellite images**.


### Data description:
_Summaries&mdash;generally including a brief plot overview, award highlights, character names, and actor credits (longer than 100 words, on average)&mdash;for every movie produced and released by Walt Disney Pictures will be scraped from [Disney A to Z](https://d23.com/disney-a-to-z/). The scraped data consist of over 2100 movie titles and summaries._

_This website was last updated in March 2020 (around the start of the coronavirus pandemic); movies that have been released since then (e.g., Soul, Cruella, Luca) are not included in the scraped data. Note, television shows (e.g., shows on ABC, which is a Disney company) are also not included in the scraped data._


### Tools:
_To scrape the Disney A to Z- website, the `requests` and `BeautifulSoup` packages in Python will be utilized, along with Selenium and ChromeDriver to allow each movie summary page to fully load before scraping. The scraped data will be stored in a `.csv` file, with rows corresponding to each movie. The data will be read in to Python and manipulated using the `pandas` package._

_The text processing libraries/tools in `scikit-learn` and `NLTK` will be used to clean and pre-process the movie summaries, including removing stopwords and handling special characters. These tools will also be used to tokenize, lemmatize, and vectorize the summaries, and represent the data as a document-term matrix. I will also use NMF/LDA for **topic modeling**. I plan to use the results of the topic modeling to build a very basic **recommendation system** to suggest movies similar in topic to a user's provided favorite Disney movie._


### MVP:

_The minimal viable product (MVP) for this project will be..._
