# Introduction 
League of Legends is a team-based strategy game where two teams of five powerful champions face off to destroy the other's base. The game provides players with the option to choose one of 140+ champions, allowing players to play through a vast array of strategies and different playstyles. 

### Background
For many League of Legends players, choosing the best champion to play is often a tough choice. It would therefore be valuable to gain insights into what makes each champion unique, what each champion excels at, and what champions share similar playstyles.

### Goal of the Project
This project was created to predict what champion a player played during a ranked 5v5 League of Legends game based on their game data. The primary cause for prediction is inference, as determining what the most important features in determining champion picked would be valuable in finding out what distinguishes each champion in League of Legends.

---
# Methods
The dataset was assembled using [Riot's developer APIs](https://developer.riotgames.com/apis). I started by initially assembling a sample of 720 players. In order for the sample to accurately reflect the general population of players, I collected number's of players proportional to the overall rank distribution in League of Legends. This meant that the majority of players were from the ranks of bronze to platinum, whilst only a couple were chosen from the upper ranked echelons of grandmaster-challenger. The player's that were selected also had to have had at least 100 games played in the current ranked season.

### Data Exploration
The assembled dataset comprised of 701,540 observations and 96 features. 17 features were categorical whilst the remaining 79 were numerical. Plotting a histogram of champions picked, we can see the dataset is severely imbalanced, with many champions having few corresponding observations.

![Class distribution](
