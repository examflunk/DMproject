### FALL 2020 -> CSE 5334 -> DATA MINING
## Project Title :- Classifier to Predict Ratings for the Reviews

#### UTID :-1001662386

**Summary :-** The goal of the project is building a classifier that predicts ratings for the reviews 
using the boardgame review dataset

The implementation of the project is as follows

- Dataset analysis
- Text Preprocessing
- Vocab and frequency list
- Models prediction
- Data resampling
- Model prediction on resampled data
- Select the best performing of models 
- Hyper parameter Tuning
- Findning the Final accuracy
- Building the live appliction


**1.Dataset analysis:-**

- Dataset has user, Id,name coulmns which are not helpful in predicting the ratings,
  so need to drop those columns
- Visulalize ratings column and we can understand that the dataset has most of the
   reviews of ratings in the range 6 to 10.
- Since the ratings column is of float type, convert it to integer using the np.round 
    on ratings coulmns.
- Looking at the comments column, it has Nan values where there ratings even though 
    they haven't commented, since we are predicting ratings based on comments  that user makes, 
    we can drop all the rows that has Nan values.
- Now we can work on text preprocessing.

**2.Text Preprocessing :-**
- Remove stopwords
- Remove digits
- Remove punctuation
- Convert text to lower
- Stemming
- Remove few text that repeats in all reviews and does not add much information to prediction

**3.Vocab list:-**
- All the reviews are tokenized and converted into words
- Create a bga of words and add all the words 
- Sum of all the words that keeps repeating 
- word frequency is list is created with the frequencies of each word in reverse order
- below shows the same way of word vectorization using count vectorizer

**4. Count Vectorization:-**
- We will be creating vectors that have a dimensionality equal to the size of our vocabulary, and if the text data features that vocab word, we will put a one in that dimension. Every time we encounter that word again, we will increase the count, leaving 0s everywhere we did not find the word even once, resulting the word vector representation of all the data.

**4. Prediction Models:-**

I have selected MultinomialNB, RandomForestclassifier, XGBoost classifier because they are normally perform better and 
XGBoost is the most model with success in the kaggale competitions

- **MultinomialNB**
The multinomial Naive Bayes classifier is suitable for classification with discrete features (e.g., word counts for text classification). The multinomial distribution normally requires integer feature counts. However, in practice, fractional counts such as tf-idf may also work.

   - alphafloat, default=1.0 -Additive (Laplace/Lidstone) smoothing parameter (0 for no smoothing).

- **RandomForest classifier**
A random forest is a meta estimator that fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting.

   - n_estimators, default=100
   
   - criterion = “gini”, “entropy” ,default=”gini”

- **XGBoost classifier**
XGBoost classifier builds an additive model in a forward stage-wise fashion, it allows for the optimization of arbitrary differentiable loss functions. In each stage n_classes_ regression trees are fit on the negative gradient of the binomial or multinomial deviance loss function.

  - learning_ratefloat, default=0.1 :-learning rate shrinks the contribution of each tree by learning_rate. There is a trade-off between learning_rate and n_estimators.
  
  - n_estimatorsint, default=100 :- The number of boosting stages to perform. Gradient boosting is fairly robust to over-fitting so a large number usually results in better performance.


**Data Resampling:-**

- Data resampling is when their is high imbalance in the dataset
- Data manipulation sampling approaches focus on rescaling the training datasets for balancing all
  class instances

**Overfitting and Hyperparameters :-** 

  **Overfitting**
- Overfitting occurs because of using a complex model that closely matches the training set but is unable to generalize to new data

**Hyperparameters tuning**
- The parameters that control the learning process are called hyperparameters and find the optimal values of those params define the hyperparametrs tuning


**Results :-**
- There types are is used
   - original data of full
   - random part of original data
   - resampled data 
   
 **performance of each model on the data**
- Multinomial NB has given the accuracies of  30.52%, 22% and 10.8% for original, fractional and resampled data          
  
- RandomForestClassifier has given an accuracy of 10.9% on the resampled 

- XGBoostClassifier has an accuracy of 10.98% of the resampled data

**Challenges**
- Volume of data is very high which caused longer time for doing the NLP(document), tried multipe ways of doing nlp of the but it processing is longer time and also getting memory out issues 
- Same issue with the Classifier randomforest and XGboost, the model prediction is taking more an hour of time and couldn't get those results, Usually XGBoost is faster but its result not produced
 - I have tried n-1 jobs in randomforest hoping to get fatser results but it hasn't.
- Next step tried with less data and i took around the size of 5000000 and tried it samething happened with the Randomforest and XGBoostclassifier took longer time still

- Later reffered to data resampling and tried to balance all the classes  
  - It has produced results of the three models
  - compared to larger dataset, these accuracy scores are less as we know that as dataset size increases,accuracy increases and it also leads to overfitting in some cases
  - XGBoost classifier has better accuracy but comparing with training accuracies it still and in case RandomforestClassifier
   it is looks like overfitting as training has very good accuracy and test it has dropped veryless
  
  - Hyperparamter is verified using XGBoost model.
 
