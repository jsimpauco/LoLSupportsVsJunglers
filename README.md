# LoLSupportsVsJunglers
Project for DSC80 at UCSD

# Introduction

This dataset was retrieved from [Oracle's Elixer](https://oracleselixir.com/tools/downloads) and contains data from all professional League of Legends games that were played in 2022. Within the dataset both individual and team performance stats for every game can be found. Based on the data found, the following question is proposed: Is the Support role in a professional League of Legends game more important in comparison to the Jungler role?

An important note of this dataset is that the data is taken only from **professional** League of Legends games rather than games from the whole player base. The significance of the data being from professionally played games is that a professional player's perspective on the game can be entirely different than the perspective of the general player base. For this reason, this study does not reflect the entire League of Legends player base but rather the professional community. In regards to the question proposed, many players consider the Support role to be the most influential role during a game. However, there are also those who believe that the Jungler role is underrated and at times more influential than Supports. This study hopes to answer this dispute through the use of a permutation test.

The dataset contains a total of 149232 rows and 123 columns. In particular to the question introduced, only 6 columns are relevant: ‘position’, ‘kills’, ‘deaths’, ‘assists’, ‘teamkills’, and ‘visionscore’.
- ‘position’ refers to the role played by a player throughout a match (string)
- ‘kills’ refers to the amount of kills a player attained throughout a match (int)
- ‘deaths’ refers to amount of times a player died throughout a match (int)
- ‘assists’ refers to the amount of assists a player attained throughout a match (int)
- ‘teamkills’ refers to the total amount of kills attained by a team throughout the whole game (int)
- ‘visionscore’ refers to the score calculated based on how a player both granted their team vision and denied their opposition vision (float)

# Cleaning and EDA

# Assessment of Missingness

# Hypothesis Testing