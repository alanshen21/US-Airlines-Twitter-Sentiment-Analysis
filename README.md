# US-Airlines-Twitter-Sentiment-Analysis
This is an NLP project analyzing stock market reaction of selected US airlines using twitter sentiment during COVID-19

Twitter Sentiment and Stock Market Reactions:
Evidence from U.S. Airlines during
the Covid-19


Abstract


This study examines the information
content of firm-specific sentiment extracted from Twitter messages during the
Covid-19. Using a sample of U.S. airline companies and multinominal naïve bayes
classifiers, we investigate the association between Twitter sentiment and sto



ck market returns. Our results show
that daily firm-specific sentiment is highly correlated with market returns and
has significant predictability for future returns. Collectively, although most Twitter users are believed to be
uninformed, our findings show that the daily firm-level Twitter sentiment
contains information that is not reflected in stock prices.


1. Introduction



In
behavioral economics, investor sentiment has frequently been considered an
important factor in determining asset prices because it reflects the
expectation of market participants on future returns and investment risk (De
Long et al., 1990; Baker and Wurgler, 2006; Stambaugh et al., 2012).
Traditionally, sentiment is measured by observing analyst estimates, survey data,
news stories, and technical indicators such as put/call ratios and relative
strength indicators. However, these indicators only reflect a limited subset of
investors and usually they are measured untimely. With the rise of the
Internet, individual investors are increasingly relying on each other as
peer-to-peer sources of information. The biggest revolution in the
dissemination of information on the Internet has been the advent of social
media platforms such as Twitter, which allow users to post their views about
stocks instantaneously to a broad audience. Prior studies have examined the
role of social media in capital markets. They find that Twitter sentiment has a
significant impact on trading volume (Duz Tan and Tas, 2020) and abnormal
returns (Gu and Kurov, 2020).



The
main challenge faced by researchers who investigate the impact of firm-level
Twitter sentiment on financial markets is that discovering and analyzing all
relevant tweets is difficult, if not impossible. Existing studies mainly
examine tweets around specific events and perform textual analysis using
existing word classifications and the relative frequency of terms “bullish” and
“bearish” in tweets to measure investor sentiment. Although straightforward,
lexicon-based methodologies are subject to significant measurement errors
(Loughran and McDonald 2011). This is especially true for the analysis of posts
on social media. The content of Twitter messages is likely to be quite
different from that of newspapers and corporate documents.



To
further understand the effectiveness of using Twitter sentiment analysis as an
indicator of stock market reactions, we focus on U.S. airline companies during
Covid-19. The airlines have remained one of the hardest-hit global industries
since the pandemic. The frequent changes in travel policy and crisis outlook
have greatly affected investor sentiment and stock performance during the time,
which provide more variations for our analysis.



Using
Tweets data from Twitter API and market data from Yahoo Finance, we plan to
examine the association between community sentiment and the change in stock
price. To be specific, we will be exploring the following question in our
investigation: is there a significant correlation between Twitter
sentiment and the change in stock price? Could Twitter sentiment predict stock
market reactions (asset returns, shifts in volatility, and abnormal trading
volume), or does Twitter sentiment follow the stock performance? 



 



2. Data



2.1 Training Tweets



We use existing labeled tweets from
Kaggle[1] to train
our sentiment classifier (positive, neutral, and negative). The training set
contains 14,600 tweets on six major U.S. airlines (American, Delta, Southwest,
United, US Airways, Virgin America) in 2015.



Figure 1:
Screenshot of the training tweets dataset





2.2 Sample Tweets



For
this project, we focus on the tweets of six major U.S. airline companies during
the Covid-19 as our testing sample:



●       
NYSE: DAL, Delta Air Lines



●       
NASDAQ: UAL, United Airlines Holdings



●       
NASDAQ: AAL, American Airlines Group



●       
NYSE: LUV, Southwest Airlines



●       
NASDAQ: JBLU, JetBlue Airways



●       
NYSE: SAVE, Spirit Airlines



Using Twitter API, we extracted
170,856 Tweets mentioning these six U.S. airline companies from January 1st,
2020 to December 31st, 2020.



Figure 2:
Screenshot of the extracted tweets dataset





To
increase the performance of the NLP learning algorithms, we clean and
preprocess our tweets dataset. The preprocessing step eliminates the following:



●       
stopwords (i.e., 'the', 'a', 'and', 'how', etc.);



●       
tweets with a question mark - questions are not good indicators of
sentiment.



●       
Non-letters (including numbers, emojis, and punctuation);



●       
URL links;



●       
accounts referenced using ‘@’ symbol;



●       
words less than three characters;



●       
retweets - we decided not to count the same tweet twice;



We create word clouds for tweets
related to each airline company to visualize the most common words. It is not
surprising that “coronavirus” appears
in every airline’s word cloud. Some words reflect users’ feelings such as
“happy”, “great”, and “love”. Financial words are also prevalent in the clouds,
including “stock”, “price”, and “Nasdaq”.



Figure 2: Word cloud extracted from
the tweets of each airline company





2.3 Financial Data



We
also extracted historical stock price data of these six airlines during the
same period from Yahoo Finance. 



Figure 3:
Screenshot of the extracted financial data





 



 



3. Methodology



3.1 Model Training



First, we provide descriptive analyses of our
training sample. As shown in the breakdown graph, most tweets tend to be
negative as passengers complain about their flight experience. The
heterogeneity among airlines may explain the long-term differences in their
operations and market performance. Then, we
distinguish the types of words that are most frequently used in positive,
negative, and neutral tweets.



Figure 4:
Sentiment breakdown of training data









 



Figure 5:
Frequency distribution of top tokens





We vectorize the training data using
N-Gram. Then we use the Multinomial Naive Bayes Classifier as our model because
it is suitable for classification with discrete features. Also, since we did not have that
much training data, Naive Bayes models can be trained faster than other models.



3.2 Testing Model Accuracy



We employ a ROC-AUC curve for
performance measurement. A ROC-AUC (Receiver Operating Characteristic/Area
Under the Curve) plot allows us to visualize the classifier’s sensitivity and
specificity tradeoff. ROC (Receiver Operating Characteristic)  shows the
classification performance at all classification thresholds (positive, neutral,
and negative). The ROC computes the relationship between true positives and
false positives. AUC (Area Under the Curve)  represents the degree or
measure of separability (i.e., how well the model can distinguish the various
classes). The higher the AUC, the better the model typically is. Our ROC curves
indicate this model is better at classifying positive tweets than negative and
neutral tweets. Overall, the macro avg AUC of 0.87 indicates that the model
performs well.



Figure 6: ROC
curve for MultinominalNB model





To visualize the learning curve of
our classification model, we plot how the f-score changes over training
iterations. We can see that the training and test scores have not converged,
but the test data seems to have converged at an F1 score of 0.73. It means the
model’s accuracy would not significantly change with more data. This model also
primarily suffers from error due to variance (the CV scores for the test data
are more variable than training data), so the model may be overfitting the
data.



Figure 7: Learning
curve for MultinominalNB model





We also measure the Precision,
Recall, and F1-Score for the model, because our dataset is imbalanced (there is
no equal number of positive and negative tweets). The metrics are defined as
follows:











3.3 Textual Analysis on
Sentiment



We employ our
MultinominalNB classifier to our testing dataset (2020 sample) and obtain the
predicted sentiment. The most frequent tokens in positive, neutral, and
negative tweets are below. 



Figure 9:
Frequency distribution of top tokens









 



Figure 10:
Average sentiment of each airline company





3.4 Twitter Sentiment and
Stock Market Movement



To gauge how Twitter feels about
each airline, we take the mean of the predicted sentiment classification. Many
of these tweets contain feedback from customers’ flight experiences. We can see
that American Airlines has the worst average sentiment score by a large margin.



We plot out the change in sentiment
each day to gauge trends over time. Ideally, we take the rolling average of the
calculated sentiment scores (this would reduce the noise we see here). The
first graph uses the average sentiment score per day (between [-1, 1]), and the
second graph displays the average sentiment’s daily percent change.



Figure 11: Daily
sentiment of each airline company





 



 



Figure 12: Daily
sentiment change of each airline company





We calculate daily and cumulative
returns to see how the stocks have reacted over the same period. We use the
5-day rolling average of each to eliminate some of the market noise. Since
percentages represent both graphs, we can easily relate price performance to
the plotted sentiment graph.



Figure 13:
Rolling cumulative returns of each airline company









 



Figure 14:
Rolling daily returns of each airline company





      Finally,
we employ OLS regression to examine the association between daily Twitter
sentiment and stock returns (the same day and the next day).



 



4.
Results



      From
the sentiment analysis, our results suggest that American
Airlines consistently had the worst sentiment scores while Spirit Airlines have
the best sentiment scores overall. Meanwhile, Twitter sentiment for JetBlue
appears to be the most volatile. The five-day rolling average of cumulative
returns for the airline stock prices shows that Southwest Airlines performed
better than the others in the same period. Notably, we can see a significant
dip in stock prices that coincides with the lowest average sentiment scores
during the period from March to June of 2020. Although this might indicate that
Twitter sentiment affected the stock prices of these airlines, we cannot be
entirely sure due to the lack of data. In an ideal situation, we would have
years worth of data to generate rolling averages for both sentiment and stock
price, eliminating the noise and resulting in a more explicit association.



      The line plot and scatter plot generated by the OLS
regression model indicate a positive correlation between sentiment and rolling
cumulative returns of airline stock price. From the model summary, we can see
that the t-statistic is around 6.19, which is relatively large, and the
corresponding p-value is 0.002, which is less than 0.005. Therefore, we can be
98% confident in rejecting the null hypothesis that there is no correlation
between Twitter sentiment and airline stock prices.



Figure 15: OLS
regression plots of the same day return









 



Figure 16: OLS
regression results of the same day return





      Similarly, the rolling daily returns and sentiment
regression plot also show a positive correlation, albeit less significant than
the previous model. Summary statistics show a t-statistic of around 3.73 with a
corresponding p-value of 0.014. From these models, we can conclude that
positive and negative sentiment on Twitter has a minor but tangible effect on
the stock performance of airlines during COVID-19.







 



Figure 17: OLS
regression plots of the next day return





Figure 18: OLS
regression results of the next day return





Additionally,
we have created word clouds generated from sentiment data separated by
“positive”, “negative”, and “neutral”. Most frequently used words that are
associated with negative emotions include “price”, “time”, “miss”, “never”, and
“canceled”, which are self-explanatory and expected from typical complaints
from airline passengers. On the other hand, words associated with positive
emotions include “new”, “gain”, “thank”, “bull”, which can be interpreted as
passengers being satisfied with the airline services and being optimistic about
stock prices.



Figure 19: Word
cloud of the classified sentiment





 



5.
Conclusion



The dramatic increase in the use of social media
these past few years had a significant impact on the capital market. Firms use
social media to communicate with their investor base, and increasingly,
individual investors use social media to share information and insights about
the prospects of stocks. Using firm-specific Twitter data and
supervised-learning NLP models, we investigate the correlation between Twitter sentiment and stock market reactions and
test the predictability of Twitter sentiment for future returns. Our results
show that Twitter sentiment is highly correlated with daily stock
returns. Moreover, although most Twitter users are believed to be uninformed,
our findings show that the daily firm-level Twitter sentiment contains
information that is useful for predicting next-day stock returns.



However, it is worth noting that there are
several caveats in our analyses. Firstly, our dataset does not split financial
information and customer reviews, though they are usually correlated at some
level. In other words, we do not split “market sentiment” and “public
sentiment”. The Twitter reviews only reflect a subsample of market participants
and overestimate the sentiment of investors who use Twitter more frequently.
Secondly, our NLP models reply on the labeled training sample, which might be
systematically different from the Tweets of airline companies. The sample bias
may decrease the accuracy of the sentiment calculation. Finally, our current
study does not split official Twitter accounts (e.g., financial media) and
personal accounts. There might be some heterogeneity among different accounts,
and we are interested in what kind of users are more influential in influencing
the stock prices. We believe financial Twitter accounts may indicate previous
market movements, but consumer data may be more indicative of future price
movements. For example, consumers fall in love or out of love with a product or
service before markets can price this shift in consumer demand accordingly. All
these remain areas for future research.



Our findings have important implications for
market participants. The predictive power of Twitter sentiment for stock
returns gives traders a solid incentive to analyze social media content
carefully. Such analysis may be helpful in making security selection decisions.
Our results are also consistent with the notion that business entities may be
able to improve transparency and market efficiency by using social media.



 



References


Bartov,
Eli, Lucile Faurel, & Partha S Mohanram. (2018). Can Twitter Help Predict
Firm-Level Earnings and Stock Returns? The
Accounting Review 93(3), 25–57.



Baker,
Malcolm & Jeffrey Wurgler. Investor Sentiment and the Cross-Section of
Stock Returns. Journal of Finance,
61(4), 1645-1680.



De
Long, J. B., Shleifer, A., Summers, L. H., & Waldmann, R. J. (1990). Noise
trader risk in financial markets. Journal
of Political Economy, 98(4), 703-738.



Duz
Tan, S., & Tas, O. (2021). Social media sentiment in international stock
returns and trading activity. Journal of
Behavioral Finance, 22(2), 221-234.



Gu,
C., & Kurov, A. (2020). Informational role of social media: Evidence from
Twitter sentiment. Journal of Banking
& Finance, 121, 105969.



Loughran,
T., & McDonald, B. (2011). When is a liability not a liability? Textual
analysis, dictionaries, and 10-Ks. The
Journal of Finance, 66(1), 35-65.



Stambaugh,
Robert F., Jianfeng Yu, & Yuan Yu. (2012). The short of it: Investor
sentiment and anomalies. Journal of
Financial Economics, 104(2), 288-302.


[1] Training set: https://www.kaggle.com/benhamner/exploring-airline-twitter-sentiment-data
