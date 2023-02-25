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

### Data Cleaning
The first step to cleaning the data was keeping only the rows where the roles were either Support or Jungler. This was done as the study focuses only on those positions on the team and thus removes the unneeded rows from the dataset. The next step that was taken was to keep only the relevant columns that help answer the proposed question. In particular, the columns kept were ‘position’, ‘kills’, ‘deaths’, ‘assists’, ‘teamkills’, and ‘visionscore’. These columns were kept for either later analysis or calculations of new data to be added to the dataset.

Using these columns, the stat kill participation (labeled ‘killparticipation’ in the DataFrame) was calculated. Regarded as one of the most important stats within League of Legends, kill participation determines the proportion of team kills a player was a part of. A higher kill participation is considered better in contrast to a lower kill participation.

Another stat calculated was kda - kill-death/assists ratio (labeled ‘kda’ in the DataFrame) - which shows if a player has a positive or negative performance on the game. A higher kda is considered favorable in comparison to a lower kda.

With all calculations complete, the following columns are kept: ‘position’, ‘visionscore’, ‘killparticipation’, and ‘kda’. These columns will be used for the permutation test to help answer the question proposed. The last step taken in cleaning the data was to find any missing values and decide what to do with them. While looking through the data, only 4 NaN values were found and were all in the ‘visionscore’ column. Since there were only 4 missing values out of the entire cleaned dataset, those rows were dropped so they don’t need to be dealt with during the testing. Because of this, ‘visionscore’ was changed to int type as the values are best reflected in this manner.

## Univariate Analysis
The frequency histogram of ‘killparticipation’ illustrates that the stat is somewhat balanced. The shape resembles a normal curve but also contains some outliers at each end. The frequency histogram of ‘visionscore’ conveys that the stat in professional matches is very inconsistent since the plot is positively skewed.

## Bivariate Analysis
It was initially thought that the scatter plot between ‘killparticipation’ and ‘kda’ would highlight that a higher kill participation stat would result in a higher kda. However, while somewhat true as the plot trends positively, it is also possible to have a high kill participation and low kda as seen in the graph.

## Interesting Aggregates
While looking at the grouped table, it can be seen that the difference between the grouped means, medians, and standard deviations of ‘killparticipation’ and ‘kda’ is very minimal. In stark contrast, the difference between the grouped means, medians, and standard deviations of ‘visionscore’ is substantial. This helps explain how the histogram of ‘visionscore’ is positively skewed since Supports have a greater mean, median, and standard deviation in comparison to Junglers.

# Assessment of Missingness

# Hypothesis Testing