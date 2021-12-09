# MediaBiasAnalysis
## Dave McKinley

Business Overview
The good people at Allsides.com try to help people "easily identify different perspectives so you can get the full picture and think for yourself." Today's media is very biased. And a lot of media sources are very acessible. As shown in National Academy of Sciences Paper, newsfeeds are often an echo chamber based on thier history of related articles and newsites, especially on Facebook. By nature, echo chambers remove media sources outside of someone's chamber, making it difficult to understand different view points regarding news events.

A <a href="https://news.stanford.edu/2019/08/22/the-power-of-language-how-words-shape-people-culture/">Stanford article</a>  points out "Studying how people use language – what words and phrases they unconsciously choose and combine – can help us better understand ourselves and why we behave the way we do." By paying attention to the words used in a article, the reader can critically think about what the article is presenting. Know what words and terms determine bias creates trasparency about topics in the article. The reader can know certain words and phrases are used in different biased articles and go deeper into the article to think about why the author used the words they did, or what message are they sending by using that word. Helping people become aware of what words and phrases drive bias in news media content can help the people understand the both sides of an argument.

People who do want to explore both side of an argument may visit a site like AllSides.com to guage a news site's bias. Allsides uses many methods to rate bias, including third party data with the requirement of transparency in the system. I have developed a model to determine bias in a corpus of news articles based on the laguage used in each article. To add transparency and explainability to my model I have utilized LIME to show what words and phrases leading to a better understanding of media bias and more informed readers

Data Understanding
This data was gathered from <a href="https://components.one/datasets/all-the-news-2-news-articles-dataset/">the website</a>  and <a href="https://www.kaggle.com/snapcrack/all-the-news">Kaggle</a> . The Kaggle dataset was created from the original source site but different for a different database. 

I began by looking at the data and understanding I would only be able to predict left, center or right. From there I decided to select two left foused, two center focused and two right focused media outlets. The news sources were determined by looking at Allsides.com Media Bias lists and selecting sources that each independent side agreed on. After selecting my sources, I gathered the articles in one DataFrame. In total, I gathered approximately 85,000 articles from from the two datasets. Each row contains an article, publisher and bias label. For modeling I will use the article and bias.

![alt text](https://github.com/DaveMcKinley/MediaBiasAnalysis/blob/main/images/pub_bias.png?raw=true)

This data set could be used to its full potential with better computing power. The article corous also has a limited amount of right leaning news sources. There is an abundance of left leaning sources. With a greater variety of sources, I would like to expand this classifer.

### Data Cleaning

Text Classification projects requre two steps to preparing data for modling. The first step is prerocessing the data to remove any noise from the documents. The next step is vectorizing the data for the models to use. <br><br>
Preprocessing:<br><br>

In the preprocessing step of the project if followed these steps:<br>
-   Lower case each word
-   Remove unwanted noise from the article(such as Twitter mentions, web adresses and other content)
-   Remove all numbers
-   Tokenize the list
-   Remove common stop words and punctuation
-   Lemmatizes each word
-   Returns a string of the remaining lemmatized words<br><br>
   
Fist I lowercase all the words to simplfy cleaning process. I then remove noice like mentions(@abc1123), hastags(#), and urls because they do not add anything to analysis. I also remove information at the end of The Hill's articles because it is contact information and does not help with analysis. Numbers are removed because they have no context by themselves. We tokenize the list and remove any common stopwords and punctuation.  Tokenizing a list is breaking each element in the list into its own list object. Next, I lemmatized the remaining words and combines the tokens back into a string to be vectorized.

Vetorizing

Once there is a string of processsed data. I use a Term Frequency-Inverse Document Frequency (TFIDF) vectorizer to vectorize the words in each document documents.


### Modeling

For this project I explored many different models. To keep things short in this notebook I have showcased a baseline, simple and 4 other models followed by my final model and evaluation. You can find the rest of the models along with tuning in the Modeling Notebook in the Notebooks folder. I went through Logsistical regression, Naive Bayes, Decision Trees, and XGboost Models, in addition to a neural network. I go more in depth in the Modeling Notebook


### Evaluation
![alt text](https://github.com/DaveMcKinley/MediaBiasAnalysis/blob/main/images/con_mat.png)

The XGBoost ensemble performed well on the hold out set. The model achieved an accuracy of 88.9%. While it is slightly overfit, more tunning hyperparameters will help the over all performance of the model. The final model is having the same trouble distinguishing between right to left compared to left or right to center. This would be interesting to dive into deeper. The LIME Explainer shows the most important words are "Donald" "President", and "missile" are some of the top words being used to predict bias.

![alt text](https://github.com/DaveMcKinley/MediaBiasAnalysis/blob/main/images/output.png)
### Next Steps

I would like to work with the model more to improve its power and capabilities. I would like to explore a more robust dataset with more news sources. Explore language transformers like BERT and GPT3. Investigate topic analysis of the corpus. Add a subjectivity analysis score to the articles. And finally, I would like to create an app or browser extension for people to use no matter what site they visit. 



├── images <br>
├── notebooks
├── README.md
├── Presentation.pdf
├── enviornment.yml
└── FinalNotebook.ipynb
