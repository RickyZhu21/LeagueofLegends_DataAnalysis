# LeagueofLegends_DataAnalysis
This is a cool project for DSC 80 at UCSD, analyzing which role impacts League of Legends Esports Match more: Top or Mid using official 2022 LoL eSports match data. 

# Introduction
League of Legends (LoL) is a highly popular and competitive multiplayer online battle arena (MOBA) game developed and published by Riot Games. With a massive player base worldwide, LoL has become a staple in the eSports industry. Players assume the roles of powerful champions, forming teams and battling against each other in intense strategic matches. The game features a vast roster of unique champions, each with their own abilities and playstyles, providing endless possibilities for dynamic gameplay and strategic depth. 

Throughout our gaming experience League of Legends, we are interested on the question: Which role “carries” (does the best) in their team more often: Top (top) or Mid laners(mid)? 

To answer the question, we used the dataset contains contains 2022 League of Legends eSports match data from OraclesElixir, as it's representative for the League of Legends player population and meta for 2022. Also it provides valuable insights into the performance and dynamics of professional teams in the game for the future. Analyzing this dataset can offer a deeper understanding of the strategies, strengths, and weaknesses of different roles within a team.

By examining the match data from 2022, we can provide evidence-based conclusions about the impact and effectiveness of top and mid laners in carrying their teams to victory. 

**2022 League of Legends eSports match data from OraclesElixir dataset breakdown:**

Rows: Each League of Legends competitive match in 2022. 

Number of rows: 149400

**Relevant Columns:**
1. datacompleteness: Whether a player's data in a single eSport match is filled. 
2. teamname: The teamname of the player.
3. Position: The player's position in a single eSport match. League of Legends only has five positions: Top(top), Jungle(jng), Mid(mid), Bot(bot), Support(sup).
4. kills: The number of kills a player have in a single eSport match.
5. assists: The number of assist a player have in a single eSport match.
6. death: The number of death a player have in a single eSport match.
7. earned gpm: Earned gold per minute by player in a single game.
8. cspm: Creep score per minute, indicating the number of minion killed by a player per minute.
9. standardized_kda: Kill Death Assist Ratio by a player in a single game, calculated by **(Kill+Assist) / Death**, standardized. 
10. standardized_gpm: Earned gold per minute by player in a single game, standardized
11. standardized_cspm: Creep score per minute, indicating the number of minion killed by a player per minute, standardized. 
12. **carry_score**: Our measurement of how well a player perform in a game, calculated by **(standardized_kda + standardized_gpm + standardized_cspm) / 3**. 




# Cleaning and EDA (Exploratory Data Analysis)

# Assessment of Missingness

# Hypothesis Testing
