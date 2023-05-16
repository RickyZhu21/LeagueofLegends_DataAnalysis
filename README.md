# League_of_Legends_Data_Analysis
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


# Assessment of Missingness

# Hypothesis Testing
