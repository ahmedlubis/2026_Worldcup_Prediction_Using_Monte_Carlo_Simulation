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


Rank | Country      |Times Crowned Champion (Out of 10,000) | Probability of Winning the World Cup
1.   | Brazil       | 1,201                                 | 12.01%
2.   | England      | 1,180                                 | 11.80%
3.   | Argentina    | 1,164                                 | 11.64%
4.   | France       | 1,111                                 | 11.11%
5.   | Spain        | 1,076                                 | 10.76%
6.   | Belgium      | 908                                   | 9.08%
7.   | Portugal     | 883                                   | 8.83%
8.   | Canada       | 664                                   | 6.64%
9.   | Egypt        | 450                                   | 4.50%
10.  | Colombia     | 336                                   | 3.36%
11.  | Switzerland  | 274                                   | 2.74%
12.  | United States| 271                                   | 2.71%
13.  | Mexico       | 218                                   | 2.18%
14.  | Norway       | 197                                   | 1.97%
15.  | Morocco      | 51                                    | 0.51%
16.  | Paraguay     | 16                                    | 0.16%

Understanding the Underlying Data
The model relies heavily on a comprehensive dataset of 49,393 historical men's full international football matches spanning from 1872 to 2025: 
- The Primary Data (results.csv): The code reads the main match history data, utilizing key details such as the date, the teams playing (home_team, away_team), and the full-time scores (home_score, away_score, which include extra time but exclude penalty shootouts).
- Filtering for Modern Relevance: To make the 2026 predictions accurate, the simulation discards ancient history (like matches from the 1800s or mid-1900s) and specifically filters the data to only include modern matches played from January 1, 2015, onward.
- Clean Data Scope: The underlying dataset strictly excludes Olympic games, B-teams, U-23 squads, or league selections, ensuring the team ratings are built purely on true senior, full international performances. Auxiliary files tracking penalty shootouts (shootouts.csv), goalscorers (goalscorers.csv), and historical team name changes (former_names.csv) provide the complete context behind these international records.

Key Takeaways From the Model
- The Top 5 Contenders are Extremely Close: Brazil, England, Argentina, France, and Spain are the heavy favorites, each holding a roughly 10% to 12% chance of winning. Brazil tops the list, winning 1,201 times out of the 10,000 runs.
- How the Model Decided This: The simulation calculates an Attack Rating and a Defense Rating for each country based on their goals scored and conceded since 2015 relative to global averages. Teams like Brazil and England have historically scored many goals while conceding few, giving them a heavy advantage when the algorithm randomly generates match scores using a Poisson distribution (rpois).
- The Role of Penalties: If a simulated match ends in a draw after full/extra time, the model simulates a penalty shootout with a balanced 50:50 coin-flip probability to determine who advances.
- The "Underdogs": Teams like Morocco (0.51%) and Paraguay (0.16%) have very low probabilities. This doesn't mean they are terrible teams; it means that in a strict knockout bracket where you have to win 4 matches in a row against world-class teams, their mathematical chances of pulling off 4 consecutive upsets are incredibly slim based on their modern statistical ratings.  


Based on the methodology and code provided in the study, here are the key limitations of this research simulation:
1. Oversimplified Penalty Shootout Logic
   When a knockout match ends in a draw, the model decides the winner using a simple 50:50 random sample (sample(c(team_A, team_B), 1)). This ignores critical real-world factors, such as:
   --> A team's historical performance or psychological resilience in penalty shootouts.
   --> Individual player skills (e.g., penalty takers' conversion rates and goalkeepers' penalty-saving abilities).
2. Incorrect Tournament Structure (Ignoring the 2026 Format)
   The simulation bypasses the group stage entirely and hardcodes a standard Round of 16 bracket with 16 pre-selected teams.
   --> In reality, the 2026 FIFA World Cup features an expanded 48-team format with a Round of 32 knockout stage.
   --> By ignoring group stage dynamics (fatigue, goal differentials, third-place qualification rules) and starting at an artificial Round of 16, the simulation excludes a significant portion of the tournament's actual volatility.
3. Lack of Strength-of-Schedule Adjustments
   The attack_rating and defense_rating are calculated based on raw goals scored and conceded divided by total games played since 2015.
   --> The model treats all opponents equally. For example, a team that scores multiple goals against historically weaker opponents in continental qualifiers will have an inflated attack rating compared to a team playing in a highly competitive region (e.g., CONMEBOL or UEFA), as the model does not weight ratings based on opponent quality.
4. Recency Bias and Static Ratings
   The study aggregates all historical data from 2015 onwards.
   --> No Weighting for Recent Form: A match played in 2015 carries the exact same mathematical weight as a match played in 2026.
   --> Roster and Manager Turnover: International squads change rapidly. A decade-long dataset fails to capture sudden drops or surges in form caused by golden generations retiring, managerial changes, or current star player injuries.
5. Standard Poisson Distribution Constraints
   The simulation relies on independent Poisson distributions (rpois) to generate team goals.
   --> Football goal counts often violate pure independence assumptions. In real matches, a game's state heavily influences scoring; for instance, a team leading by 2 goals might shift to an ultra-defensive strategy, or a trailing team might concede more on a counter-attack. The model fails to capture these dynamic in-game shifts.
6. Arbitrary Default Ratings
   If a team in the bracket is not found in the historical dataset, the function assigns them a default rating of 1.0. While this keeps the code running, giving an unlisted team an exactly average baseline rating could heavily skew predictions if that team is a major underdog or an unranked overachiever.  
