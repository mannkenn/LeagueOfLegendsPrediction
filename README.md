# LeagueOfLegendsPrediction
Predicting champion picked and outcome (Win/Loss) of League of Legends games based on match data.  

# Project Overview
* Predicted what champion was played out of 140 available champions in League of Legends based on ranked match data
* Assembled dataset with over 700,000 entires from over 72,000 ranked games using Riot Games API
* Engineered features like classifying whether a champion is AP/AD based on type of damage, and normalized continuous features by game duration
* Built ML pipeline and used Random Forest, K-Nearest Neighbors, Support Vector Machines, Naive-Bayes, and Logistic Regression achieving 84% with Random Forest algorithm
* Performed cross-validation to ensure random forest was not overfitting achieving mean of 84% accuracy

### Assembling Dataset
* Used Riot's [LEAGUE-V4]([https://www.example.com](https://developer.riotgames.com/apis#league-v4)https://developer.riotgames.com/apis#league-v4) and [SUMMONER-V4](https://developer.riotgames.com/apis#summoner-v4) APIs to get a set of player names from each rank then filtered player names to represent overall rank distribution of League of Legends players. This was to assemble a dataset that would be more representative of the overall playerbase rather than just equal amounts of players from each rank.
* From there I filtered even further to only get players who have played more than 100 ranked so the dataset would represent active players
* Left me with 720 players to get 100 games each from
* Used Riot's [MATCH-V5](https://developer.riotgames.com/apis#match-v5) API to assemble dataset of 72,000+ ranked games from summoner names
* Connected to PostgreSQL server to store data

### Cleaning Data
* [MATCH-V5](https://developer.riotgames.com/apis#match-v5) API returned json including everything I needed
* Created dataframe filtering through json: metadata -> participants -> info to access actual game data of players
* By creating dataframe when getting data from api, I reduced a lot of the data cleaning up front by just skipping matches that returned KeyErrors
* Filtered out remade games (games where someone was AFK)
* Used [Community Dragon](https://raw.communitydragon.org/latest/) to map item ids and summoner spell ids to actual game names for simplicity
* Dropped duplicate games
* Data had no null values thanks to creating dataframe manually when assembling data from API

### Exploratory Data Analysis


