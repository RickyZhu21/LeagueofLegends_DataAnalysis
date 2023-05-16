# League_of_Legends_Data_Analysis
By Ricky Zhu(r2zhu@ucsd.edu) and Tony Guo(xig003@ucsd.edu)

# Introduction
League of Legends (LoL) is a highly popular and competitive multiplayer online battle arena (MOBA) game developed and published by Riot Games. With a massive player base worldwide, LoL has become a staple in the eSports industry. Players assume the roles of powerful champions, forming teams and battling against each other in intense strategic matches. The game features a vast roster of unique champions, each with their own abilities and playstyles, providing endless possibilities for dynamic gameplay and strategic depth. 

Throughout our gaming experience League of Legends, we are interested on the question: Which role “carries” (does the best) in their team more often: Top (top) or Mid laners(mid)? 

To answer the question, we used the dataset contains contains 2022 League of Legends eSports match data from OraclesElixir, as it's representative for the League of Legends player population and meta for 2022. Also it provides valuable insights into the performance and dynamics of professional teams in the game for the future. Analyzing this dataset can offer a deeper understanding of the strategies, strengths, and weaknesses of different roles within a team.

By examining the match data from 2022, we can provide evidence-based conclusions about the impact and effectiveness of top and mid laners in carrying their teams to victory. From our conclusion about which position carries more can motivate more players of League of Legends to become the main of that position, for example: Faker motivated million of League of Legends players to become Mid mains when people watched how Faker outperforms and carries his team SKT/T1 as a mid laner. TheShy also motivated millions of League of Legends players to become Top mains when people watched how TheShy outperforms and carries his team IG as a top laner. 

### 2022 League of Legends eSports match data from OraclesElixir dataset breakdown:

Rows: A League of Legends eSports player's match statistics in a single game in 2022. 

Number of rows: 149400

**Relevant Columns:**
1. datacompleteness: Whether a player's data in a single eSport match is filled in original dataset before we did data cleaning.

2. teamname: The name of the team the player is in.

3. position: The player's position in a single eSport match. League of Legends only has five positions: Top Laner(top), Jungle(jng), Mid Laner(mid), Bot Laner(bot), Support for Bot Laner(sup). Note: In a League of Legends match, there are 3 lanes total and jungle areas. Top laner goes to top lane, Mid laners goes to mid lane, and Jungle clears Jungle area and potentially help other lanes. Bot Laners and Support goes bot lane. 

4. kills: The number of kills a player have in a single eSport match.

5. assists: The number of assists a player have in a single eSport match.

6. death: The number of deaths a player have in a single eSport match.

7. earned gpm: Earned gold per minute by player in a single game. In League of Legends, gold is used to buy items in order to make your league character stronger.

8. cspm: Creep score per minute, indicating the number of minions killed by a player per minute.

# Cleaning and EDA (Exploratory Data Analysis)
Notes:
Each match contains 2 teams, 10 players.
We created a copy of the original dataframe to keep original dataframe intact. 

Pattern: Each 1-10 rows contains individual player's statistic in a single match, and every 11th and 12th contains the team's statistics in a single match. (5 players versus 5 players, 2 teams)
## Data Cleaning
1. Remove row contains position == team, to keep individual positions(top, mid,etc)

2. Keep only relevant columns from of the dataframe described from above.

3. Replace the column "teamname" of values such as "unknown team" to np.NaN, as "unknown team" should be considered as missing data.

4. The datacompleteness column contains 3 types: complete, ignore, and partial. We replace ignore and partial with False, and replace complete
with True. This process makes the column boolean, to present a much cleaner data. 

5. Adding a column kda_ratio: KDA ratio is Kill Death Assist Ratio by a player in a single game, calculated using the formula **(Kill+Assist) / Death**. 

6. Standardize the kda_ratio, cspm, and earned gpm column and create 3 new columns: standardized_kda, standardized_gpm, standardized_cspm

7. Adds a new column named **carry_score**: For our analysis, we calculate a score for every player called 'carry_score'. Our self designed measurement of how well a player performs in a game, calculated by **(standardized_kda + standardized_gpm + standardized_cspm) / 3**. The reason why we use these three statistics is that these three factors impact the development of a League character the most. The higher the three statistics are, the better a player's possible performance would be in various aspects such as the amount of damage dealt or the quality of a player's items equipped. Also, these three statistics are the most crucial factors in determining which player is the Most Valuable Player(i.e. MVP) in a single match.

8. Drops non-standardized columns, using standarized columns for future analysis. 

**Cleaned Data**: 
```
print(league_head.to_markdown(index=False))
```

| datacompleteness   | teamname                 | position   |   standardized_kda |   standardized_gpm |   standardized_cspm |   carry_score |
|:-------------------|:-------------------------|:-----------|-------------------:|-------------------:|--------------------:|--------------:|
| True               | Fredit BRION Challengers | top        |          -0.696223 |           0.242621 |            0.563221 |     0.0365397 |
| True               | Fredit BRION Challengers | jng        |          -0.633408 |          -0.47272  |           -0.37376  |    -0.493296  |
| True               | Fredit BRION Challengers | mid        |          -0.507778 |          -0.242903 |            0.134244 |    -0.205479  |
| True               | Fredit BRION Challengers | bot        |          -0.759038 |           0.111582 |            0.506755 |    -0.0469004 |
| True               | Fredit BRION Challengers | sup        |          -0.675285 |          -1.45253  |           -1.57038  |    -1.23273   |

## Univariate Analysis
The distribution of the standarized KDA among players: x-axis describes the KDA ratio for players in standardized units, ranging from -1 to 8,  y-axis describes the amount of players with their specific standardized KDA. 
The graph is skewed to the right, inferring that most player's standardized KDA is in the range of -1 to 0 standardized units, which implies that many player's KDA is relatively lower compared to the mean KDA within the dataset. 
<iframe src="assets/univariate2.html" width=800 height=600 frameBorder=0></iframe>

## Bivariate Analysis
Boxplot showing various information on all positions and their carry score, including median, interquartile range, and outlier. The x axis shows carry score in standardized units, and the y axis labels each of the five positions. While top laners and mid laners have similar carry score distribution, mid laners' scores are a little higher overall. 
* Interestingly, carry score tend to have more outliers when carry score is high.

<iframe src="assets/boxplot1.html" width=800 height=600 frameBorder=0></iframe>

## Interesting Aggregates
Pivot Table showing respective mean standardized KDA, GPM, CSPM, and carry score. It demonstrates the mean statistics for each position in League of Legends and can be used for comparison among different positions. For example, bot laners has the highest KDA, GPM, CSPM, and carry score in standardized units among all other positions.
```
print(league_position.to_markdown(index=True))
```

| position   |   standardized_kda |   standardized_gpm |   standardized_cspm |   carry_score |
|:-----------|-------------------:|-------------------:|--------------------:|--------------:|
| bot        |         0.122206   |           0.798652 |            0.793597 |      0.571485 |
| jng        |         0.00599775 |          -0.196162 |           -0.22893  |     -0.139698 |
| mid        |         0.0684821  |           0.430029 |            0.625648 |      0.37472  |
| sup        |        -0.0218033  |          -1.35438  |           -1.67982  |     -1.01867  |
| top        |        -0.174883   |           0.321859 |            0.489504 |      0.21216  |

# Assessment of Missingness
## NMAR Analysis
NMAR means that there is a good reason why the missingness depends on the values of a column themselves. We don't believe there are any column in our dataset that is NMAR. We would like to obtain additional information about possible correlation between datacompleteness and missingness in teamname column, as our "teamname" column is one of the column that contains missing values. 

## Missingness Dependency
We performed permutation tests to check whether "teamname" column depends on other columns
Our first permutation testing: We test if "datacompleteness" columns depends on "teamname" or not. 
We computed the p-value by comparing the simulated TVD's from the permutation testing to the observed TVD.
After obtaining the our p-value for this permutation testing: 0.004, we reject the null hypothesis: In year 2022, distribution of "datacompleteness" when "teamname" is missing is not same as when "teamname" is not missing. The result of this permutation leads to MAR, "datacompleteness" depend on "teamname" missingness. 
<iframe src="assets/missingness_perm.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/datacompleteness_new_perm.html" width=800 height=600 frameBorder=0></iframe>

Our next permutation testing is : We test if "position" columns depends on "teamname" or not.
We computed the p-value by comparing the simulated TVD's from the permutation testing to the observed TVD.
After obtaining the our p-value for this permutation testing: 0.00, we fail to reject the null hypothesis: In year 2022, distribution of "position" column when "teamname" is missing is the same as when "teamname" is not missing. The result of this permutation leads to MCAR, "position" does not depend on "teamname" missingness. 
<iframe src="assets/missingness_pos_perm.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/position_new_perm.html" width=800 height=600 frameBorder=0></iframe>

# Hypothesis Testing
We are focused on the following question: Which role “carries” (does the best) in their team more often: Top (top) or Mid laners(mid)?" using permutation testing. 

Null hypothesis: Top carries(does the best) in their team as the same as the mid laners(mid). 

Alternative hypothesis: Mid carries (does the best) in their team more often than top, as we observed from the boxplot in bivariate analysis such that the observed carry score for Mid laner is higher than Top laners in general. 

Choice of test statistic: Difference in group means of carry_score between Top laners and Mid laners, as the distribution of carry score between Top laners and Mid laners are similar shapes, but shifted version of each other demonstrated in the graph below. 

<iframe src="assets/hypothesis_stat.html" width=800 height=600 frameBorder=0></iframe>

Significance Level: 0.05 significance level. We use 0.05 as our significance level as it's widely used in many hypothesis testing. 

Result p-value: 0.0, from our permutation testing. 

Conclusion: We reject the null hypothesis, which suggests that Mid laners might possibly carry (do the best) in their team more often than top. This rejection is based on our statistical analysis, specifically the calculation of the p-value, which is a measure of the likelihood of obtaining a result as extreme as, or more extreme than, the one observed if the null hypothesis were true. In our case, the obtained p-value is less than the commonly used significance level of 0.05 (0.0 < 0.05), indicating that the observed result is statistically significant.

However, it is important to consider the limitations of our study, such as the specific context, sample size, and potential confounding variables, when interpreting these results. Further research and analysis may be warranted to gain a deeper understanding of the relationship between Mid laners and their impact on team performance.
