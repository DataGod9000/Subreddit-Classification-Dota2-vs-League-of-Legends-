![](https://github.com/Aspiring-DataGod9000/Subreddit-Classification-Dota2-vs-League-of-Legends-/blob/main/read_me_images/dota_vs_lol.png)

# Subreddit classification (Dota2 vs League of Legends)

We are a hypothetical team of Data Scientists working for the American video live streaming company, Twitch. 

Twitch is currently hosting a forum for twitch viewers to come together and discuss their 
favourite topics in threads like Video Games, Youtubers, or Music. In an effort to further improve and expand its current forum, Twitch is looking to create sub-threads for existing threads, i.e. dividing the existing Video Game thread into Dota2, Valorant, and League of Legends subthreads. By doing so, Twitch hopes to help users better navigate the forum, and to help better foster community spirit within the platform.

 Our team is, therefore, tasked to analyse existing comments in Twitch's Video Games thread and categorise them into their respective sub-threads, Dota2 or League of Legends.


## Data Dictionary

| Feature                | type   | Description                                                                                                    |
|------------------------|--------|----------------------------------------------------------------------------------------------------------------|
|df_dota_lol             | object | Combined Dataframe containing cleaned, lemmetized, tokenized and stemmed data from the two subreddits combined |   
|df_dota                 | object | dataframe including Self text and posts of leagueoflegends subreddit pulled from reddit via pushAPI.           |
|df_lol                  | object | dataframe including Self text and posts of dota2 subreddit pulled from reddit via pushAPI                      |

A total of 8000 posts and comments were pulled from both the Leagueoflegends and dota2 subreddits using pushAPI. Around 5800 comments and post, to be used as input for our model, remains after the data cleaning process.
## EDA 
1) the top 5 most frequent words in Dota2 subreddit is Stockholm major, gaimin gladiator, esl stockholm, and tundra esports.
2) the top 5 most frequent words in leagueoflegends subreddit is Spell Immune, challenger, riot, champion and league.
3) this goes to shows that people on the Dota2 subreddit is discuss more about Dota2 esports tournament, which may suggest that Dota2 has a bigger esports tournament presence then LoL
## Models

![](https://github.com/Aspiring-DataGod9000/Subreddit-Classification-Dota2-vs-League-of-Legends-/blob/main/read_me_images/MODELLING.png)

| Models                             | Cross Validation Score | Train AUC Score | Test AUC Score | train Accuracy Score| Test Accuracy Score | Sensitivity | Specificity |       
| ---------------------------------- | ---------------------- | --------------- | -------------- | ------------------- | -----------         | ----------- | ----------- |
|TF-IDFVec + Multinomial Naive Bayes |	0.970813              |	0.995011        | 0.970556       |	0.963163	       | 0.908362	         | 0.947317	   | 0.852982    |
|CountVec + Multinomial Naive Bayes  |	0.967973	          |0.986141	        | 0.969839	     | 0.943271	           | 0.902062	         | 0.903415	   | 0.900139    |
|TF-IDF Vec + random forest	         |	0.949812              |     0.999075    | 0.958665	     | 0.993861	           | 0.899198	         | 0.960000	   | 0.812760    |
|TF-IDFVec + Logistic Regression  	 |0.967175                |	0.994350	    | 0.969788	     | 0.946709	           | 0.895762	         | 0.972683	   | 0.786408    |
|CountVec + Random Forests	         |  0.947185	          | 0.998788	    | 0.954295	     | 0.994352	           | 0.895189	         | 0.932683	   | 0.841886    |
|CountVec + Logistic Regression	     |     0.956559	          |0.992004	        | 0.965459	     | 0.916749	           | 0.870561	         | 0.976585	   | 0.719834    |

## Conclusion And Recommendation

From the results above we can observe that Multinomial Naive Bayes in TF-IDF vector data gives the highest accuracy, and will hence be the model choosen for model testing and evaluation. With the model accuracy score of 90.%, it is also safe to assume that the model will be adequent at classifying posts and comments on Twitch's now single thread forum for VideoGames. The model will however be expect to be a little over-fitted when doing the actual test especially when we are doing classification outside of reddit, with data pulled from reddit. The following section on limitations and future works will detail how we can improve this model to further improve model accuracy and reduce model over-fitting.
## Limitation & Future Works

As seen from the Train and test results from each models that the model is slightly overfitted. This is a result of insufficient removal of extra stopwords, and words that are not meaningful in classifying the respective video games comments. For e.g. the word Gold is one of the predictors of the model but it appears in both subreddits as both the in-game currency in Dota2 and LoL is refered to as Gold.
The analysis is only based on 3 models, other models like KNN might give better results.
Sub-threads from sources other than reddit can be used for a more holistic analysis for model building
