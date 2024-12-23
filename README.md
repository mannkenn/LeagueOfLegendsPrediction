# LeagueOfLegendsPrediction
Using Random Forests to predict League of Legends Champions

# Project Overview
* Predicted what champions were played out of 140 available champions in League of Legends based on ranked match data
* Assembled dataset with over 700,000 entries from over 72,000 ranked games using Riot Games API
* Engineered features like classifying whether a champion is AP/AD based on type of damage, and normalized continuous features by game duration
* Built ML pipeline and used Random Forest, K-Nearest Neighbors, Support Vector Machines, Naive-Bayes, and Logistic Regression achieving 92%+ accuracy with Random Forest algorithm
* Performed cross-validation to ensure random forest was not overfitting achieving mean of 92% accuracy

## Assembling Dataset
* Used Riot's [LEAGUE-V4]([https://www.example.com](https://developer.riotgames.com/apis#league-v4)https://developer.riotgames.com/apis#league-v4) and [SUMMONER-V4](https://developer.riotgames.com/apis#summoner-v4) APIs to get a set of player names from each rank then filtered player names to represent overall rank distribution of League of Legends players. This was to assemble a dataset that would be more representative of the overall playerbase rather than just equal amounts of players from each rank.
* From there I filtered even further to only get players who have played more than 100 ranked so the dataset would represent active players
* Left me with 720 players to get 100 games each from
* Used Riot's [MATCH-V5](https://developer.riotgames.com/apis#match-v5) API to assemble dataset of 72,000+ ranked games from summoner names
* Connected to PostgreSQL server to store data

## Cleaning Data
* [MATCH-V5](https://developer.riotgames.com/apis#match-v5) API returned json including everything I needed
* Created dataframe filtering through json: metadata -> participants -> info to access actual game data of players
* By creating dataframe when getting data from api, I reduced a lot of the data cleaning up front by just skipping matches that returned KeyErrors
* Filtered out remade games (games where someone was AFK)
* Used [Community Dragon](https://raw.communitydragon.org/latest/) to map item ids and summoner spell ids to actual game names for simplicity
* Dropped duplicate games
* Data had no null values thanks to creating dataframe manually when assembling data from API

## Exploratory Data Analysis
Prior to my EDA, I already had a good idea of what features were most important just based on my domain knowledge from playing the game for thousands of hours...
* Lane
* Abilities Used
* Damage types
* Maybe items

### Correlations
![Correlations](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/correlations.png)

### Damage
Distribution
![Damage](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/damagedistribution.png)

Over Time
![Damageovertime](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/damageovertime.png)

Damage Types
![Damagetypes](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/damagetypes.png)

Can see that very specific champions emerge from seperating based on damage type, also true damage reveals champions with certain abilities. Most damage taken is by champions part of the tank class. Can conclude that damage is a defining feature of many champions.


### Healing/Shielding
One of the defining traits of some champions (mainly support ones) is the ability to heal themselves or other champions, I wanted to see if the difference was truly noticeable by getting the top healers/shielders.

![Healshield](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/healingshielding.png)

Top healers are the champions in league that everyone hates... Shielding champions are all support champions.

### Objectives
![Objectives](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/objectives.png)

Baron/dragon is almost always killed by junglers, towers and inhibitors are mainly taken by champions known as "split-pushers" or champions that can take towers from a safe distance. Funny to see that Ziggs tops the tower damage chart thanks to his passive...

### Spells Casted
### ![SpellsCasted](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/spellscasted.png)
This one was interesting, it was cool to see what champions press what abilities (Q,W,E,R) the most and how that matches up with my game knowledge. For example, transform champions like Nidalee, Jayce and Elise all spammed R. Zeri spams Q because that is her basic attack. Cass spams E because that's her bread and butter. Etc..


### Summoner Spell Choice

Summoner spell distribution

![SSdist](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/summonerspelldistribution.png)

Flash is obviously most popular, followed by TP and ignite.
![SSLane](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/summonerspellbylane.png)

Summoner spell varies greatly by lane, with junglers always taking smite.

### Vision/CC
Just wanted to see if support champions have best vision score (they should) and who CCs the most

![VisionCC](https://github.com/mannkenn/LeagueOfLegendsPrediction/blob/main/photos/visioncc.png)

Made me realize Nocturne R counts as a huge amount of CC as it blinds everyone in the game for 5 seconds.

## Feature Engineering
* Developed feature to classify whether a champion was AP/AD based on their predominant damage type for each game
* AP meant a champion had more magic damage than physical damage that game
* AD meant a champion had more physical damage than magic damage that game
* Normalized continuous features by game length so results were not skewed for shorter/longer games

## Model Building
* Top features: 'lane', 'ap', 'ad', 'spell1Casts', 'spell2Casts', 'spell3Casts', 'spell4Casts','totalDamageTaken', 'magicDamageDealtToChampions', 'physicalDamageDealtToChampions', 'trueDamageDealtToChampions','totalDamageShieldedOnTeammates','totalHeal', 'visionScore', 'timeCCingOthers', 'objective_kills', 'building_kills'
* Developed pipeline to preprocess numeric and categorical features
* Standardized continuous features to deal with right skew distributions (had lots of 0 values for example for magic damage, if a champion has no magic damage in their kit, then they would obviously do 0 magic damage, but those who do have magic damage would deal infinitely more)
* One-hot encoded lane feature rather than ordinal encoding as it is nominal
* Label encoded target feature from 0-140 representing champion names
* Trained and tested using Random forests, K-nearest neighbors, Support vector machines, Naive-Bayes, and Logistic Regression

## Results
* Random Forest algorithm achieved highest accuracy at 92%

Model: Random Forest
Accuracy: 0.929
Precision: 0.929
Recall: 0.929
F1 Score: 0.928
--------------------
Model: K Nearest Neighbours
Accuracy: 0.832
Precision: 0.838
Recall: 0.832
F1 Score: 0.831
--------------------
Model: Support Vector Machines
Accuracy: 0.919
Precision: 0.920
Recall: 0.919
F1 Score: 0.918
--------------------
Model: Naive-Bayes
Accuracy: 0.691
Precision: 0.766
Recall: 0.691
F1 Score: 0.679
--------------------
Model: Logistic Regression
Accuracy: 0.897
Precision: 0.897
Recall: 0.897
F1 Score: 0.896
--------------------
### Cross Validation
* Performed cross-validation with Random Forest to ensure model was not overfitting
* Achieved mean accuracy of 92%
