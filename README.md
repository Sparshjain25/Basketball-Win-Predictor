# Basketball-Win-Predictor
Basketball analytics has evolved significantly, leveraging data to enhance team strategies and predict game outcomes. In this project, I delve into an extensive basketball dataset to uncover key performance metrics and forecast playoff dynamics. Our analysis encompasses critical metrics such as offensive and defensive rates, providing insights into team strengths and weaknesses. Utilizing these metrics, I developed predictive models to estimate win percentages for teams in the playoffs, offering a data-driven approach to assessing team success. Additionally, I built a model to predict the number of games between two teams in the playoffs, adding a layer of foresight to playoff predictions. This project aims to demonstrate the power of data analytics in sports and provide valuable tools for teams and analysts to make informed decisions during the crucial playoff season.

### SEASONS COVERED ###

Both player and team data cover the 2014-15 to 2023-24 regular seasons and the 2004-05 to 2022-23 playoffs

# Explanations for select columns

### player_game_data columns ###

season: The starting season of an NBA calendar year. The 2023 season is the 2023-24 NBA season. This means that the 2024 playoffs took place during the 2023 season (i.e. 2023-24 season).

gametype: An indicator for whether the game was from the regular season (gametype = 2) or playoffs (gametype = 4)

offensivereboundchances: The number of opportunities the player had to grab an offensive rebound while on the court (for example, a teammate missed FGA). This is the appropriate denominator if you would like to calculate offensive rebound percentage (OREB%).

defensivereboundchances: The number of opportunities the player had to grab a defensive rebound while on the court (for example, an opposing team missed FGA). This is the appropriate denominator if you would like to calculate defensive rebound percentage (DREB%).

shotattempts: The total number of shots plus shooting fouls drawn by the player. Shot attempts represents the number of team shooting opportunities utilized by the player. It is the appropriate denominator for the efficiency measure points per attempt (shotattemptpoints/shotattempts). This measure is roughly equal to 2*TS% and can be used in situations when you would normally use TS%.

shotattemptpoints: The total number of points scored on FGA + shooting foul FT points. It does not include player points from off ball foul FT and other non-SF free throws (like technical foul shots). It is the numerator for PPA.

offensiveseconds: The number of seconds the player played on offense.

offensivepossessions: The number of offensive possessions the player played. 

defensiveseconds: The number of seconds the player played on defense.

defensivepossessions: The number of defensive possessions the player played.

teampoints: The number of points the player's team scored when he was on the court.

opponentteampoints: the number of points the opponent scored when the player was on the court.

teamshotattempts: the number of shot attempts the player's team took when the player was on the court (see above for shot attempt definition)


### team_game_data columns ###

**NOTE** : All stats are team stats from the perspective of the offensive team.

reboffensive: the number of offensive rebounds gathered by the offensive team. Note that this includes "team" rebounds and thus should be >= the sum of individually credited offensive rebounds for the players on that team in that game. This is the numerator for team OREB%.

rebdefensive: the number of defensive rebounds (both individual and team) conceded by the offense. This is NOT the number of defensive rebounds that the offensive team got. For example, if the row lists GSW on offense and NOP on defense, rebdefensive is the number of rebounds that NOP gathered when GSW was on offense and NOP was on defense. This is the numerator for team DREB%.

reboundchance: An opportunity for a rebound when the off_team was on offense and the def_team was on defense. This is the denominator for team REB% and includes both individual and team rebounds.

### Common Advanced Stat Definitions ###

Here are a few definitions of common measures that you may want to use:

PPA = shotattemptpoints/shotattempts

USG% = (shotattempts + turnovers)/(teamshotattempts + team turnovers)

AST% = assists/(teamfgmade - (fg3made + fg2made)) [rephrased as: assists/(teammate made shots)]

OREB% = offensiverebounds/offensivereboundchances

DREB% = defensiverebounds/defensivereboundchances

TOV% = turnovers/(shotattempts + turnovers) [Note that this is sometimes alternatively defined as turnovers/(possessions/100)]

STL% = steals/defensivepossessions

BLK% = blocks/opponentteamfg2attempted

ORTG = points/(possessions/100)

DRTG = points allowed/(defensive possessions/100) [Same as ORTG calculation but for the defensive team]

NET RTG = ORTG - DRTG

### Questions covered for this dataset ###

#### PART 1 -
1. What was the Warriors' Team offensive and defensive eFG% in the 2015-16 regular season? Remember that this is in the data as the 2015 season.
2. What percent of the time does the team with the higher eFG% in a given game win that game? Use games from the 2014-2023 regular seasons. If the two teams have an exactly equal eFG%, remove that game from the calculation.
3. What percent of the time does the team with more offensive rebounds in a given game win that game? Use games from the 2014-2023 regular seasons. If the two teams have an exactly equal number of offensive rebounds, remove that game from the calculation.
4. Do you have any theories as to why the answer to question 3 is lower than the answer to question 2?
5. Look at players who played at least 25% of their possible games in a season and scored at least 25 points per game played. Of those player-seasons, what percent of games were they available for on average? Use games from the 2014-2023 regular seasons.
6. What % of playoff series are won by the team with home court advantage? Give your answer by round. Use playoffs series from the 2014-2022 seasons. Remember that the 2023 playoffs took place during the 2022 season (i.e. 2022-23 season).
7. Among teams that had at least a +5.0 net rating in the regular season, what percent of them made the second round of the playoffs the following year? Among those teams, what percent of their top 5 total minutes played players (regular season) in the +5.0 net rating season played in that 2nd round playoffs series? Use the 2014-2021 regular seasons to determine the +5 teams and the 2015-2022 seasons of playoffs data.  

#### PART 2 -
For this part, I will work to fit a model  that predicts the winner and the number of games in a playoffs series between any given two teams.   
Include, as part of your answer:   
  - A brief written overview of how your model works, targeted towards a decision maker in the front office without a strong statistical background.  
  - What you view as the strengths and weaknesses of your model.  
  - How you'd address the weaknesses if you had more time and/or more data.  
  - Apply your model to the 2024 NBA playoffs (2023 season) and create a high quality visual (a table, a plot, or a plotly) showing the 16 teams' (that made the first round) chances of advancing to each round.
  - 
**COMMENT** -
This is an intentionally open ended question, and there are multiple approaches we can take. Here are a few notes and specifications:    
1. My final output includes the probability of each team winning the series. For example: “Team A has a 30% chance to win and team B has a 70% chance.” instead of “Team B will win.” I am also predicting the number of games in the series.
2. I have only used data available prior to the start of the series. For example, I am not using a team’s stats from the 2016-17 season to predict a playoffs series from the 2015-16 season.

#### PART 3 -
Find two teams that had a competitive window of 2 or more consecutive seasons making the playoffs and that under performed your model’s expectations for them, losing series they were expected to win. Why do you think that happened? Classify one of them as bad luck and one of them as relating to a cause not currently accounted for in your model.

