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

| position   |   visionscore |   killparticipation |   kda |
|:-----------|--------------:|--------------------:|------:|
| jng        |            48 |            0.888889 |   1.6 |
| sup        |            69 |            0.777778 |   1.4 |
| jng        |            39 |            0.736842 |  14   |
| sup        |            67 |            0.947368 |   9   |
| jng        |            52 |            0.666667 |   1   |

### Univariate Analysis
The frequency histogram of ‘killparticipation’ illustrates that the stat is somewhat balanced. The shape resembles a normal curve but also contains some outliers at each end. The frequency histogram of ‘visionscore’ conveys that the stat in professional matches is very inconsistent since the plot is positively skewed.

### Bivariate Analysis
It was initially thought that the scatter plot between ‘killparticipation’ and ‘kda’ would highlight that a higher kill participation stat would result in a higher kda. However, while somewhat true as the plot trends positively, it is also possible to have a high kill participation and low kda as seen in the graph.

### Interesting Aggregates
While looking at the grouped table, it can be seen that the difference between the grouped means, medians, and standard deviations of ‘killparticipation’ and ‘kda’ is very minimal. In stark contrast, the difference between the grouped means, medians, and standard deviations of ‘visionscore’ is substantial. This helps explain how the histogram of ‘visionscore’ is positively skewed since Supports have a greater mean, median, and standard deviation in comparison to Junglers.

|   ('visionscore', 'mean') |   ('visionscore', 'median') |   ('visionscore', 'std') |   ('killparticipation', 'mean') |   ('killparticipation', 'median') |   ('killparticipation', 'std') |   ('kda', 'mean') |   ('kda', 'median') |   ('kda', 'std') |
|--------------------------:|----------------------------:|-------------------------:|--------------------------------:|----------------------------------:|-------------------------------:|------------------:|--------------------:|-----------------:|
|                   43.1164 |                          41 |                  16.7728 |                        0.686667 |                          0.695652 |                       0.178333 |           5.17399 |                   3 |          5.05879 |
|                   79.2727 |                          77 |                  27.8943 |                        0.686323 |                          0.7      |                       0.191087 |           5.06084 |                   3 |          5.10975 |

# Assessment of Missingness

### NMAR Analysis
I believe that there are no columns in the dataset that are considered NMAR. The reasoning behind this belief is that if data is missing, it is because it is dependent on another column. There is also data missing due to missing by design. Since there are rows for both individuals and teams, not all columns are needed or cannot be filled in since entering data for both can be different in some scenarios.

### Missingness Dependency
The column explored for missingness was the ‘doublekill’ column. The two columns that were used to see if the ‘doublekill’ column is dependent on for its missingness were ‘league’ and ‘result’. The ‘league’ column refers to the professional league that the match was played under. The ‘result’ column refers to if a match was won or lost. Based on the results of the missingness tests, it can be seen that the ‘doublekill’ column’s missingness was dependent on the ‘league’ column and, therefore, MAR. However, when comparing the ‘doublekill’ and ‘result’ columns, the ‘doublekill’ column was not dependent at all on the ‘result column.

# Hypothesis Testing

**Null Hypothesis**: Junglers and Supports have the same impact on a professional League of Legends game.

**Alternative Hypothesis**: Supports are more important than Junglers in a professional League of Legends game.

With the columns being qualitative, the test statistic of choice is the TVD and significance level is set at 0.05. 

The resulting p-value was 0.0, and thus the null hypothesis is rejected. However, as seen earlier in the bivariate analysis of the ‘visionscore’, there is high variation in the column. Because of this, another permutation test was conducted that only focused on ‘killparticipation’ since it is considered the most important stat within League of Legends.

With the column being quantitative, the test statistic of choice is the difference in means with the significance level still set at 0.05. 

The result p-value was 0.583, and thus the null hypothesis is not rejected.

Based on the results and the question, determining the importance of a role is highly subjective. Thus, the following conclusion is drawn: if vision score, kda, and kill participation are all considered priorities, then Supports may be more useful than the Jungler role. In contrast, if kill participation is the only stat prioritized, then both roles may be considered as providing the same production value.