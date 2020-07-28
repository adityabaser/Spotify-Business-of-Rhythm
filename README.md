# Spotify-Business-of-Rhythm

## Table of contents

- 1 - Project at a Glance Table of Contents
   - 1.1- What is the project all about?
   - 1.2- Why this project?
   - 1.3- Data Set
   - 1.4- Target Problems
- 2 - Probability of skipping a song
- 3 - Analysis of hour of the day to generate recommendations
- 4 - Analyzing the features of current song being played to predict the next song to be played:
- 5 - Predicting the popularity of a new song
- 6 - Determining the trend of features by plotting it against each year
- 7 - Conclusion
   - 7.1- How can companies use these results?
   - 7.2- How do we scale this?
   - 7.3- Video Link


## 1 - Project at a Glance

### 1.1- What is the project all about?

Provide business recommendations to Spotify to help them make better marketing decisions and playlists by analyzing available data, which includes:-  

Analysis of the hour of the day to generate recommendations on the following problem statements:  
a. Computing the number of times each context type is played during the time of observation.  
b. Finding the optimum hour of the day by analysing the number of active users to promote under-performing context types.  
c. Learning how various context types are permorming during each hour of the day and drawing conclusions out of it.  

Predicting whether a song would be skipped or not by taking into consideration correspondingly other significant factors.  

Analysing the features of the current song being played to predict the next song to be played.  

Finding the popularity of a song by analyzing several acoustic factors that govern the song.  

Inferencing the trend of various track features with years

### 1.2- Why this project?

Spotify, a music streaming service, with over 190 million active users and a library of over 40 million
tracks creates multiple playlists that are directed towards users by taking into consideration their
preferences. Analyzing the probability of skipping a song can provide insight into how efficient the
Spotify-generated playlists are. If a user skips songs in a user-specific playlist, it can tell the company
that they have not entirely understood the user and require further analysis. The reason why this
problem is interesting is because it focuses on how a particular user interacts with the provided
streaming service and further helps in developing business recommendations from it.

### 1.3- Data Set

The links to the two major datasets used in this analysis are giving below:-

```
1) User Interaction -
https://drive.google.com/open?id=1mA6dXXjkp8M5euIoBQKNx4QmO9d20eeG
The above dataset gives one insights about the interaction of the user with respect to every
track played. The dataset includes information about at what point was the song skipped and
also about the context type of the song.
2) Track features –
https://drive.google.com/open?id=10ZmHn8yxvzs-sif4xpN1pQkuL6kvRVOC
The above dataset gives one insights about the various features of the track associated with the
song, including various acoustic features such as tempo, bounciness etc.
```
### 1.4- Target Problems

Provide business recommendations to a music streaming company by analyzing available data, which
includes:-

1. Predicting the skip probability of a song.
2. Predicting which hour of the day the users have the highest favorability towards company-
    generated playlist.
3. Predicting which song will be played next
4. Ascertaining the popularity of a song by analyzing several acoustic factors.
5. Analyzing trends of features with years


## 2 - Probability of skipping a song

**Aim:** To find the probability of a song being skipped based on the previous listening session history. The
following 3 steps are involved in this:

Data Pre-processing: We cleaned the original data set to remove redundancies created due to the back-
button and endplay which led to the data repeated twice. Next, we incorporated categorical variables
for different features to further incorporate a random forest. Then, we bi-furcated the data set into
Training and Testing set with a split of 70:30. There were a total of 60+ features, however if we were to
use them all, it would’ve lead to over-fitting. Hence, we had to focus on the most important features
that affected the probability of a song getting skipped the most.

Random Forest: We deployed a Random Forest Classifier to identify the most important features. In
doing so, we assigned weights to each feature according to their importance. We determined the most
important features by assigning a threshold value above which we would select the features. This gave
us 7 most important features which we used in the next steps. They are as follows:

```
hour_of_day
duration
hist_user_behavior_reason_start_fwdbtn
hist_user_behavior_reason_start_trackdone
hist_user_behavior_reason_end_fwdbtn
hist_user_behavior_reason_end_trackdone

```
Logistic Regression: Once we had the most important features, we used the Logit Model to perform
logistic regression using covariates, to find the outcome of the song being skipped or not. We were able
to predict the probability of the song being skipped with an accuracy of 90%.

**Inferences based on the coefficients of regression:**

```
1. We infer from the above model that out of the selected features, features such as hour of day, popularity and liveness are statistically insignificant features.

2. We can also infer that provided the other factors remain the same, a song which has started by pressing the forward button would have a higher probability of getting skipped. This might be due to the recommendation system of the application that puts songs of similar features together. 

3. Provided the other factors remain the same, a song which has started by the track getting over would have a lower probability of getting skipped. This might be due to the recommendation system of the application that puts songs of similar features together.

4. The model also rightly predicts the fact that a song ended by pressing the forward button has a high positive coefficient provided other factors remain the same. 

5. Provided the other factors remain the same, more the duration of the song lesser is the probability of the song getting skipped.  
```

**Outcomes:**

```
● We can determine the skip probability for a new song with similar features using this model.
● This analysis can help in computing the songs that are skipped the most number of times.
● Give better recommendations to the users in the form of playlists with songs that are less likely
to be skipped.
```
## 3 - Analysis of hour of the day to generate recommendations

Aim: To provide business insights and recommendations by analyzing the trends w.r.t the hour of the
day

Motivation: Spotify has various types of playlists (context type). We want to analyze the popularity of
these context types (especially the company-generated playlists) and to even analyze their performance
with respect to the hour of the day to determine when users are most active and when to promote
company-generated playlists.

Process: We carry out three types of analysis. They are performed by data visualization using python.

```
a. Computing the number of times each context type is played during the time of observation(fig a)
b. Finding the optimum hour of the day by analyzing the number of active users to promote under-
performing context types (fig b)
```
```
Figure a
![alt text](https://github.com/adityabaser/Spotify-Business-of-Rhythm/blob/master/Results/Figure%20a%20-%20Number%20of%20times%20each%20category%20was%20played.PNG)

Figure b
![alt text](https://github.com/adityabaser/Spotify-Business-of-Rhythm/blob/master/Results/Figure%20b%20-%20Number%20of%20Active%20users%20versus%20the%20hour%20of%20the%20day.PNG)

Figure c
![alt text](https://github.com/adityabaser/Spotify-Business-of-Rhythm/blob/master/Results/Figure%20c%20-%20Stacked%20Bar%20Graph%20of%20Categories%20played%20per%20hour.PNG)
c. Learning how various context types are performing during each hour of the day and drawing
conclusions.
```

## 4 - Analyzing the features of current song being played to predict the next song to be played:

Aim: To predict the next song that should be recommended to any user depending on the current song
that he is listening to.

Process: We use K-nearest neighbors to find the most similar songs to the current song based on the
acoustic vectors of the song and other factors like danceability, liveness, tempo etc. We first standardize
the features to bring them to a common scale and then feed these features to the KNN algorithm. We
can input the first song the customer searches and starts listening to in this KNN algorithm. And the next
songs can be played in the order in which KNN recommends if the customer himself does not switch
songs. We can continue playing the songs in the order in which the algorithm gives as these songs are
most similar to the song that the user himself searches and we do not again run KNN for the
recommended songs. We only run this algorithm in the case when a user just searches a song and that
track is completed. Then, instead of repeating the same song (unless it is on repeat), we can play the
following tracks with the help of this algorithm.

To give an example, if the first song the user plays has track id 73, the following songs can be played in

order (Here we have printed out 9 songs including the 1st one that the user himself searches).

We cannot develop a user-specific recommendation in this case because the dataset does not provide
us with any user-specific data.

## 5 - Predicting the popularity of a new song

Aim: To predict the popularity of a song on the basis of various features of the song

Motivation: One of the major complains that Independent artists have is of the trade-off between
joining music streaming platforms. On one hand, if they don’t join the platform (like Spotify), they will
not get enough traction and will find it difficult to grow. On the other hand, because these artists are not
well established currently, they are not provided with lucrative deals on signing with such platforms (like
other well-known artists might get). The revenue they make is meager. Additionally, being a part of such
platforms will cannibalize their records and album sales too (further dropping their revenue)


The only way such artists can make money is by generating a lot of exposures (number of times their
songs are played).

Thus, we want to create a model that can provide the artist with a rough estimate of popularity, to
understand if their song will receive enough traction (and thus, whether or not they should sign with the
platform).

Process: Since we want to predict the popularity of a song, we only want to focus on features that relate
to the song and ignore features that are artist-related.

Data Cleaning: Manipulation of columns, creating dummy variables, scaling the dependent variable to
normalize the distribution, standardization of features.

Model Selection: Using a Random Forest Regressor model to predict the most important features. We
ascertain the ideal number of features=8, and then run the RF model to help us select the top 8
features.

Cross-Validation: Prediction of RF model is tested against the test set. The following output is received:

Cross-validation result Top 8 Features

One must keep in mind that popularity is a very subjective notion, and is difficult to estimate. Feature
selection is performed only so that the artist can get a sense of which features to focus on while making
their song. (Depending on the genre, target audience, etc, they can decide the value of their features)

## 6 - Determining the trend of features by plotting it against each year

Aim: To find the trends of various acoustic vectors and track features over the years to be able to
recommend the ideal values of such features which could increase the likelihood of popularity.

Process: To find the trend of different track features with years, we visualized the popular songs over-
time from 1950 to 2019. We infer that most track features of popular songs converge or lie within a very
specific range. Hence, if a new thriving artist wants his music to be popular in this age, the artist should
aim to have the features of his songs to be in these ranges. Let us give some examples.

1. First, we start with duration. Through the below graph we see that, early on during 1950s-1960s,
    duration was not an important feature that affected popularity but as the years progressed, we
    see that now the most popular songs have a duration of about 220 seconds.


2. Second, let’s look at organism. We see that popular songs since 1990 have the feature organism
    around 0.3 and 0.4. So, if a new song wants to enter the market, its organism value should be in
    this range to have a higher probability of being popular.

Similarly, we can analyze other features of popular songs and recommendations can be given to new
thriving artists that the feature values of their songs should be in these ranges to have a higher
probability of getting their songs more popular. Also, along with the music company’s streaming service;
it can roll out such a product which can evaluate the probability of a new song being popular in the
current market and on its platform by using these feature values.


## 7 - Conclusion

### 7.1- How can companies use these results?

As discussed above, there are multiple applications and uses of these results.

```
● To help companies build better recommendation systems by helping them predict whether a
song will be skipped and which song should be played next.
● To help the marketing team with the analysis of different playlists at different hour of the day
● To help artists focus on important features to help them come up with a song that generate
enough traction and popularity
```
### 7.2- How do we scale this?

We can improve the algorithm to handle larger data-sets and to increase the efficacy in terms of time
and space. Currently, we have analyzed Spotify data-set. The next step is to tailor the algorithm to fit
different company data-sets.

### 7.3- Video Link

The link below is for video submission –

https://drive.google.com/open?id=164MjU96ngjR-7HP1YjdZs42VVrCtWJ8z
