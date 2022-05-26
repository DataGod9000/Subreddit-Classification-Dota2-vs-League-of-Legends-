# Project 2

## Background
<p style="color:Navy;">TWITCH</p>
Twitch is a video live streaming service based in the United States that centers around video game live streaming, including esports tournament broadcasts,
 as well as music broadcasts, creative content, and "in real life" feeds. Twitch Interactive, an Amazon.com, Inc. subsidiary, runs it. It debuted in June 2011 as a spin-off of Justin.tv,
 a general-interest streaming network. The site's content can be accessed in real time or on demand.

<p style="color:Navy;">DOTA2</p>
Valve created and distributed Dota 2, a multiplayer online battle arena (MOBA) computer game. Defense of the Ancients (DotA),
 a community-created mod for Blizzard Entertainment's Warcraft III: Reign of Chaos, is the game's sequel. Dota 2 is a game in which two teams of five players compete against each other,
 each defending and occupying their own base on the map. Each of the ten players takes control of a powerful figure known as a "hero," who all have different powers and play styles. In player vs player combat,
 players gather experience points and gear for their characters in order to beat the enemy team's heroes. A team wins if they are the first to destroy the opposing team's base.

<p style="color:Navy;">LEAGUE OF LEGENDS</p>
On another hand, League of Legends (LoL), sometimes known as League, is similarly a multiplayer online battle arena video game created and distributed by Riot Games in 2009.
 Riot's founders were inspired by Defense of the Ancients, a custom map for Warcraft III, to create a standalone game in the same genre. League has been free-to-play since its launch in October 2009, 
with character customization available for purchase.

## Problem Statement
We are a hypothetical team of Data Scientist working for the American video live streaming company, Twitch. Twitch currently has a forum for twitch viewers to come together and discuss their 
favourite topics under thread titles like Video Games, Youtubers, or Music. In an effort to improve and expand its forum sectio, Twitch is looking to create sub threads for specific respective game titles like Dota2, 
Valorant, or League of Legends. Our team are, therefore, engaged to categorise each existing comments in the VideoGames thread and place them into their respective sub-threads of Dota2 and LoL (League of Legends).
To achieve this, 4000 posts and comments are pulled from each of the Leagueoflegends and dota2 subreddits for analysis, and to work as basis for our machine learning model building. 
The machine learning models will be taught key differentiator of the two video games, and hence be tasked to categorise comments of the respective video games on the Twitch Forum.

## Data Used
* ['df_lol.csv'](./data/df_lol.csv): Self text and posts of leagueoflegends subreddit pulled from reddit via pushAPI.
* ['df_dota.csv'](./data/df_dota.csv): Self text and posts of dota2 subreddit pulled from reddit via pushAPI.


##  DataDictionary
| Feature                | type   | Description                                                                                                    |
|------------------------|--------|----------------------------------------------------------------------------------------------------------------|
|df_dota_lol             | object | Combined Dataframe containing cleaned, lemmetized, tokenized and stemmed data from the two subreddits combined |   
|df_dota                 | object | dataframe including Self text and posts of leagueoflegends subreddit pulled from reddit via pushAPI.           |
|df_lol                  | object | dataframe including Self text and posts of dota2 subreddit pulled from reddit via pushAPI                      |



##  EDA FINDINGS
1) the top 5 most frequent words in Dota2 subreddit is Stockholm major, gaimin gladiator, esl stockholm, and tundra esports.
2) the top 5 most frequent words in leagueoflegends subreddit is Spell Immune, challenger, riot, champion and league.
3) this goes to shows that people on the Dota2 subreddit is discuss more about Dota2 esports tournament, which may suggest that Dota2 has a bigger esports tournament presence then LoL

##  Methology (missing values)
Fill null values as blank in order not to remove valuable data in other columns of the row

## Machine Learning Models

Logistic Regression (TFIDF) train/test = 94.6% / 89.9% 
Logistic Regression (Count Vec) train/test = 91.6% / 87%


Multinomial Naive Bayes (TFIDF) train/test = 96.3% / 90.8%
Multinomial Naive Bayes (Count Vec) train/test = 94% / 90.2% 


Random Forest (TFIDF) train/test = 99% / 89.9%
Random Forest (Count Vec) train/test = 99.4% / 89.5%


## Machine Learning Models Summary

0	TF-IDFVec + Multinomial Naive Bayes	0.970813	0.995011	0.970556	0.963163	0.908362	0.947317	0.852982
1	CountVec + Multinomial Naive Bayes	0.967973	0.986141	0.969839	0.943271	0.902062	0.903415	0.900139
2	TF-IDF Vec + random forest	 	0.949812        0.999075	0.958665	0.993861	0.899198	0.960000	0.812760
3	TF-IDFVec + Logistic Regression  	0.967175	0.994350	0.969788	0.946709	0.895762	0.972683	0.786408
4	CountVec + Random Forests	        0.947185	0.998788	0.954295	0.994352	0.895189	0.932683	0.841886
5	CountVec + Logistic Regression	        0.956559	0.992004	0.965459	0.916749	0.870561	0.976585	0.719834

TF-IDFVec + Multinomial Naive Bayes is choosen for model evaluation

## Conclusion 
From the results above we can observe that Multinomial Naive Bayes in TF-IDF vector data gives the highest accuracy, and will hence be the model choosen for model testing and evaluation. With the model accuracy score of 90.%, 
it is also safe to assume that the model will be adequent at classifying posts and comments on Twitch's now single thread forum for VideoGames. The model will however be expect to be a little over-fitted when doing the actual 
test especially when we are doing classification outside of reddit, with data pulled from reddit. TF-IDF data in general is also found to give better results then data that are
simply count vectorized. One reason for this may be because count vectorization has a tendency to transform words in a manner that completely change the meaning of the word.
For example, the word Challenger, a strong predictor for the models, which refers to the highest tier of players in league of legends was transfromed into the word challeng
via count vectorization. This apparantly made the word a weaker predictor and may explain the least accurate results it generates when working with the various models.
The following section on limitations and future works will detail how we can improve this model to further improve model accuracy 
and reduce model over-fitting. 

## limitations (future work)

1. As seen from the Train and test results from each models that the model is slightly overfitted. This is a result of insufficient removal of extra stopwords, and words that are not meaningful in classifying the respective video games comments. For e.g. the word Gold is one of the predictors of the model but it appears in both subreddits as both the in-game currency in Dota2 and LoL is refered to as Gold.
2. The analysis is only based on 3 models, other models like KNN might give better results.
3. Sub-threads from sources other than reddit can be used for a more holistic analysis for model building

