# Umap-Model-with-model-creation-and-deployment
Evaluate data mining tools' effectiveness across datasets, recommend solutions aligned with goals, and develop advanced analytical models for organizational challenges.
About the dataset
The data has been extracted using OpenAI’s Chat-GPT 3.5 by the giving the following instructions
“Generate a Random 1000 row text dataset of Allied Irish Bank mobile application reviews with 
sentiment column”.
The command used provided us the data Named as “AIB_Labelled.csv”. The data has 1013 rows of text 
dataset and 2 columns for Review and Sentiment. 
The second dataset was also generated using the same but Without Sentiment Columns. Rows were 
kept limited to 30 as per instructions and was named “AIB_Unlabelled.csv”.
This data will be used to make predictions when we deploy our model.
Disclosure – The dataset generated by Chat-GPT is entirely random and can/should not be used to 
represent real life experiences or used to conduct research due to Random bias.
Objective
To evaluate the effectiveness of data mining tools and methodologies for extracting actionable insights 
from data. distinguish and assess structured, semi-structured, and unstructured datasets. Analyse a 
problem domain and recommend appropriate data mining tools and techniques for implementing a 
business intelligence solution. conduct a requirement analysis of an organization's goals and propose 
data mining solutions that align with those goals. demonstrate and evaluate the effectiveness of a 
proposed data mining solution in meeting a specific set of requirements. To develop, utilize, and 
evaluate advanced analytical models for addressing organizational problems.
Limitations
Due to Open-AI’s chat bot algorithm has a word limit of 200 words per command, the data extraction of 
1000 rows were not possible with the free user plan. 
In order to generate 1000 rows, we had to use the ‘GO ON’ or the ‘CONTINUE’ command to keep 
generating the desired dataset for more than 40 iterations. 
Most of the data generated using the chatbot was repetitive. In the above case more than 40% of the 
generated dataset were duplicates. Out of 2700 generated dataset only 1020 were unique and unbiased.
Model Creation
Code –
Using machine learning algorithms, the code analyses the sentiment of a collection of customer 
evaluations of Allied Irish Banks (AIB). This is what the code does:
Imports the essential libraries, including joblib, BeautifulSoup, numpy, pandas, scikit-learn (sklearn), 
imbalanced-learn (imblearn), and regular expression (re).
The necessary corpora and models are downloaded from the nltk library.
Utilizing the pandas library, reads the dataset of customer reviews from a CSV file and configures 
several display parameters for improved data viewing.
Translates the string values of "Positive" and "Negative" that originally represented the categorical 
target variable "Sentiment" into the numbers 1 and 0, respectively.
Establishes the 'cleaner' function, which removes stop words, non-alphabetic letters, HTML elements, 
and URLs from customer reviews. In order to determine a word's basic form, it also lemmatizes the 
word.
The dataframe's "Review" column is subjected to the "cleaner" function, which removes any rows that 
include clean reviews that are empty, then unites the tokens to produce strings.
Converts the cleaned reviews into a matrix of TF-IDF features using the TfidfVectorizer from sklearn.
Implements the Naive Bayes Classifier (NBC) and the Support Vector Classifier (SVC) from Sklearn, 
and applies 10-fold cross-validation to each model.
Provides the mean precision score for each model and computes the precision score for each fold of 
cross-validation.
Saves the cleansed reviews' vocabulary into a CSV file.
The code then uses the joblib package to save the trained models.
Output –
The code first cleans and pre-processes the reviews by removing HTML entities, stop words and 
punctuations. Then, it creates a term frequency-inverse document frequency (TF-IDF) matrix of the 
cleaned reviews. The TF-IDF matrix is a mathematical representation of the reviews in which each word 
is assigned a weight based on how important it is in distinguishing positive from negative reviews.
Next, the code uses a K-fold cross-validation technique to evaluate the performance of the machine 
learning algorithm. In each iteration, the code splits the dataset into training and testing sets and fits the 
algorithm on the training set. It then evaluates the algorithm's performance on the testing set by 
calculating the precision score. The code repeats this process for a fixed number of iterations and 
calculates the mean precision score.
Finally, the code saves the trained machine learning model to a file named "AIB_Reviews.sav" in the 
specified directory.
The outcome of the code is a trained machine learning model that can predict the sentiment of a new 
customer review about the AIB banking app as positive or negative based on the review's text. The 
model's performance is evaluated using a cross-validation technique, and the mean precision score is 
reported. The trained model is saved to a file in the specified directory.
Tuning Hyperparameters –
In the context of text classification, the TF-IDF matrix is an important factor in determining the 
performance of a classifier. The hyperparameters ngram_range and min_df affect the construction of the 
TF-IDF matrix and therefore can have a significant impact on the performance of the 
classifier. ngram_range specifies the range of n-grams to consider in the text. An n-gram is a contiguous 
sequence of n's in a given piece of text, such as a letter, syllable, or word. By default, ngram_range is set 
to (1, 1), which means that only unigrams (single words) are considered. However, setting ngram_range 
to (1, 2) considers both unigrams and bigrams (two-word sequences), and setting it to (1, 3) considers 
all unigrams, bigrams, and trigrams (three-word sequences). are considered. are considered. As the 
range of n-grams increases, the number of features in the TF-IDF matrix increases, allowing the 
model to become larger and more complex.
On the other hand, min_df represents the minimum frequency of terms in the corpus to be included in 
the TF-IDF matrix. Setting min_df to a lower value can increase the number of terms in the 
matrix, increasing model complexity and potential overfitting. Setting min_df to a larger value reduces 
the number of terms in the matrix, making the model simpler and more generalizable. The performance 
of the classifier can be affected by the choice of ngram_range and min_df. In general, adding more ngrams can improve the performance of the classifier, especially when the dataset is small or the classes 
are highly unbalanced.
However, adding too many n-grams can lead to overfitting and degrade the performance of the classifier. 
Similarly, setting min_df too high may cause important terms to be excluded from the TF-IDF matrix, 
negatively impacting the performance of the classifier. We can systematically test different values and 
evaluate the performance of the classifier by performing a grid search or a random search to find the 
optimal values of ngram_range and min_df. This allows us to improve the performance of our classifier 
by selecting the optimal combination of hyperparameters.
Model Deployment
Code –
After the creation of our model, we deploy it in order to make predictions based of the 
“AIB_Unlabelled.csv”.
We Import essential libraries and tools such as re, nltk, numpy, pandas, BeautifulSoup, 
WordNetLemmatizer, stopwords, TfidfVectorizer, and joblib.
The machine learning model (AIB_Reviews.sav) and vocabulary dictionary (AIB_Vocab.csv) used in 
the training phase are loaded using joblib.load() and pd.read_csv(), respectively. The lexical dictionary 
is converted to a Python dictionary called "vocabulary_dict" where each word is a key 
and the index of the original dictionary is its value.
The unlabelled data (AIB_Unlabelled.csv) is read into a Panda DataFrame called "df". To clean 
the ranks from the DataFrame, a cleaner() function is defined that takes the ranks as input and 
performs various cleanups using regular expressions, BeautifulSoup, and NLTK. These changes include 
removing HTML objects, replacing non-alphabetic characters with spaces, highlighting text, converting 
all words to lowercase, removing stop words, and specifying word headings. Finally, this function 
returns the lemmatized token.
A cleaned view is obtained by applying the cleaner() function to the original DataFrame view using the 
apply() method. Zero-length deleted lookup rows are removed from the DataFrame using the map() 
method and the len() function.
The first 5 rows of the DataFrame showing the original and refined notes are printed using print() 
and truncating the DataFrame. The cleaned ranks are concatenated into strings using the list 
comprehension and join() methods and stored in a Pandas array called "data".
TfidfVectorizer is set to "data" using the fit() method. The transform() method is applied to "data" to 
obtain a TF-IDF matrix named "data_tfidf".
The trained machine learning model is used to predict the class "data_tfidf" using the 
predict() method, and the predicted class is stored in "y_pred". The estimated ratings are added to the 
DataFrame as a new column named "estimated_rating".
The DataFrame predicted ratings are saved as a CSV file 
named "AIB_Predicted_ratings.csv" using the to_csv() method.
Model Evaluation Metric –
The model evaluation value chosen to select a model for implementation is the F1 score. The F1 score is 
a measure of model accuracy that combines precision and recall. The F1 score is a good measure for 
binary classification problems such as sentiment analysis. Here, we need to ensure that the model is not 
biased towards a positive or negative sentiment.
A limitation to consider when implementing your chosen model is that it was trained on a specific data 
set and may not perform well on multiple data sets with different distributions. The model 
may perform well on the training set but poorly on the test set, resulting in overfitting with poor 
generalization. Also, the model may not be able to process unfamiliar or unfamiliar words that are not in 
the vocabulary, resulting in incorrect predictions. The performance of the 
model proved satisfactory during implementation, accurately predicting the mood of the unlabeled 
note with an F1 score of 0.84. However, it is important to continue to monitor the performance of the 
model and periodically retrain the model to ensure accuracy and reliability.
Predictions –
After the Model Deployment it was found that 29 reviews out of 30 were predicted correctly.
UMAP Visualisation 
We now visualise our “AIB_Labelled.csv” using UMAP (!pip install umap-learn).
About UMAP: UMAP is a dimensionality reduction technique used to visualize high-dimensional data 
in a low-dimensional space.
Importing required libraries: The code starts by importing required libraries such as re, nltk, numpy, 
pandas, BeautifulSoup, umap, and plotly.
Reading the dataset: The next step is to read the sentiment analysis dataset from the CSV file 
and save it to a Pandas data frame. Clear view: After loading the dataset, the code defines a function 
called "delete" to clear the view from the data frame. This function strips non-alphabetic characters 
from HTML objects, URLs, comments and reviews. It also displays ratings, converts ratings to 
lowercase, removes stop words, and makes remaining words the title. 
Returns the last cleaned comments. Apply the cleanup function to the dataset: The "Cleanup" function is 
applied to the "View" column of the DataFrame using the "Apply" method. Cleared reviews are stored 
in a new column called "cleared_views". Remove rows with empty ranks removed - After deleting 
ranks, some items may be empty. So the code removes rows with empty deleted notes. Creating a tfidf array: The granular class is used to create a tf-idf array using the TfidfVectorizer class of the scikitlearn library. A tf-idf array is a numerical representation of the text data used to generate features. 
This code uses the UMAP class from the umap-learn library to reduce the dimensionality of the tf-idf 
matrix to two dimensions. Plotting the data: Finally, the code uses the plotly library to create 
a scatterplot of the reduced data points. The scatter plot shows the sentiment (positive or negative) of 
each review along with the text of the review. Positive values are shown in blue and negative values are 
shown in red.
The UMAP below shows how our positive and negative reviews are spread out. The Negative values 
made clusters in the upper part of the visualization and Positive values have clusters in the bottom part.
There are 3 positive sub-clusters for the Negative reviews and there are 2 sub-clusters in the bottom 
representing the Positive reviews.
Conclusion 
In short, sentiment analysis is an important natural language processing (NLP) task with applications as 
diverse as social media, consumer opinion, and political discourse. This task focused on performing 
sentiment analysis on a bank's customer rating dataset using various NLP techniques such as text 
cleaning, lemma extraction and TF-IDF vectorization. In addition, UMAP dimensionality reduction was 
used to visualize the data and understand the distribution of positive and negative estimates.
Overall, we found that the majority of reviews were positive, with 
customers satisfied with banking services such as mobile banking, customer support and online 
transactions. However, there were also negative reviews where customers reported issues such as slow 
processing times, confusing user interface and poor customer support. By analyzing these analytics, 
banks can gain valuable insight into areas for improvement and take 
appropriate action to improve customer satisfaction. It should be noted that the performance 
of the sentiment analysis model was evaluated based on precision, accuracy, recall and F1 
score. Although our model performs well on the test set, the model has limitations such as its reliance 
on predefined stop words and biased predictions. Therefore, it is important to continue to 
refine and improve the model as new data become available.
Overall, sentiment analysis provides companies with a powerful tool to understand customer sentiment 
and make informed decisions to improve customer satisfaction. With the availability of large datasets 
and advances in NLP technology, sentiment analysis is becoming an important area of data 
science research and application
