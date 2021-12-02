# MediaBiasAnalysis
## Dave McKinley

### Overview

Today's media is very biased. And a lot of media sources are very acessible. People's newsfeeds are often an echo chamber based on thier history of related articles and newsites. By nature, echo chambers remove media sources outside of someone's chamber, making it difficult to understand different view points regarding news events. By knowing a media source's bias, the reader can critically think about what the article is presenting. People who do want to explore both side of an argument may visit a site like AllSides.com to guage a news site's bias. Allsides uses many methods to rate bias, including third party data with the requirement of transparency in the system. This project has two goals. One is to develop a model to correctly identify bias is news articles. The other is to explain how the model made its decisions. 

### Data Collection

This data was collected from two sources found here:https://components.one/datasets/all-the-news-articles-dataset and https://components.one/datasets/all-the-news-2-news-articles-dataset. I used allsides.com and mediabiasfactcheck.com's ratings to determine what sources had what leaning. Based on available sources, I decided on using left, center and right classes and using two publications per class. The data used for modeling was combined from the two sources. Articles from The Hill and Vox came from the first dataset, the remaining artciles came from the second dataset. I narrowed the working DataFrame to publication and content columns. I then assigned the bias based on the ratings systems previously mentioned.

### Data Cleaning

Text Classification projects requre two steps to preparing data for modling. The first step is prerocessing the data to remove any noise from the documents. The next step is vectorizing the data for the models to use. 
Preprocessing:

In the preprocessing step of the project if followed these steps:
    Lower case each word
    Remove unwanted noise from the article(such as Twitter mentions, web adresses and other content)
    Remove all numbers
    Tokenize the list
    Remove common stop words and punctuation
    Lemmatizes each word
    Returns a string of the remaining lemmatized words
Fist I lowercasing all the words to simplfy cleaning process. I then remove noice like mentions(@abc1123), hastags(#), and urls because they do not add anything to analysis. I also remove information at the end of The Hill's articles because it is contact information and does not help with analysis. Numbers are removed because they have no context by themselves. We tokenize the list and remove any common stopwords and punctuation.  Tokenizing a list is breaking each element in the list into its own list object. Next, I lemmatized the remaining words and combines the tokens back into a string to be vectorized.

Vetorizing

Once there is a string of processsed data. I use a Term Frequency-Inverse Document Frequency (TFIDF) vectorizer to vectorize the documents. The TF-IDF Vectorizer weight is found by measuring the Term Frequency and Inverse Document Frequency. Term frequency is how many times a term appears in the docuemnt divded my the number of terms in document. The Inverse Document Frequency is the log loss of the total number of documents divided by the number of documents with the term in it. It is based on the idea that rare words contain more information about the content of a document than words that are used many times throughout all the documents. Now our corpus of articles is ready for modeling.

### Modeling

Before deciding what models to tune, I decided to run a cross validation on the data. I noticed Logitsic Regression and support Vector Machines are not over fitting the data while still performing well. Let's see if hypertuning the parameters can boost performance. The Decision Tree and Random Forest Classifiers are extremely overfit to the training data. I will only do a grid search on the Decision Tree Classifier because it is extremely expensive to run a grid search on Random Forest Classifier. Lastly, the Multinomial Naive Bayes did not perform well so I will skip the grid search on this model.

Best performing Model:

It is difficult to explain how certain models, like a neural network, work under the hood. Opening the black box of accurate complex models is an important aspect of this project. While I do want to accurately predict bias, I also want to understand what is driving decision making and be able to showcase what words are driving decisions. So I used the LIME explainer to show what words are driving the models decision. 

### Evaluation


### Next Steps




├── images
├── notebooks
├── README.md
├── Presentation.pdf
└── MVPNotebook.ipynb
