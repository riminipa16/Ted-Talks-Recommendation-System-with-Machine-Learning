TED Talks Recommendation System with Machine Learning

A content-based TED Talks recommendation system that uses TF-IDF text vectorization, cosine similarity, and Pearson correlation to identify talks with content similar to a user's input topic or description.

Project Overview

This project processes TED Talk titles and descriptions, cleans the text, converts the talk content into numerical TF-IDF vectors, and recommends talks based on textual similarity.

The workflow includes:

Loading the TED Talks dataset.

Exploring the dataset and checking missing values.

Extracting the year and month from the posted column.

Combining the talk title and details into a single text field.

Removing unnecessary columns and missing records.

Removing English stopwords and punctuation.

Visualizing frequently occurring words using a WordCloud.

Converting talk descriptions into TF-IDF vectors.

Calculating cosine similarity and Pearson correlation.

Ranking and displaying the most similar TED Talks.

Technologies Used

Python

Pandas

NumPy

Matplotlib

NLTK

WordCloud

SciPy

Scikit-learn

Machine Learning Approach

TF-IDF

TF-IDF (Term Frequency-Inverse Document Frequency) represents each TED Talk's text numerically based on the importance of words in the dataset.

Cosine Similarity

Cosine similarity measures how similar two TF-IDF vectors are. A higher value indicates that two talks have more similar textual content.

Pearson Correlation

Pearson correlation is also calculated between the TF-IDF vectors and is used alongside cosine similarity when ranking recommendations.

The recommendation function sorts talks primarily by cosine similarity and then by Pearson correlation, both in descending order.

Dataset

The code expects a CSV dataset containing TED Talk information, including at least the following columns:

posted

title

details

main_speaker

The current code loads the dataset using:

pd.read_csv('/content/tedx_datase.csv')

If you run the project outside Google Colab, update this path to the location of your dataset.

Project Structure

TED-Talks-Recommendation-System/
│
├── ted_talks_recommendation_system_with_machine_learning.py
├── tedx_datase.csv
└── README.md

Installation

Install the required Python packages:

pip install pandas numpy matplotlib nltk scipy wordcloud scikit-learn

Then download the NLTK English stopwords:

import nltk
nltk.download('stopwords')

How to Run

1. Prepare the dataset

Place the TED Talks CSV dataset in the project directory and make sure the filename/path matches the one used in the Python script.

2. Import the required libraries

The script uses libraries including:

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import nltk
import string
from scipy.stats import pearsonr
from nltk.corpus import stopwords
from wordcloud import WordCloud
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

3. Create the TF-IDF vectorizer

The recommender requires a fitted TfidfVectorizer before get_similarities() is called.

For example:

vectorizer = TfidfVectorizer(analyzer='word')
vectorizer.fit(df['details'])

4. Provide a topic or talk description

The script demonstrates recommendations for topics such as:

talk_content = ['Time Management and working hard to become successful in life']
recommend_talks(talk_content)

and:

talk_content = ['Climate change and impact on the health. How can we change this world by reducing carbon footprints?']
recommend_talks(talk_content)

The system then displays the most similar speakers and talk descriptions.

Example Output

For an input such as:

Time Management and working hard to become successful in life

the system ranks TED Talks according to their similarity to the supplied text.

The output contains:

main_speaker

details

Main Functions

remove_stopwords(text)

Removes common English stopwords from the supplied text.

cleaning_punctuations(text)

Removes punctuation characters from the text.

get_similarities(talk_content, data=df)

Calculates:

Cosine similarity

Pearson correlation

between the input text and each TED Talk in the dataset.

recommend_talks(talk_content, data=data)

Ranks TED Talks according to similarity and displays the top recommendations.

Important Notes

The project is a content-based recommender system. Recommendations are based on the textual content of talks rather than user ratings or collaborative filtering.

The original script was generated from a Google Colab notebook.

The dataset path currently points to /content/tedx_datase.csv, which is a Google Colab-style path.

The TF-IDF vectorizer must be initialized and fitted before calling the recommendation functions.

The original notebook has several import/vectorizer setup lines commented out for Python compatibility, so they may need to be uncommented or recreated when running the .py file independently.

The recommendation function modifies the working dataframe by adding cos_sim and pea_sim columns and sorting it.

Future Improvements

Possible improvements include:

Add a user-friendly command-line or web interface.

Use stemming or lemmatization during preprocessing.

Experiment with n-grams in TF-IDF.

Use modern sentence embeddings such as Word2Vec, GloVe, or transformer-based embeddings.

Improve recommendation speed by vectorizing the complete dataset once instead of transforming each row repeatedly.

Add filters for TED Talk year, speaker, or topic.

Return recommendation scores to the user.

Build a Streamlit or Flask application for interactive recommendations.

Evaluate recommendation quality using a suitable recommendation evaluation methodology.

Author

Rimi Moni

BSc in Computer Science and Engineering (CSE)

Canadian University of Bangladesh

License

No license is specified in the current project. Add an appropriate license if you plan to publish or distribute the project publicly.
