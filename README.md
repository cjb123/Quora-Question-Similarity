<h1 style="color:red"> 1. Business Problem </h1>
<h2> 1.1 Description </h2>

<p>Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.</p>
<p>
Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.
</p>
<br>
> Credits: Kaggle 


 Problem Statement 
1. We have to identify which questions asked on Quora are duplicates of questions that have already been asked. 
2. This could be useful to instantly provide answers to questions that have already been answered and also users don't have to answer semantically similar questions again and again.


<h2> 1.2  Sources/Useful Links</h2>
- Source : https://www.kaggle.com/c/quora-question-pairs
<br><br> Useful Links:<br>

- Discussions : https://www.kaggle.com/anokas/data-analysis-xgboost-starter-0-35460-lb/comments
- Kaggle Winning Solution and other approaches: https://www.dropbox.com/sh/93968nfnrzh8bp5/AACZdtsApc1QSTQc7X0H3QZ5a?dl=0
- Blog 1 : https://engineering.quora.com/Semantic-Question-Matching-with-Deep-Learning
- Blog 2 : https://towardsdatascience.com/identifying-duplicate-questions-on-quora-top-12-on-kaggle-4c1cf93f1c30
 
 <h2> 1.3  Real world/Business Objectives and Constraints</div> </h2>
 1. The cost of a mis-classification can be very high.
2. You would want a probability of a pair of questions to be duplicates so that you can choose any threshold of choice.
3. No strict latency concerns.
4. Interpretability is partially important.

<h1 style="color:red">2. Machine Learning Problem </h1>
<h2> 2.1 Data</div> </h2>
<p> 
- Data will be in a file Train.csv <br>
- Train.csv contains 5 columns : qid1, qid2, question1, question2, is_duplicate <br>
- Size of Train.csv - 60MB <br>
- Number of rows in Train.csv = 404,290
</p>

<p> It is a binary classification problem, for a given pair of questions we need to predict if they are duplicate or not. </p>

<h2> 2.2 Performance Metric </h2>
Source: https://www.kaggle.com/c/quora-question-pairs#evaluation

Metric(s): 
* log-loss : https://www.kaggle.com/wiki/LogarithmicLoss
* Binary Confusion Matrix




<h2>$ Observations...$</h2>


^^^ USING TFIDF WEIGHTED WORD2VEC ^^^

1. For SVM , LR, XGBoost the train log-loss  test log-loss is almost similar.So no overfitting is expected.

2. XGBOOST is a more complex model than SVM and SVM is  a more complex model than Logistic Regression.So, giving similar accuracy(slightly better in xgBoost)signifies that there is very less or no underfitting.

^^^ USING TFIDF WEIGHTED W2V ^^^

1. In these models also, the train and test accuracy(log-loss) are relatively close.So no overfiiting expected.

2. The LR model gives a fairly good test accuracy(0.394);SVM with l2 regulization and random hyperparameter gives similar accuracy(0.393).But XGBOOST gives a worser accuracy(0.593). XGBOOST is a fairly complex model,but it gives an accuracy similar to LR and SVM models(train: 356 ; test: 359).Since a complex model like xgBoost gives a fairly good accuracy and even lower than a  less complex model like LR and SVM, we can expect no underfitting.


NOTE: However, in all the models we see that although the log-loss is significantly lower than that given by a random model,but the precision and specially recall for negative class(non similar question) is low.Low recall(like 0.644) for negative class can be really harmful considering the business constraints of this problem.Low recall for negative class implies that the number of False positives are high.So two non similar questions will be categorized as similar by the models and so will have same answers which will hamper the reader's experience.