# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP


## Table of Contents
|Folder Name|File Name|File Description|
|---        |---      |---             |
|main|`README.md`| This README file contains an executive summary of the whole project.|
|data|`ask_men.csv`|This contains AskMen subreddit posts scrapped from Reddit.|
|data|`ask_women.csv`|This contains AskWomen subreddit posts scrapped from Reddit.|
|data|`men_women_posts_cleaned.csv`|This contains the combined posts from both subreddits that have been cleaned.|
|data|`men_women_posts.csv`|This contains the combined posts from both subreddits.|
|notebooks|`01_data_collection.ipynb`|In this notebook, I performed my data collection from Reddit.|
|notebooks|`02_data_cleaning_eda.ipynb`|In this notebook, I clean the data and perform EDA.|
|notebooks|`03_preprocessing_modeling_evaluation.ipynb`|In this notebook, I preprocess the data, create models on the data, and evaluate my best model's performance.|

----
## Problem Statement

The subreddits r/AskWomen and r/AskMen serve as online communities for people to share their experiences, questions and opinions on a vast array of topics reguarding relationships, gender issues, service or product recommendations, plus so much more. As a social experiment, I set out to build an NLP model that can analyze and compare the language used by users posting in the AskWomen and AskMen subreddits. I wanted my model to be able to distinguish any gender-based differences for questions asked, topics discussed, etc. With this language analysis, we can try to get insight on how gender might affect social interactions, specifically online. My hope is for this NLP model to serve as a tool for researchers and everyday people who are interesting in how language might affect social identities.


----
## Data Collection and Preprocessing

I used Pushshift's API to collect posts from the subreddits r/AskWomen and r/AskMen. I was able to gather a total of 4,994 from AskWomen and 4,990 from AskMen, which I then stored in a dataframe. I cleaned the data and decided I would only use the "title" column for word analysis because "selftext" was dominantly marked with "[removed]" or null. I then had to binarize the subreddit column, so "AskWomen" was set to 1 and "AskMen" was set to 0. I was then able to perform EDA to look at character and word count distributions, top occuring words and bigrams for each subreddit, and create a customized list of stopwords based on my findings. I made my own lemmatizer and preprocessor that kept only roots of words, lowercased everything, and removed punctuations, both of which I would implement when count-vectorizing. 

----
## Model Production
Once I completed my eda and preprocessing, I began modelling. The estimators I created models with were logistic regression, naive bayes and random forest. I gridsearched to find the best hyperparameters for each and found that logisitic regression test accuracy score was the best by a small amount. I went a step further by using ada boosting with the logistic regression estimator as well as bagging with the logistic regression estimator and got test accuracy scores close but not higher than before. For my final model, I created a stacked model with level 1 estimators: logistic regression, naive bayes, bagging classifier, and ada boost classifier and the final estimator of logistic regression. This model had the best test accuracy score, which was 62.2%. I found specificity to be 59.6% and recall to be 64.7%, so there were a little more false positives (ie misclassified AskMen posts). I looked at each type of misclassified post and their top words, bigrams and trigrams to find any overlap. The top words and bigrams contained a decent amount of overlap with words pertaining to relationship talk, "advice", and  "best friend". The trigrams for misclassified AskWomen did show an interesting trend as most of them referred to "son", "work", "job", and "bos" (probably boss).

----
## Conclusion and Recommendations 


