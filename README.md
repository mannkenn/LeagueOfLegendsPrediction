Intro: League of Legends is a team-based strategy game where two teams of five powerful champions face off to destroy the other's base. The game provides players with the option to choose one of 140+ champions to allowing players to play through a vast array of strategies and different playstyles. 

Background: For many League of Legends players, often choosing the best champion to play is a tough choice, granted there are so many options to choose from. From a player's standpoint, it would therefore be valuable to gain insights into what makes each champion unique, and generally what each champion excels at.

Goal of the project: This project was created to predict what champion a player played during a ranked 5v5 League of Legends game based on their game data. The primary cause for prediction is inference, as determining what the most important features in determining champion picked would be valuable in finding out what distinguishes each champion in League of Legends.

Assembling the Dataset: The dataset was assembled using Riot's developer API's. I started by initially assembling a sample of 720 players. In order for the sample to accurately reflect the general population of players, I collected number's of players proportional to the overall rank distribution in League of Legends. This meant that the majority of players were from the ranks of bronze to platinum, whilst only a couple were chosen from the upper ranked echelons of grandmaster-challenger. The player's that were selected also had to have had at least 100 games played in the current ranked season.

 From there, I got the players corresponding encrypter player id's through another API, and used that to assemble a list of the player's 100 most recent games. 

After assembling game data from all of the games, I upserted the data into a postgreSQL server. When upserting the data, I avoided headaches later down the road by simply skipping any matches that contained metadata errors. Hopefully this would lead to a somewhat cleaner dataset that I wouldn't have to clean too much.


Initial data exploration:
Shape:
approx 700,000 observations, 96 features. 17 categorical and 79 numerical. 

Many features are highly correlated with game duration such as champion level, gold earned, total damage 

Game duration normally distributed, sample average game time about 30 minutes. Longest game played was about 1 hour and 7 niutes, minimum game time played is about 3 minutes, or roughly the time it takes to remake. 

Imbalanced data 

What features are affected by game length?
Insert figure

KDA not normally distributed, as well as many other quantitative features

High multicollinearity

Outliers? 
