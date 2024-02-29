# LeagueOfLegendsPrediction
Predicting champion picked and outcome (Win/Loss) of League of Legends games based on match data.  

# Project Overview
* Test

## Intro
The goal of this project was to teach me the data science workflow. From assembling a dataset all the way to selecting and training ML models, I wanted to learn it all in one go.

I chose to do this project on League of Legends as I have EXTENSIVE expertise on the game, and it would be easier for me to understand all the features in my assembled dataset.

I had the choice of using a pre-made dataset vs. assembling my own. Of course I chose the harder option (which truly tested my sanity) but it taught me a lot and really honed in the idea that 80% of a data scientists work is spent cleaning and assembling data. I go more in detail on how I assembled my dataset in the (#getting-data). 


## Getting Data
Boy oh boy was this by far the longest part of the project... 

Riot Games provides many handy developer APIs which you can use to access all sorts of fun things. Unfortunately the things you can do with said APIs are very limited because of specified rate limits when you use your personal developer API key. 

Because of this, I had to get pretty creative on how I was going to assemble my dataset. 

First of all, I wanted to assemble a dataset that represented the overall League of Legends population (in North America specifically). Using Riot's LEAGUE-V4 API, you can get player usernames from every rank and division in League of Legends. Problem is, the API returns a set number of players for each rank and division you input. This is not representative of League of Legends' overall rank distribution, so I had to filter for that. 





