# Executive Summary

*By Calahan Lackovic and Zach Riley*

---

Calahan Lackovic and Zach Riley

Data Collection: 

Articles: (df_articles)

We gathered 169 articles about Men’s DI ultimate frisbee in 2023 from Ultiworld, the most reputable news source in ultimate frisbee (https://ultiworld.com/division/usau-college-d-i-mens). Viewing each article requires a user to log in, presenting a challenge when trying to scrape all the text programmatically. With the use of the selenium package and several troubleshooting sources, we were able to write a script to visit a particular article, navigate to the login page, enter our credentials, and proceed to scrape the desired text. Iterating through this process for each link, we populated a data frame containing the text, author, title, and date of each article. Given the need to wait for a page to load, scraping all the articles took over half an hour in runtime. This was done in a separate notebook (Web Scraping) so that we only had to run it once, since it took so long.

Upon manually searching through the articles in a CSV file, we found several of them to be irrelevant to our research, as they discussed other divisions, despite their location on the Ultiworld website. After such cleansing, we were left with 163 articles for analysis. Of these articles, we removed certain mentions of teams that were not about our search, but would have caused problems when looking for occurrences. One example was UNC-Wilmington, which would have counted as North Carolina (UNC) in our search, so it was removed. 

Team Rankings and Rosters: (df_rankings and df_rosters)

	USAU, the governing body of ultimate frisbee in the United States, displays the rank, name, roster, and school for every registered team in the college division on its website. From this source, we populated two data frames. A rankings data frame hosted the names of the entire roster of each team while a rankings data frame contained the rank, name, power rating, region, and conference for each of the top twenty teams in the country. The rankings are solely determined by power rating, a metric used to determine a team’s strength based on its performance and record. The team ranked 20th in this table was Colorado College, a team competing in division three. To preserve the continuity of our data set and subsequent analysis, we replaced Colorado College with the 21st-ranked team (NC State), which indeed was in division one. 

From these data frames, and monikers we found perusing our article set, we manually constructed a dictionary containing all of the possible ways each team is mentioned. This includes team names, acronyms, school names, and player’s full names. 

Findings

	After gathering all of our data, we wanted to answer our first question, Is Cal Poly’s Men’s Ultimate Frisbee team (SLOCORE) mentioned less than other teams proportional to their rank? After running a linear regression model on first Rank and then Power rating versus total team mentions in all of the articles, we found that Cal Poly has 63 more mentions than predicted. To try and find the cause of this, we first looked at the 18 different authors. Just by count alone, Jake Thorne mentioned Cal Poly the most amount of times, with 154 mentions. This is extremely important since Jake is a recent Cal Poly alumni, and SLOCORE alumni. To see if the author had a large impact on the team mentions, we decided to test some models to predict the author. We can also see the UNC (North Carolina) is mentioned far more than any team. To do a little background research we read a few of the articles where UNC is mentioned highly out of proportion and found that in many articles, each team is compared to UNC since they were ranked first for most of the season. This contributed to their large number of mentions.

Machine Learning: 

TF-IDF

Computing the tf-idf for the text in each article, we trained a K nearest neighbors classifier using the tf-idf values for each word as the features. The model was trained to predict the author of each article. 

To little success, we used hyper-parameter tuning to plot the accuracy score of each model with a k value of 1 to 20, and found that the best model was a K nearest neighbor with 4 neighbors. 

Our best model has an accuracy of under 40%. Upon investigating this model we find that of the 18 authors listed, the model has assumed 142/169 articles were written by Keith Raynor. Keith Raynor wrote 38.2% (62) of the articles listed. 

Computing a k nearest neighbors model to predict author based on team mentions yielded a similar result. While the k=18 model displayed an accuracy of 50%, the articles attributed to different authors did not leave much to be concluded about their similarity.