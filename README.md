# NBAScoresPrediction
Predicts Over/Under and Score Difference on Daily NBA Matchups

## Motivation
The average points scored per team in a game is 112 in the season 2020-2021 and that makes the total 224 points. The over/under threshold ranges from 200 to 240 in different matchups and I'm curious to find out if the variaton/uncertainty is indeed +- 20 points. In sports betting, the score difference is often broken down into intervals of 5 points and I'm also curious if I can limit the score difference down to a few brackets with little uncertainty. 

## Approach
In the 2020 season due to COVID-19, many teams play against each other back to back with a rest day in between to decrease travelling. It occurred to me that the second game outcome can be heavily related to the first game which they played just 2 days ago. I was only taking in games within 7 days of each other, and later had no such limit because I was using a random forest that can take care of that limit for me and the results were a little better with no limit on the number of days in between.

## Files
[GetData](GetData.ipynb): Get NBA game data from 1983 to 2019 and the play-by-play data for each game, clean them up to the training data format, and save them to a local Postgres database.

[Models](Models.ipynb): Implement clustering on play-by-play data to generate features and model the score total and difference given the first game outcomes. Webscrape the game schedule for tomorrow from MSN at https://www.msn.com/en-us/sports/nba/schedule, make predictions, and email to myself.

[UpdateGames](UpdateGames.ipynb): A script to be run daily to update the local database by getting the game and play-by-play data today, converting them to training data format, and adding them to the local database.

### Key Takeways and Notes
* Time series analysis and clustering on time series data
* Mean Absolute Error 9 points for score difference and 14 for total score. If our prediction is 14 points higher than the over/under threshold, we can confidently go with Over and vice versa.
* Add in more variables to capture recent performance.
