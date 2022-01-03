
# Project 3
## Problem Statment
We are a group of data scientist hired by a rehabilitation center to help create a chatbot or online platform, to aid them identify users that need help. As such, we are looking into the 2 most common addictions, smoking and alcoholism, as they are the most accessible legal substances available to adults. 

From the subreddits r/alcoholicsanonymous and r/stopsmoking, we aim to identify whether a user is reaching out to address a smoking addiction or alcoholism.

We will be using Logistic Regression and Multinomial Naive Bayers build the classification model, with the following vectorizers: CVEC (Count Vectorization) and TF-IDF (Term Frequency-Inverse Document Frequency) with the use of n-grams within each to further tune the parameters.

Metrics for measure of success of the model include the train and test accuracy score, Receiver Operating Characteristic Area Under the Curve (ROC AUC), sensitivity, specificity and precision.

## Background
#### Subreddits
Reddit is an website consisting of aggregation of forums where people share news, content and discuss any topic of their choosing ([*source*](https://www.digitaltrends.com/web/what-is-reddit/)). Reddit can be further broken down into different communities known as 'subreddits', which starts with 'r/'. For instance, r/boardgames is a subreddit for people to discuss board games, while r/starwars is a subreddit for star wars enthusiast.

#### Addiction
Addiction is a condition of being addicted to a particular substance or activity, 2 of the most common forms of addiction is to alcohol and nicotine.

Alcoholism involves problems controlling a person's drinking, which persist even when it affects the person's overall quality of life. Such consumption may lead to tolerance causing the person to consume more to attain the same effect, or experiencing withdrawal symptoms when trying to cut off alcohol ([source](https://www.mayoclinic.org/diseases-conditions/alcohol-use-disorder/symptoms-causes/syc-20369243), [source](https://www.healthline.com/health/alcoholism/basics)).

Cigarette smoking tends to be correlated to a host of diseases including (but not limited to) cardiovascular disease, respiratory disease and even cancer ([source](https://www.cdc.gov/tobacco/data_statistics/fact_sheets/health_effects/effects_cig_smoking/index.htm)). Despite this knowledge that a smoker may have, it is hard to quit as cigarettes contain tabacco which often leads to addiction hence making it hard to drop the habit ([source](https://www.healthhub.sg/live-healthy/615/smoking_habitoraddiction)).

#### r/alcoholicsanonymous and r/stopsmoking
Smoking and alcoholism arise as these are the most accesible legal substances available to adults. A common thread we see between these 2 types of addiction is that the difficulty one faces when trying to break the addiction. As such, when a person is looking to quit, they often seek external help, be it seeking professional treatement or a community of like-minded people. The subreddits r/alcoholicsanonymous and r/stopsmoking provide such a community to those seeking it, and with COVID-19 and the acccompanying social restrictions, these online communities provide a feasible alternative to real life meetings and support groups.

## Datasets
Data was obtained through PushShift API to collect data from two subreddits.

1. Pushshift API Link: https://github.com/pushshift/api
- Pushshift API allows us to collect data from reddit.com and collect processable data using json.

2. alcoholicsanonymous_raw.csv
- Subreddit for discussing alcoholic recovery
- Source: https://www.reddit.com/r/alcoholicsanonymous/

3. stopsmoking_raw.csv 
- Subreddit for discussing smoking cessation
- Source: https://www.reddit.com/r/stopsmoking/

## Executive Summary
This project aims to create a classification model based on the subreddits r/alcoholicsanonymous and r/stopsmoking to classify posts based on their key feautres.

The data was scraped from both subreddits and clean through the removal of duplicate post and imputing of null values. Special characters and emojis removed via regex, and the text was cleaned through punctuation removal, tokenization and removal of stopwords. Both stemming and lemmatizing were compare to see which would be more appropriate in obtaining the root word, and lemmatizing was chosen as it produced more meaningful words. 

Both CVEC and TVEC were performed to see how each vectorize words, and unigram, bigram and trigrams were created for visualisation of the top features in each. New stopwords were added based on overlapping words detected in the n-grams.

Both logistic regression and multinomial naive bayes were chosen as potential candidates. A pipeline with gridsearch helped to determine the optimal parameters for each of the vectorizer-model combination. The final model was CVEC/multinomial NB as it produced the highest accuracy (96.9%), though all models faired well. 

## Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---| 
|subreddit|object|combined_df|Subreddist of post|
|title|object|combined_df|Title of the subreddit post|
|selftext|object|combined_df|Body text of subreddit post|
|combined_text|object|combined_df|Concatenation of title and body text of subreddit post|

## Conclusions and Recommendations
Overall, both subreddits have users that are active in searching for support and resource in their journey to ceasing the addictive substance (alcohol and cigarettes). With the top model (CVEC with multinomial NB), we are able to get a prediction with 96.9% accuracy. 

We propose that the rehabilitation center to build a chatbot using the algorithm from our model to aid the center identify users seeking help. This can be utilized in 2 main ways:
* Using the user's response to classify them into the respective group
* Presenting users with messages containing features of each group to correctly classify them

This would be incredibly useful during COVID-19 as there are less opportunities to seek out physical help. Having an outlet online, such as a platform or chatbot, would enable the rehabilitation center to make a preliminary assessment on the user, by identifying which resources and medical professional would best suit their needs.

## Future Steps
For our current model, we could optimize it by improving the list of customised stopwords in this iteration. As our data may have overlapping words from both subreddits, we could look into identifying these overlaps and remove them to narrow down the features for our model.

Another point for exploration would be expanding the scope of data collection. As reddit posts may not be as binary to solely contain just alcoholism/smoking words, there are 2 things we could look at:
1. For posts containing both smoking and alcoholism, we could refine our model to be able to classify posts as containing both features, and not just force it into a single category.
2. Some posts may contain other words pertaining mental health conditions (that often presents as comorbidities) such as depression, anxiety or bipolar. Expanding our data collection to include other subreddits would allow the model to learn and classify other conditions, making it more comprehensive.


