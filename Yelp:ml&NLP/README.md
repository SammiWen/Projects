# Yelp data challenge
## NLP & Recommender systems
find the goole doc copy here:
https://docs.google.com/document/d/1bd5ZwaunUldMiPeMsv91F6FJ5JV2eeWJqfxsxDFwaaQ/edit?usp=sharing
### Table of Contents 
=================

[Background of the business: 2](#background-of-the-business)

[Summary of Dataset 2](#summary-of-dataset)

[BI requirements and key BI questions:
4](#bi-requirements-and-key-bi-questions)

[For business entities 4](#for-business-entities)

[For Yelp 4](#for-yelp)

[Data warehouse architecture 5](#data-warehouse-architecture)

[ETL and data quality control 5](#etl-and-data-quality-control)

[Data Warehouse Design 6](#data-warehouse-design)

[OLAP and Data mining 6](#olap-and-data-mining)

[Data preprocessing 6](#data-preprocessing)

[Natural Language Processing & Sentiment Analysis
7](#natural-language-processing-sentiment-analysis)

[Process 7](#process)

[Model Comparation 8](#model-comparation)

[Results/Findings 9](#resultsfindings)

[Clustering 13](#clustering)

[Recommender System 14](#recommender-system)

[Item-item similarity recommender 14](#item-item-similarity-recommender)

[Content-based recommender 15](#content-based-recommender)

[Popularity-based recommender 17](#popularity-based-recommender)

[Future development and growth potential
18](#future-development-and-growth-potential)

[Conclusion 18](#conclusion)

[Appendix: 19](#appendix)

[Appendix I : Dataset info 19](#appendix-i-dataset-info)

[Appendix II : Star-Schema 22](#appendix-ii-star-schema)

[Appendix III : 23](#appendix-iii)

[Appendix IV: NLP & Sentiment Analysis
23](#appendix-iv-nlp-sentiment-analysis)

[Most 10 similar reviews: 23](#most-10-similar-reviews)

[Most 10 reviews for restaurant in Las Vegas.
27](#most-10-reviews-for-restaurant-in-las-vegas.)

[Model comparation 29](#model-comparation-1)

Background of the business:
===========================

Yelp is a crowd-sourced forum. It provides service for both customer and
business. Users can give reviews for business and search for service
based on his or her location and needs. The business entity, on the
other hand, can advertise its business on Yelp's platform. After user
clicked on the restaurant he or she is interested in, Yelp will show the
restaurant location address, open hour, phone number, in addition to the
restaurant's past reviews from the other Yelp users. The reviews could
be the taste of food and recommendation for the good dishes. They could
also be a review for the service and the restaurant general features.
Yelp also allows users to make reservations via the Yelp app. The
business entity such as restaurants with the higher reviews are more
likely to attract new customers. When people travel to a new place and
want to pick a place to eat, most often they will use Yelp and see what
other people like. You could never underestimate the power of other
user's opinion on your decision process to pick a restaurant. The
restaurant with higher reviews tends to be picked up by the customer
instead of the ones with bad reviews. Yelp is using the world of mouth
algorithm, gathers data from all its user and sets up a reliable
recommendation platform for its user. However, as Yelp become more and
more influential, some business is paying people to give bad reviews for
its competitors and give good reviews for itself. Yelp has been working
to prevent this kind of fake reviews and setting up models to identify
fake reviews.

Summary of Dataset
==================

The dataset is available from the Yelp website[^1]. Yelp provides these
data to interest party and set up a competition challenge encouraging
students or professional scholars use the provided data and come up with
interesting BI questions and solutions.

The original dataset is in JSON file. We transfer the Jason file to
Pandas Dataframe and use the Dataframe.info () function to get a view of
these datasets.

The dataset consists of a total of six files including Business,
Checkin, Review, Tip, User and Photo. We will briefly explain each
dataset including its size and some important attributes including how
we are going to use the dataset below. Please refer to Appendix I for
dataset details. For additional information, please refer to Yelp
dataset webpage[^2]. Noticeably, for our project, we are going to use
total of four files including Business, Tip, Review and User.

*[Business file]{.underline}*

Business file contains 188592 rows 15 columns including the business
location, attributes and categories.

*[Checkin file]{.underline}*

Checkin data file contains the customer check in information with 157075
entries, and 2 columns.

*[Review file]{.underline}*

Review data file contains the full review text data. We can identify who
wrote the review to which business using the user\_id and business\_id.
In addition, we can also process data further using text mining for the
text data.

*[Tip File]{.underline}*

Tip data file is the tip written by user of yelp or the business. To be
noticed, there are also review text data in this file. The reviews in
this data set are tends to be shorter than the reviews in the review
data file. Usually a shorter review also gives a quicker suggestion.

*[User file ]{.underline}*

User data includes the user general info plus the metadata associated
with the user.

*[Photo file]{.underline}*

Photo data file include photo data with caption and classification.

BI requirements and key BI questions:
=====================================

With the comprehensive data provided by Yelp, we can extract useful
information by using data manipulation skills such as inner join and
outer join to link these data set together. we will use data mining and
natural language processing models to gain insights from the Yelp
dataset and generate reports for the business and user of Yelp as well
as for the Yelp platform.

For business entities
---------------------

We want to identify the key attributes associated with good reviews. In
order to do this, we use regression analysis. To obtain a better result
and construct an optimized model, we will use machine learning
techniques, add penalty (Lasso and Ridge) to the model and apply
cross-validation analysis.

In addition, we will use text mining and NLP technique like
stem/lemmatize text, bag-of-words, TF-IDF, PCA, Bayes classification
method to get insights from both the bad reviews and positive reviews
from review file and the tip file.

For Yelp
--------

We are going to construct several recommender systems based on different
algorithms. One is similarity-based collaborative filtering recommender
system for customers based on the reviews and stars the customers given
to different restaurants before. The recommender will be based on a
similarity metric using cosine similarity. We can use the recommender
system to recommend the restaurants that the customer would like.
Popularity-based recommender and content-based recommender will also be
conducted.

Data warehouse architecture 
============================

In terms of which data warehouse architecture we are going to use, we
decided to use hub-spoke architecture. Hub-spoke architecture focus on
building a scalable and maintainable infrastructure. Our goal is to
build a data warehouse for end-user to easily manipulate the data based
on their customized need. The end-user of this data warehouse will be
students and scholars like us and it is intended to be used by end-users
to come up with different interesting business Intelligence questions.
Hub-spoke architecture allows user to easily interact with different
dimensions in the data warehouse. In additional, based on a web-based
survey, more than one thirds of the business entities who responded to
the survey prefer hub-spoke architecture, and this architecture has the
highest score on information quality and system quality which are the
two perspectives that we pay attention to. In order to come up with
meaningful reports, we need to insure the accuracy of information, and
how the data warehouse system implement. Hub-spoke architecture in this
case is well qualified for our needs.

ETL and data quality control 
=============================

The quality of data provide by Yelp are extremely good in terms of
completeness, consistency and interpretability. To consolidate and
extract these large amounts of data was a challenging task for us to
complete. In order to process the data and obtain a more meaningful
result, we decided to decrease the data size by placing the filter on
the attributes. For our project, we are going to focus on restaurant
business, so we select business contains 'restaurant' in the category.
On top of that, we also decrease our data size by only selecting
restaurants in Las Vegas and Pittsburgh. To insure we have the most
updated data, we only keeping the data updated from 2016-09-01.

Data Warehouse Design
=====================

We choose Kimball's approach, also known as bottom-up approach as our
data warehouse development strategy. Our objective is to insure the
accessibility of data for end-user and make it easier for them to
directly query the data. Bottom up perfectly fits this criterion.

For dimensional modeling, we have our data warehouse star schema shown
in the Appendix II. We have the restaurant-review fact table surround by
Business, User, Tip, Review, Time dimensional tables. For the
restaurant-review fact table it has foreign keys come from all the
dimensional tables. It also has its own degenerate dimensional called
restaurant-review key. As for performance measures, it has review counts
which counts the number of reviews for each restaurant and
average-rating which calculate the average star received from user. For
additional detail information regarding to star schema please refer to
Appendix.

OLAP and Data mining
====================

Data preprocessing
------------------

In this section, we will illustrate how we do the data cleansing and
data selection for different model process. In order to process the data
in python, we read each data file originally in json file to pandas
DataFrame. As we mentioned before, the datasets we have are huge. We
have more than one million yelp users, almost two hundred thousand
business and around six million reviews. It will be nearly impossible
for us to process these amounts of data, and it is also difficult to
come up with meaning reports. To decrease our data size, we decided to
only include restaurants business. In addition, we decided to add the
location filter on the restaurants. We linked review file with business
file together and put all the restaurants in Las Vegas with user reviews
in one data set, and all the restaurants in Pittsburgh with user reviews
in another dataset. One of the reasons we choose Las Vegas and
Pittsburgh is Las Vegas is famous for touring, most of the reviews will
be made by visitors. Pittsburgh on the other hand is more like a
traditional city and the reviews will be made mainly by local residents
and local students. It will be more interesting if we compare the
reviews made to the business in these two very different cities. In
order to gain a more up-to-dated result, we also put a filter on date
and select reviewed made on the last two years. We selected the top 10
restaurants in Las Vegas and in Pittsburgh, the bar chart graphs are
included in Appendix. The restaurant in Pittsburgh that has the most
reviews is an American restaurant called Primanti Bros. it is famous for
sandwiches and has over six hundred reviews from the last years. The
restaurant in Las Vegas that has the most reviews is an American
restaurant called Hash House A Go Go. The restaurant has over two
thousand and five hundred reviews over the last two years which is more
than four times the number of reviews for the top restaurants in
Pittsburgh. The huge difference on the number of reviews for the top
restaurants is expected, since restaurants in Las Vegas have a much
large customer base than the restaurants in Pittsburgh. The bar chart
graphs for top ten restaurants in Las Vegas and Pittsburgh are located
in Appendix III

Natural Language Processing & Sentiment Analysis
------------------------------------------------

### Process

Python code and output for natural language process and sentiment
analysis are in Appendix IV.

In this part, our team used the datasets we generated after data
preprocessing. The file pittsrestfinallast2year.csv and
lasvegasfinallast2year.csv, and we received two NLP results (one for
restaurant in Pittsburgh and the other for Las Vegas) in this part. The
process of NLP is illustrate below using the pittsrestfinallast2year.csv
as an example.

Before we train the data into models, we defined the feature variable as
review text. We extracted all the text data and saved it to a separate
document. Then our team set average star as our target variable. we set
the 5 stars as perfect and 1-4 stars as imperfect, and created a column
named 'target', with Boolean type value which means the result will be
either True or False. We then split the dataset into train set and test
set in terms of 70%:30%.

In the second step, we removed the stop-words and converted the
extracted words into TF-IDF (term frequency-inverse document frequency)
vectors by sk-learn TfidfVectorizer & TfidfTransformer[^3] and then
trained different models with these vectors.

### Model Comparation

For classifying positive and negative review our team trained
Naïve-Bayes Classifier, Logistic Regression Classifier and a Random
Forest Classifier. We used cross validation to evaluate these
classifiers and use grid search [^4]to find best predictable classifier.

                                                model comparation table   
  --------------------------------------------- ------------------------- ---------------------
  model name                                    TRAIN ACCURACY SCORE      TEST ACCURACY SCORE
  logistic regression classifier                0.8355718355718356        0.7970639534883721
  cross validation for logistic regression      0.845204                  0.792878
  random forest classifier                      0.9221950888617555        0.7656395348837209
  naïve-bayes classifier                        0.8036901370234704        0.778546511627907
  Random forest classifier using graid search   0.808778                  0.758140

According to the accuracy scores wo got from these different models, we
select Logistic Regression Classifier which has the highest accuracy
score on test dataset to get the results. The ROC curve of these models
is in the Appendix.

### 

### Results/Findings

#### NLP results for restaurant in Pittsburgh

The top 50 key features/words that make the positive prediction (5
star):

{\'amazing\', \'best\',
\'delicious\',\'great\',\'incredible\',\'awesome\',\'excellent\',\'fantastic\',\'wonderful\',\'perfect\',\'everything\',\'favorite\',\'perfection\',\'recommend\',\'pittsburgh\',\'absolutely\',\'perfectly\',\'thank\',\'highly\',\'must\',\'gem\',\'phenomenal\',\'omg\',\'every\',\'everyone\',\'love\',\'outstanding\',\'definitely\',\'glad\',\'life\',\'loved\',\'knowledgeable\',\'pgh\',\'world\',\'vegan\',\'owner\',\'die\',\'fabulous\',\'bomb\',\'heaven\',\'oysters\',\'notch\',\'top\',\'divine\',\'ever\',\'taiwanese\',
\'welcoming\',\'chef\',\'stuff\',\'place\'}

We have some interesting finding from the result above. from the
words'owner','knowledgeable','stuff' we made an assumption that if the
owner and stuff in knowledgeable and know what they are doing the guest
will probability give a 5 star and a perfect review; from word
'taiwanese' ,'oyster','vegan'we draw a conclusion that the most
Taiwanese, vegan and oyster restaurants have high reviews. There is also
a word 'die' seems wrongly classified but actually it may come from the
sentence like this ' xxx is so delicious that I would die for it'.

The top 30 key features that makes the negative prediction (1-4 star):

{
\'ok\',\'however\',\'okay\',\'bland\',\'average\',\'worst\',\'horrible\',\'rude\',\'dry\',\'unfortunately\',\'mediocre\',\'terrible\',\'disappointing\',\'slow\',\'pretty\',\'would\',\'overpriced\',\'awful\',\'though\',\'nothing\',\'used\',\'reason\',\'seemed\',\'decent\',\'said\',\'bad\',\'star\',\'overall\',\'told\',\'lacking\'}

From the results above we can find that service attitude is really
important since the words 'rude', 'slow' showed up in these features,
and the word 'overpriced' told us the price is very important. The most
interesting finding is 'ok' and 'okay', that means if a customer feels
okay with the restaurant, he probability doesn't satisfied with this
restaurant and will likely to give a low score (star).

Our team also built a function to select most similar reviews, this
function is based on cosine similarity of the sentences. Given a review
(sentence), the function will return k (k=4 in this example) similar
reviews. The purpose of this function is to help business entities to
get more insight of the reviews given by customers and help them improve
their services. User of this function can select a text review randomly
and the function will give you top n (in this example n =4) similar
reviews calculated on their cosine similarity.

For example,

Our search query:

My wife and I came here on a freezing cold late Saturday afternoon. We
found street parking and rushed to get inside. It wasn\'t too busy when
we first got here. We were greeted by the hostess and sat right down at
a two-seater.

Here is one similar review we got:

Our Ramen came out about ten minutes later. Our dishes looked really
good and we were hungry. My wife liked her dish and you can read her
review on her Ramen. My Ramen was good but not great. The noodles were
really good. The broth warmed us up and was good but I felt it needed a
little more salt or something to bring out more the flavors in my Ramen.
I\'d give it a six out of ten. I like the vegetable in my Ramen but the
chicken looked a little funny to me and tasted funny too. The Ramen
filled me up and I was satisfied. Not the best Ramen and maybe a little
over priced but if your in the area and it\'s cold out this is a good
spot to try out.

The results are meaningful since these reviews are really similar in
common sense when we are taking a look at them. Both of the two review
is talking about eating ramen with their wife, and they both mentioned
that ramen is really good if it's cold outside.

Our team also generated most 10 similar reviews for all the reviews for
all the restaurant in Pittsburgh, here we present 3 of them, and the
whole 10 reviews is in the appendix.

Most 10 similar reviews:

\#0:

A great new ramen place in Pitt! The spicy miso ramen ... The yakitori
skewers were also really good!!

\#1:

I read mixed reviews of Ki Ramen, but decided I had to try it out for
myself. We went in at lunch time and placed an order to go. The staff
were extremely friendly and helpful. Our order was ready extraordinarily
quickly. I ordered the Dan Dan ramen with the butter bomb and the
vegetarian bao bun. ... so that our food did not get soggy before we got
a chance to eat it! We will definitely be coming back to Ki Ramen!

\#2:

I was extremely excited to take my family to get good ramen. Having
lived in Korea and visited many parts of Japan, I was pretty
disappointed with the quality of the ramen and ingredients used in our
meal. First, the chasu wasn\'t real chasu ... Little did we know until
the check had arrived, we were charged for the broth although it should
have been part of the ramen in the first place.

It isn\'t that I have high standards, I don\'t think many costumers
coming to Ki Ramen has any idea what they should expect.

We can find that the most similar reviews are all about ramen
restaurant, from that we can draw two conclusions, one is the ramen is
really popular in Pittsburgh maybe, the other is that when people giving
a review to ramen restaurant, they tend to use the similar words and
similar sentence.

#### NLP results for restaurant in Las Vegas

The top 50 key features/words that make the positive prediction (5
star):

{\'amazing\',\'best\',\'awesome\',\'thank\',\'delicious\',\'incredible\',\'perfect\',\'fantastic\',\'heaven\',\'excellent\',\'perfection\',\'highly\',\'great\',\'phenomenal\',\'regret\',\'love\',\'favorite\',\'die\',\'outstanding\',\'everything\',\'exceptional\',\'bomb\',\'perfectly\',\'every\',\'omg\',\'holy\',\'deserves\',\'notch\',\'glad\',\'soooo\',\'beyond\',\'absolutely\',\'reasonably\',\'impeccable\',\'fabulous\',\'thanks\',\'personble\',\'wonderful\',\'sooo\',\'loved\',\'wow\',\'superb\',\'gem\',\'definitely\',\'life\',\'blown\',\'lived\',\'five\',\'hands\',\'ever\'}

The top 30 key features that makes the negative prediction (1-4 star):

{\'worst\',\'horrible\',\'ok\',\'rude\',\'mediocre\',\'disappointing\',\'terrible\',\'okay\',\'slow\',\'bland\',\'however\',\'reason\',\'poor\',\'meh\',\'awful\',\'lacking\',\'disgusting\',\'worse\',\'decent\',\'disappointment\',\'overpriced\',\'average\',\'unfortunately\',\'lacked\',\'dry\',\'bad\',\'sucks\',\'alright\',\'nothing\',\'gross\'}

3 of 10 most similar reviews (the whole 10 reviews are in the appendix)

Most 10 similar reviews:

\#0:

This place is amazingly good and the service is just amazing! Coming
here for the second time never amazes me! Will be coming back again and
again in the future!

\#1:

Best. Prime. Rib. Ever! Period, hands down, no competition! Have been
coming to Lawry\'s 30+ years ever since I was a little kid and it has
always been an outstanding meal each and every time. There is literally
no better place for prime rib, Lawry\'s wrote the book on this! The
service is always spectacular, the atmosphere is nice, and the food (the
most important part) is always exceptional. From the spinning salad to
their amazing beef to all the wonderful sides, everything at Lawry\'s is
always spectacular. I look forward to going there whenever I am in the
area and I recommend it whole hardheartedly to everyone I know who a fan
of prime rib is! It has been around this long for a reason, and they are
the best when it comes to prime rib! Even the Las Vegas location is as
good as the original location that started long ago in Los Angeles.
Always nice to know it is an option when I\'m in Vegas!

\#2:

I have nothing negative to say about this place it\'s absolutely
fantastic. I have been to this location a few times and have never had
any problems service is great the staff is wonderful there always very
friendly and helpful the Gyro\'s are absolutely fantastic. Definitely a
place you should stop in and check out its a spot I definitely will
continue to go back to over and over again.

\#3:

One of my favorite places in town. Love the service, the staff there are
awesome, and the food is amazing.

#### Comparation of the two results

The top 50 words that can predict positive reviews are very similar, but
we can find that customers in Las Vegas use 'sooo' and 'soooo' more
frequently that customers in Pittsburgh.

The top 30 words that can predict negative reviews are similar too, they
both contains 'overprice', 'lack' and some other words.

As for the most similar reviews, the results in Las Vegas are about the
services and the delicious food while the results from Pittsburgh are
all about the ramen food and ramen restaurants.

Clustering
----------

We use the k-means cluster analysis for all the last two years reviews
texts for restaurants in Pittsburgh and create eight cluster for the
review text data. The details cluster information is shown in Appendix.
Some interesting things to noticed in the result is that in cluster
three, we have burger and fries and sandwiches which usually come
together in the menu. Same thing with cluster four, we have Thai, pad,
noodle and spicy. In cluster five, we have pizza, delivery and crust. In
Cluster seven, we have taco, salsa, chips, queso and guacamole. We also
use Principle Component Analysis and Random Forest for classifying
positive and negative reviews. However, these models have a poor
performance on the test dataset. If we refer to the accuracy score
obtained by each model, we can see the score for Principle Clustering
Analysis is 68%. For random forest model, we have accuracy score at 71
percent for test data. Random forest can achieve as high as 98 percent
accuracy score on train data set and we conclude that the model was
overfitting on the train dataset. At the end, we did a K-means cluster
analysis on the category of the restaurant business and divided them
into 8 different clusters. For example, in cluster 7 we have Japanese,
Asian, fusion, Chinese, Korean, ramen, poke which are all Asian food. In
cluster 2, we have nightlife, bars, American, cocktail, sports, beer,
pubs which can be classified as American bars. In cluster 5, we have
Italian, pizza, delis can be seen as Italian pizza place with delis. We
also give out the most representative restaurant in each cluster based
on the total number of reviews for the restaurants in each cluster. In
cluster 7 we have "noodlehead" as the restaurant which has the most
reviews.

Recommender System
------------------

Our team built several recommender systems for users and business
entities in Las Vegas and Pittsburgh, here we use Pittsburgh as an
example to explain how we build these recommender systems and the python
codes are in the appendix.

### Item-item similarity recommender 

Item-item collaborative filtering, also known as item-based, or
item-to-item, is a form of collaborative filtering for recommender
systems based on the similarity between items calculated using people\'s
ratings of those items. Item-item collaborative filtering was invented
and used by Amazon.com in 1998.[^5]

This model first computes the similarity between items using the
observations of users who have interacted with both items. Given a
similarity between item $i$ and $j$, $S\left( I,j \right)$, it scores an
item $j$ for user $u$ using a weighted average of the user's previous
observations $I_{u}$.

There are three choices of similarity metrics to use: 'jaccard',
'cosine' and 'pearson'. Jaccard similarity is used to measure the
similarity between two set of elements. In the context of
recommendation, the Jaccard similarity between two items is computed as

$$\mathrm{\text{JS}}(i,j) = \frac{|U_{i} \cap U_{j}|}{|U_{i} \cup U_{j}|}$$

Prediction for jaccard similarities are made via:

$$y_{\text{uj}} = \frac{\sum_{i \in I_{u}}^{}\mathrm{\text{SIM}}(i,j)r_{\text{ui}}}{\sum_{i \in I_{u}}^{}\mathrm{\text{SIM}}(i,j)}$$

The recommender results(sample):

  **user\_id**              **business\_id**         **score**         **rank**
  ------------------------- ------------------------ ----------------- ----------
  D5\_iQw0N9wO7kT7FrT7j6A   q2y2K9RwT954oQGgeNAu1w   0.0192307680845   1
  D5\_iQw0N9wO7kT7FrT7j6A   5-wiVRTpKwhz2wKxNS-JzA   0.0166122019291   2
  D5\_iQw0N9wO7kT7FrT7j6A   ts4ZmG1Fde5UfQDDskR5eQ   0.014653109014    3
  nyzncOg3goSAMK15IijIqA    5-wiVRTpKwhz2wKxNS-JzA   0.0588235259056   1
  nyzncOg3goSAMK15IijIqA    ldGnkfXjRNAxRP9cizgr0Q   0.0526315569878   2
  nyzncOg3goSAMK15IijIqA    T-OuUSSzWgrMCv9TUX3epg   0.0526315569878   3
  YFRp9i9sDuA1T5oMKq5cbg    5-wiVRTpKwhz2wKxNS-JzA   0.0588235259056   1
  YFRp9i9sDuA1T5oMKq5cbg    ldGnkfXjRNAxRP9cizgr0Q   0.0526315569878   2
  YFRp9i9sDuA1T5oMKq5cbg    T-OuUSSzWgrMCv9TUX3epg   0.0526315569878   3
  QqdHAP9tSwjteG7b9q7sAw    VkeVbH5zcm0MBKuKtytGKw   0.032051295042    1

The whole results table has 64560 rows x 4 columns

### Content-based recommender

Content-based filtering methods are based on a description of the item
and a profile of the user's preferences. The different between the
content-based recommender and item-item based recommender is that the
similarity between the items recommended in a content-based recommender
model is determined by the content of those items rather than learned
from user interaction data. [^6]In our content-based recommender system,
keywords used to describe the items are the categories of these business
entities.

The similarity score between two items is calculated by first computing
the similarity between the item data for each column (here is
categories), then taking a weighted average of the per-column
similarities to get the final similarity. The recommendations are
generated according to the average similarity of a candidate item to all
the items in a user's set of rated items.

The returns are dataframes with the top ranked similar items for each
item. The columns item, 'similar', 'score' and 'rank', where item
matches the item column name specified at training time. The 'rank' is
between 1 and k (here k = 10) and 'score' gives the similarity score of
that item. The value of the score depends on the method used for
computing item similarities, for example, we selected a sample item
(business entity id) : \[\'\--ujyvoQlwVoBgMYtADiLA\'\], and then we got
10 recommendations for this single item (here we only show the top 4 of
10):

  **business\_id**         **score**        **rank**
  ------------------------ ---------------- ----------
  lKom12WnYEjH5FFemK3M1Q   0.897495567799   1
  ABiwctEu-OZ8YsVc5lnLZQ   0.885692715645   2
  WE7UsbkilPeI8nw9ODnD-g   0.870426177979   3
  ehtDfDwcOBghAKAjgWlg4Q   0.844665825367   4

This recommender system can generate recommendations for all 1769
business entities by giving 10 recommendations per item, here is the
sample result:

           **business\_id**          **similar**               **score**   **rank**
  -------- ------------------------- ------------------------- ----------- ----------
  **0**    \--ujyvoQlwVoBgMYtADiLA   lKom12WnYEjH5FFemK3M1Q    0.897496    1
  **1**    \--ujyvoQlwVoBgMYtADiLA   ABiwctEu-OZ8YsVc5lnLZQ    0.885693    2
  **2**    \--ujyvoQlwVoBgMYtADiLA   WE7UsbkilPeI8nw9ODnD-g    0.870426    3
  **3**    \--ujyvoQlwVoBgMYtADiLA   ehtDfDwcOBghAKAjgWlg4Q    0.844666    4
  **4**    \--ujyvoQlwVoBgMYtADiLA   TKDL0wiztnEr\_rMkX8ZomQ   0.834016    5
  **5**    \--ujyvoQlwVoBgMYtADiLA   JzB7NITHQ7gVHGVZ1ntgIQ    0.830173    6
  **6**    \--ujyvoQlwVoBgMYtADiLA   z1nFepEOkn\_Bp5aopscf9w   0.827484    7
  **7**    \--ujyvoQlwVoBgMYtADiLA   FB33W3bwg3ADcIJOcLLz0w    0.824463    8
  **8**    \--ujyvoQlwVoBgMYtADiLA   WXd7r6Yvjxhyo1L6R3lQMA    0.823049    9
  **9**    \--ujyvoQlwVoBgMYtADiLA   HFr3uQI9h8sTTvGn3xk5Zg    0.810444    10
  **10**   -1xCh7Cocn6IwFzhELyohA    7mU3l5VjH1IxsXcxBxUblg    0.847667    1
  **11**   -1xCh7Cocn6IwFzhELyohA    qME1CvFxSrhqE6-YGcp3Rw    0.843009    2
  **12**   -1xCh7Cocn6IwFzhELyohA    0r1Ow0HYAAjU7oM\_2ePN6g   0.787646    3
  **13**   -1xCh7Cocn6IwFzhELyohA    WXd7r6Yvjxhyo1L6R3lQMA    0.773573    4

###  Popularity-based recommender

This recommender system makes recommendations using item popularity, the
popularity is computed using the item's mean target value, here is the
stars of the business entities. The model computes the mean rating for
each item and uses this to rank items for recommendations. In short,
this recommender system makes recommendations for all the popular
business entities for all users.

The sample result:

user\_id \| business\_id \| score \| \... \|

+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--+\-\-\-\-\-\--+\-\-\-\--+

\| D5\_iQw0N9wO7kT7FrT7j6A \| 56worzbzO-fnU-0WDuabQg \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| **3ybsKWA03f16v4OPC0jApg** \| 5.0 \| \...
\|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 3ed7T7HvUJUnPf6jDmys9A \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 2NLyAZne2fH5zTHSBin92A \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 1yQvJ-By1zO7HzSYhSlz1w \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 1n8bvxpBoUOAJsC5csuV3Q \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 0aT7sqTIIv5zMApt4p4VWQ \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 0OkfU0vDBprsIEd5hWuhAQ \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| 0IfrcGbFzQvn9w8bl9GKDg \| 5.0 \| \... \|

\| D5\_iQw0N9wO7kT7FrT7j6A \| -7teXSpi9nqy58WUd-8yfw \| 5.0 \| \... \|

\| nyzncOg3goSAMK15IijIqA \| 56worzbzO-fnU-0WDuabQg \| 5.0 \| \... \|

\| nyzncOg3goSAMK15IijIqA \| **3ybsKWA03f16v4OPC0jApg** \| 5.0 \| \...
\|

\| nyzncOg3goSAMK15IijIqA \| 3ed7T7HvUJUnPf6jDmys9A \| 5.0 \| \... \|

\| nyzncOg3goSAMK15IijIqA \| 2NLyAZne2fH5zTHSBin92A \| 5.0 \| \... \|

\| nyzncOg3goSAMK15IijIqA \| 1yQvJ-By1zO7HzSYhSlz1w \| 5.0 \| \... \|

\| nyzncOg3goSAMK15IijIqA \| 1n8bvxpBoUOAJsC5csuV3Q \| 5.0 \| \... \|

\| nyzncOg3goSAMK15IijIqA \| 0aT7sqTIIv5zMApt4p4VWQ \| 5.0 \| \... \|

This recommender is more suitable for new users since this recommender
makes recommendations based on the popularity of business entities. If
you check the list the model recommended to user, they are all the same.

Future development and growth potential
=======================================

In our team's project, we performed NLP analysis and conducted
recommender systems based on the restaurants business data in Las Vegas
and Pittsburgh. End-user can use the data warehouse to preform analysis
on restaurants on other cities. In additional, they can also focus on
other business besides restaurants.

For recommender systems, we only conducted item-item based,
popularity-based and content-based recommenders, in the future
development, our team can conduct Hybrid recommender systems by
combining collaborative filtering and content-based filtering models for
better performance.

Conclusion 
===========

After trying several models on classifying reviews into positive or
negative, we satisfy the logistic regression model which can achieve
nearly eighty percent of the accuracy rate. By applying the model, we
also find some top words associated with positive reviews and negative
reviews. It is very interesting to see that even the top worlds are
straightforward in indicating the attitude of users to the certain
restaurants. We can also see difference on the use of word based on
city.

For the different recommendation models we built, we have some doubt on
the performance of the models. For example, from the popularity-based
model, the top restaurant even has 5 stars reviews, it is permanently
closed right now. So, we also need take consideration of some of other
important attributes, instead of only focus on the customer rating.

Appendix:
=========

Appendix I : Dataset info
-------------------------

Business file

RangeIndex: 188593 entries, 0 to 188592

Data columns (total 15 columns):

address 188593 non-null object

attributes 162807 non-null object

business\_id 188593 non-null object

categories 188052 non-null object

city 188593 non-null object

hours 143791 non-null object

is\_open 188593 non-null int64

latitude 188587 non-null float64

longitude 188587 non-null float64

name 188593 non-null object

neighborhood 188593 non-null object

postal\_code 188593 non-null object

review\_count 188593 non-null int64

stars 188593 non-null float64

state 188593 non-null object

**Checkin file**

RangeIndex: 157075 entries, 0 to 157074

Data columns (total 2 columns):

business\_id 157075 non-null object

time 157075 non-null object

Review file

RangeIndex: 5996996 entries, 0 to 5996995

Data columns (total 9 columns):

business\_id object

cool int64

date object

funny int64

review\_id object

stars int64

text object

useful int64

user\_id object

Tip file

RangeIndex: 1185348 entries, 0 to 1185347

Data columns (total 5 columns):

business\_id 1185348 non-null object

date 1185348 non-null object

likes 1185348 non-null int64

text 1185348 non-null object

user\_id 1185348 non-null object

User file

RangeIndex: 1518169 entries, 0 to 1518168

Data columns (total 22 columns):

average\_stars 1518169 non-null float64

compliment\_cool 1518169 non-null int64

compliment\_cute 1518169 non-null int64

compliment\_funny 1518169 non-null int64

compliment\_hot 1518169 non-null int64

compliment\_list 1518169 non-null int64

compliment\_more 1518169 non-null int64

compliment\_note 1518169 non-null int64

compliment\_photos 1518169 non-null int64

compliment\_plain 1518169 non-null int64

compliment\_profile 1518169 non-null int64

compliment\_writer 1518169 non-null int64

cool 1518169 non-null int64

elite 1518169 non-null object

fans 1518169 non-null int64

friends 1518169 non-null object

funny 1518169 non-null int64

name 1518169 non-null object

review\_count 1518169 non-null int64

useful 1518169 non-null int64

user\_id 1518169 non-null object

yelping\_since 1518169 non-null object

Appendix II : Star-Schema
-------------------------

![](media/image1.png){width="6.5in" height="6.000694444444444in"}

Appendix III : 
---------------

![](media/image2.png){width="3.9833333333333334in"
height="3.1534722222222222in"}

![](media/image3.png){width="3.6666666666666665in"
height="2.873005249343832in"}

Appendix IV: NLP & Sentiment Analysis
-------------------------------------

### Most 10 similar reviews:

\#0:

A great new ramen place in Pitt! The spicy miso ramen I got was
delicious and had the depth of flavor in the broth that a ramen should
have. The yakitori skewers were also really good!!

\#1:

I read mixed reviews of Ki Ramen, but decided I had to try it out for
myself. We went in at lunch time and placed an order to go. The staff
were extremely friendly and helpful. Our order was ready extraordinarily
quickly. I ordered the Dan Dan ramen with the butter bomb and the
vegetarian bao bun. My partner had the inferno ramen and the meat bao
bun. He ordered a butter bomb in his ramen too but we were pretty sure
they forgot to give it to him. He also felt that the inferno ramen could
be slightly spicier as the name leads you to believe. Overall though we
really really liked the food. The house-made noodles were wonderful. We
really appreciated the thoughtful packaging of the to go order (broth
separate from noodles and toppings) so that our food did not get soggy
before we got a chance to eat it! We will definitely be coming back to
Ki Ramen!

\#2:

I was extremely excited to take my family to get good ramen. Having
lived in Korea and visited many parts of Japan, I was pretty
disappointed with the quality of the ramen and ingredients used in our
meal. First, the chasu wasn\'t real chasu. It was just steamed or boiled
pork. Second, the noodles which should be the most important part of the
ramen was sub quality and something they would never serve in Japan, not
even at the \$2 ramen stands. Lastly, my wife\'s ramen lacked enough
broth to cover the noodles, so we asked for more. Little did we know
until the check had arrived, we were charged for the broth although it
should have been part of the ramen in the first place.

It isn\'t that I have high standards, I don\'t think many costumers
coming to Ki Ramen has any idea what they should expect.

\#3:

I am newly crowning Fujiya as the KING of RAMEN in Pittsburgh. I\'ve
been to every other ramen place in Pittsburgh, and the others just
don\'t compare. Having lived in DC, NYC, and eaten ramen in Philly and
Tokyo, as well as being Japanese-American, I know a thing or two when it
comes to ramen. The ramen here is nearly up there among the best, which
is saying a lot. The broth is so rich and the noodles are good. I tried
the spicy miso ramen. Some criticism tho: the Chiar shu is TOO SMALL and
TOO FEW. It\'s a tiny single slice. Also, couldn\'t hurt to have a bit
more noodle for the price point. Otherwise, this place is definitely
going to be my new go-to ramen joint.

\#4:

Ramen can be the best to warm your insides on a cold, bitter day.
There\'s certainly a lot of those days in Pittsburgh.

I was pretty excited to find out about the Ramen Bar, and was
recommended to come here by a few others. While the portions of noodles
and broth, there was a lack of vegetables and meats. My Ramen Ramen dish
had only a few bean sprouts a single slice of pork. It was great for
flavoring the broth, but the meat itself was terribly overcooked.

My partner ordered the seafood ramen, which for \$4 more than my dish,
and included only two shrimp and and two mussels.

I also wish a spoon had been offered. I struggled to eat my ramen with
chopsticks. While we were getting ready to leave, I saw everyone at the
table next to ours ask for spoons and forks. I felt kinda silly not
asking at that point, but a soupy dish is not easy to eat using
chopsticks.

I do applaud the quick service and the hot meal, but I\'m curious if I
could find a better local ramen place.

\#5:

Funny, I have not actually gotten the frozen yogurt here, but I\'ve been
here multiple times for their ramen. This review is for their ramen, and
not their desserts.

That said - this is probably the best ramen option in Pittsburgh right
now. I\'d rank the ramen at i Tea Cafe a close \#2 (if they remember to
salt the broth), Grit and Grace \#3, and Tan Izakaya and Ramen Bar a
distant \#4 or \#5, depending on whether you consider not actually
having ramen noodles in your ramen to be a greater sin than excessively
MSG\'ed broth. All things considered it\'s a rather low bar to be the
best ramen in Pittsburgh, but this yogurt place does a decent enough job
of it and the prices are reasonable enough that I keep coming back.

The noodles are fresh and come out with the right amount of springiness.
The toppings available to build your bowl are plentiful. The pork belly
is flavorful and tender. The broth is well salted but their tonkotsu
broth is lacking in richness.

Service is relatively quick and informal, so it makes for a great lunch
place.

\#6:

After literally several years in development, this place is finally
open! And not even as what it was originally advertised to be, which was
Lanzhou noodles. This restaurant is now a solid Japanese ramen
restaurant, which miscellaneous offerings of donburi, yakisoba, and
apps. Somewhat interesting that it finally opens now, when ramen places
are seemingly popping up all over Pittsburgh. From the price point and
feel of the restaurant though, it seems more accurate to group it with
the older places like Ramen Bar and Love Ramen (formerly Love Yogurt).
The ramen bowls are priced at \$10/11 and the ambience is quite casual,
fitting in with most of the other Oakland restaurants nearby. For
comparison, others like Ki Ramen or Yuzu Kitchen are more formal
settings with more extensive menus and ramen bowls costing up to 50%
more.

The ramen selections here encompass the usual shio, shoyu, and miso
varieties, where each item has different combinations of ingredients.
They also have curry ramens as well as tan tan, kimchi, and seafood
ones. When we came in it was late at night and no other customers were
here (perhaps also because they just recently opened), so our ramens
came out soon after ordering. It looked quite authentic\--it contained
all the ingredients promised on the menu, and the size was large enough
to be quite filling. The broth was immediately impressive\--very savory
and decently thick, giving you a warm feeling in your whole body. The
noodles were cooked just right and not too firm nor too soft. The chashu
was extremely tender, with maybe just a bit more fat than I would\'ve
liked, but it was not a dealbreaker in any way. The runny egg was also
cooked to perfection with the right consistency. In all these factors,
this ramen solidly beats out Love Ramen and Ramen Bar, and is at the
same time cheaper than some of the other places that I mentioned. The
other ingredients in my bowl were the standard accompaniments and made
the bowl delightful to finish.

This is a great addition to Oakland, and I definitely look forward to
coming back and trying more of their ramens and maybe non-noodle dishes
as well.

\#7:

Ki Ramen is awesome. I can\'t say enough about their ramen bowels.

And my almost 3 year old is obsessed with \"stop to eat the big soup
bowl of noodles\" place. Or just saying hello and waving to their diners
at the open bar window down stairs who are slurping and/or cheering for
them for their good taste in food. Or waving through the glass on Butler
Street at the diners inside. My three year old is a character. He really
loves soup. And people who choose to eat soup. We love Ki Ramen.

Personally, I love the ramen bowl customized w a butter bomb, some extra
chicken, and my egg held. Ki Ramen like all good Ramen places has you
season your own bowl. Seasoning is on the table. It\'s the diners choice
to decide how bland or spicy they prefer their experience. I love a good
Ramen place that knows how to follow tradition.

I am also OBSESSED with their buns. My only \"complaint\" is that their
isn\'t multiple flavors of bins daily or that their best buns aren\'t on
the menu each day. They\'re awesome. If I had a better idea what was
expected, I\'d plan around the bun to choose when to eat at Ki Ramen. As
someone who eats very little meat, and mostly just chicken a couple
times a month not knowing the Bun schedule makes choosing Ki Ramen buns
for a meal difficult.

BUT- I only mentioned it because those little buns filled with goodies
are so delicious and I just crave them all the time. I can\'t get
enough!

\#8:

Hmmm\.... maybe I had an off night but was incredibly disappointed.

Myself and 2 friends sat at the bar on a Thursday night. We ordered
drinks first, they were fine.

Ordered the deviled eggs and the pancake. Both were good, interesting
flavors, close to 4 stars.

I ordered the udon and my both ordered the tonkatsu ramen, add chili.
The udon was pretty good, 3 stars. Knife cuts on the veg were very small
so difficult to eat with a chopstick with the thick/heavier udon noodle.
One of my friends got the unagi hand roll and thought that was the best
hung we ate (\"bomb.com\").

The ramen deserves its own paragraph. To levelset, we just got back from
Japan and that is my standard. Regardless, I am beyond confused why some
think this ramen is the best ramen in Pittsburgh. The ramen broth was
inedible. Basically drinking ocean water. I guess some are considering
that flavor? The meat on the bone is difficult to incorporate into the
ramen with chopsticks. It is nothing like the tonkatsu ramen we had in
Tokyo and I will never be back for it. Negative stars.

Overall giving 3 stars because appetizers were ok and our bartender did
end up taking the ramen off of the menu.

\#9:

Despite all of the attention lavished on the Pittsburgh food scene
recently, we still can\'t get a decent bowl of ramen in this town. In
the case of Tan Izakaya, the situation is worse because they don\'t even
seem to know what proper ramen is.

If you want ramen, don\'t eat here. We were served lukewarm spaghetti in
a tasteless broth and were treated like idiots when we asked why they
didn\'t use real ramen noodles. Soba and Udon are not used in any
version of ramen. Period. Full stop. Their insistence that they\'re
serving authentic ramen is as confusing as it is sad.

In addition to the fact that it wasn\'t actually what anyone would
consider ramen, it wasn\'t even a very good version of noodle soup.
Bland broth with no depth of flavor served over slimy pasta. The pork
seemed ok, but there was so little of it that if it had been bad, I\'m
not sure I would have been able to tell.

I would\--without hesitation\--rather eat top ramen than what we were
served. It was gross and hurt my feelings.

### Most 10 reviews for restaurant in Las Vegas.

Most 10 similar reviews:

\#0:

This place is amazingly good and the service is just amazing! Coming
here for the second time never amazes me! Will be coming back again and
again in the future!

\#1:

Best. Prime. Rib. Ever! Period, hands down, no competition! Have been
coming to Lawry\'s 30+ years ever since I was a little kid and it has
always been an outstanding meal each and every time. There is literally
no better place for prime rib, Lawry\'s wrote the book on this! The
service is always spectacular, the atmosphere is nice, and the food (the
most important part) is always exceptional. From the spinning salad to
their amazing beef to all the wonderful sides, everything at Lawry\'s is
always spectacular. I look forward to going there whenever I am in the
area and I recommend it whole hardheartedly to everyone I know who is a
fan of prime rib! It has been around this long for a reason, and they
are the best when it comes to prime rib! Even the Las Vegas location is
as good as the original location that started long ago in Los Angeles.
Always nice to know it is an option when I\'m in Vegas!

\#2:

I have nothing negative to say about this place it\'s absolutely
fantastic. I have been to this location a few times and have never had
any problems service is great the staff is wonderful there always very
friendly and helpful the Gyro\'s are absolutely fantastic. Definitely a
place you should stop in and check out its a spot I definitely will
continue to go back to over and over again.

\#3:

One of my favorite places in town. Love the service, the staff there are
awesome, and the food is amazing.

\#4:

Lobster tail and Prime rib for 50 bucks! The food was great. I\'ve had
better prime rib but it was still really good. I will absolutely return.
You definitely get your money\'s worth here.

\#5:

You look all over for a good prime rib in Vegas everyone\'s got it put
this prime rib is the most succulent I\'ve ever had it is certain the
plate that is filled with ah juice it is the most fabulous Prime ribs
I\'ve ever had if you want to make the trip up the Southpoint which is
not that far from downtown hit the Prime Cut at Southpoint you love it
plus is not a bad Hotel they have a huge bowling alley movie theater and
they\'re supposed to die for enjoy your vacation

\#6:

Been here 3x now. Love, love, love! Entire staff with every
visit\--wonderful, pleasant and attentive. Owner goes through the entire
restaurant and personally check on every patron to make sure everything
is good and make you feel like family. She knows what she\'s doing. My
first Filipino Gastropub-APPROVE! Wishing your establishment great
continued success!

\#7:

Amazing food.

Great staff.

Prime times are busy so be prepared and plan accordingly.

Big Cheese ( add bacon ) is stellar.

\#8:

This is such a great restaurant I can\'t really put it all in a review.
I\'ve been here three times and every time I\'m just blown away by all
of it. You cannot go wrong with Prime. The seafood tower appetizer is
seriously incredible I get it every time I come here. Everything on the
menu is absolutely amazing. Waiters are awesome. Highly recommend!

\#9:

This restaurant is now my absolute favorite prime rib place. My husband
and I are visiting from Hawai\'i and celebrated our anniversary by
having dinner here. Every staff member we encountered was wonderful.
They were very professional and attentive to out needs. The food was
amazing. From the appetizers , to our 14oz prime rib was heavenly, and
perfectly prepared. We had the sizzling apple caramel pie with vanilla
bean ice cream for Dessert and it was so delish!

### Model comparation

![](media/image4.png){width="6.5in" height="5.170958005249344in"}

![](media/image5.png){width="6.5in"
height="5.388194444444444in"}![](media/image6.png){width="6.5in"
height="4.633333333333334in"}![](media/image7.png){width="6.5in"
height="3.529166666666667in"}

[^1]:  <https://www.yelp.com/dataset>

[^2]:  https://www.yelp.com/dataset/documentation/main

[^3]: https://scikitlearn.org/stable/modules/generated/sklearn.feature\_extraction.text.TfidfTransformer.html\#sklearn.feature\_extraction.text.TfidfTransformer

[^4]: Exhaustive searching through a manually specified subset of the
    hyperparameter space of a learning algorithm.

[^5]: https://en.wikipedia.org/wiki/Item-item\_collaborative\_filtering

[^6]: https://turi.com/products/create/docs/generated/graphlab.recommender.item\_content\_recommender.create.html\#graphlab.recommender.item\_content\_recommender.create
