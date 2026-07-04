This dataset includes 49,393 results of international football matches starting from the very first official match in 1872 up to 2025. The matches range from FIFA World Cup to FIFI Wild Cup to regular friendly matches. The matches are strictly men's full internationals and the data does not include Olympic Games or matches where at least one of the teams was the nation's B-team, U-23 or a league select team.

results.csv includes the following columns:
1. date - date of the match
2. home_team - the name of the home team
3. away_team - the name of the away team
4. home_score - full-time home team score including extra time, not including penalty-shootouts
5. away_score - full-time away team score including extra time, not including penalty-shootouts
6. tournament - the name of the tournament
7. city - the name of the city/town/administrative unit where the match was played
8. country - the name of the country where the match was played
9. neutral - TRUE/FALSE column indicating whether the match was played at a neutral venue

shootouts.csv includes the following columns:
1. date - date of the match
2. home_team - the name of the home team
3. away_team - the name of the away team
4. winner - winner of the penalty-shootout
5. first_shooter - the team that went first in the shootout

goalscorers.csv includes the following columns:
1. date - date of the match
2. home_team - the name of the home team
3. away_team - the name of the away team
4. team - name of the team scoring the goal
5. scorer - name of the player scoring the goal
6. own_goal - whether the goal was an own-goal
7. penalty - whether the goal was a penalty

former_names.csv includes the following columns:
1. current - name of the team as is used currently (or the last name if the team does not exist anymore)
2. former - former name used by said team
3. start_date - start date of when former name was used
4. end_date - end date of when former name was used
