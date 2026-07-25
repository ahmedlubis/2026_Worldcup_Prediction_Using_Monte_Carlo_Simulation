# ⚽ International Football Match Analysis & World Cup Simulation

## 📖 Dataset Overview

This project analyzes historical **men's full international football matches** and applies statistical simulation techniques to estimate potential outcomes in a FIFA World Cup-style tournament.

The dataset contains **49,393 international football matches** spanning from the first official international match in **1872** until **2025**.

The data covers various international competitions, including:

- FIFA World Cup
- International tournaments
- Friendly matches
- Other recognized senior men's competitions

### Dataset Scope

The dataset strictly includes:

✅ Men's senior full international matches  
✅ Official national teams  
✅ Matches from 1872–2025  

The dataset excludes:

❌ Olympic Games  
❌ B-team matches  
❌ U-23 teams  
❌ League selection teams  

This ensures that team performance ratings are based purely on senior international competition.

---

# 🗂️ Dataset Structure

The dataset consists of four interconnected files:

---

# 1. Match Results (`results.csv`)

The primary dataset containing historical match outcomes.

| Column | Description |
|--------|-------------|
| **date** | Date of the match |
| **home_team** | Home team name |
| **away_team** | Away team name |
| **home_score** | Full-time home team score (including extra time, excluding penalties) |
| **away_score** | Full-time away team score (including extra time, excluding penalties) |
| **tournament** | Tournament or competition name |
| **city** | Match location city |
| **country** | Country where the match was played |
| **neutral** | Indicates whether the match was played at a neutral venue |

---

# 2. Penalty Shootouts (`shootouts.csv`)

Contains information about penalty shootouts after drawn knockout matches.

| Column | Description |
|--------|-------------|
| **date** | Match date |
| **home_team** | Home team |
| **away_team** | Away team |
| **winner** | Winner of the penalty shootout |
| **first_shooter** | Team taking the first penalty |

---

# 3. Goal Scorers (`goalscorers.csv`)

Contains detailed information about goals scored during matches.

| Column | Description |
|--------|-------------|
| **date** | Match date |
| **home_team** | Home team |
| **away_team** | Away team |
| **team** | Team scoring the goal |
| **scorer** | Player scoring the goal |
| **own_goal** | Whether the goal was an own goal |
| **penalty** | Whether the goal came from a penalty |

---

# 4. Historical Team Names (`former_names.csv`)

Tracks historical changes in national team names.

| Column | Description |
|--------|-------------|
| **current** | Current team name |
| **former** | Previous team name |
| **start_date** | Start date of former name usage |
| **end_date** | End date of former name usage |

---

# 🏆 World Cup Simulation Results

A Monte Carlo simulation with **10,000 tournament iterations** was conducted to estimate each team's probability of winning the World Cup.

## Predicted Championship Probability

| Rank | Country | Championships (Out of 10,000) | Winning Probability |
|------|---------|-------------------------------:|--------------------:|
| 1 | Brazil | 1,201 | 12.01% |
| 2 | England | 1,180 | 11.80% |
| 3 | Argentina | 1,164 | 11.64% |
| 4 | France | 1,111 | 11.11% |
| 5 | Spain | 1,076 | 10.76% |
| 6 | Belgium | 908 | 9.08% |
| 7 | Portugal | 883 | 8.83% |
| 8 | Canada | 664 | 6.64% |
| 9 | Egypt | 450 | 4.50% |
| 10 | Colombia | 336 | 3.36% |
| 11 | Switzerland | 274 | 2.74% |
| 12 | United States | 271 | 2.71% |
| 13 | Mexico | 218 | 2.18% |
| 14 | Norway | 197 | 1.97% |
| 15 | Morocco | 51 | 0.51% |
| 16 | Paraguay | 16 | 0.16% |

---

# ⚙️ Simulation Methodology

## Data Preparation

The model uses historical international football performance data to calculate team strength.

### Primary Dataset

The simulation relies mainly on:

`results.csv`

Key variables:

- Match date
- Home team
- Away team
- Goals scored
- Goals conceded

---

## Modern Performance Filtering

To improve relevance for modern football prediction, historical data was filtered.

The simulation uses only matches from:

```
January 1, 2015 - 2025
```

This reduces the influence of outdated football eras and better reflects current team strength.

---

## Team Rating Calculation

Each national team receives:

### ⚔️ Attack Rating

Calculated from:

- Goals scored
- Number of matches played
- Comparison against global scoring averages

### 🛡️ Defense Rating

Calculated from:

- Goals conceded
- Number of matches played
- Comparison against global defensive averages

Teams with stronger attacking and defensive records receive higher probabilities during simulation.

---

## Match Simulation Model

The model generates match scores using a **Poisson distribution**.

The simulation process:

1. Generate expected goals for both teams.
2. Simulate match score.
3. Determine winner.
4. If tied after full/extra time:
   - Simulate penalty shootout.
   - Winner selected using a 50:50 probability.

---

# 📊 Key Findings

## 1. Top Contenders Are Closely Matched

The simulation shows that the strongest World Cup contenders are:

1. Brazil
2. England
3. Argentina
4. France
5. Spain

Each team has approximately a **10–12% probability** of winning the tournament.

Brazil ranks first by winning:

> 1,201 simulations out of 10,000 runs

---

## 2. Why These Teams Rank Highly

The model favors teams with:

- High goal-scoring ability
- Strong defensive records
- Consistent international performance since 2015

Countries such as Brazil and England receive strong ratings because they combine:

- High attacking output
- Low goals conceded
- Consistent results against international opponents

---

## 3. Role of Penalty Shootouts

Knockout matches ending in draws require a penalty shootout.

The current model assumes:

```
50% chance Team A wins
50% chance Team B wins
```

This introduces randomness but simplifies real-world penalty dynamics.

---

## 4. Understanding the Underdogs

Teams such as:

- Morocco (0.51%)
- Paraguay (0.16%)

have lower championship probabilities.

This does not indicate poor team quality.

Instead, the probability reflects the difficulty of:

- Winning multiple knockout matches
- Defeating stronger opponents consecutively
- Maintaining performance throughout a tournament

---

# ⚠️ Model Limitations

Although the simulation provides useful probability estimates, several limitations exist.

---

# 1. Simplified Penalty Shootout Model

The penalty system uses a simple random 50:50 outcome.

It does not consider:

- Historical penalty shootout performance
- Player penalty conversion rates
- Goalkeeper penalty-saving ability
- Psychological factors

---

# 2. Incorrect Tournament Structure

The simulation does not fully replicate the actual **2026 FIFA World Cup format**.

Current limitations:

- Ignores the group stage
- Uses a predefined Round of 16 bracket
- Does not include the expanded 48-team structure

The real tournament includes:

- 48 teams
- Group-stage qualification
- Round of 32 knockout phase

Therefore, important factors such as:

- Fatigue
- Goal difference
- Qualification scenarios

are not captured.

---

# 3. Lack of Strength-of-Schedule Adjustment

The model calculates ratings using raw goals scored and conceded.

However, it assumes all opponents have equal difficulty.

Example:

A team scoring many goals against weaker opponents may receive an inflated attacking rating compared with a team competing against stronger regional opponents.

The model does not currently adjust for:

- Opponent quality
- Confederation strength
- Match difficulty

---

# 4. Static Ratings and Recency Bias

The model aggregates matches from 2015 onward equally.

Limitations:

- A match from 2015 has the same weight as a recent match.
- Squad changes are not considered.
- Manager changes are ignored.
- Injuries and current player form are not included.

International football changes rapidly, making static ratings less responsive to current conditions.

---

# 5. Poisson Distribution Assumption

The simulation assumes goals occur independently.

However, football matches are dynamic.

The model does not capture:

- Tactical changes after scoring
- Defensive strategies when leading
- Increased attacking risk when losing
- Momentum shifts during matches

---

# 6. Default Rating Assignment

If a team does not exist in the historical dataset, the model assigns:

```
Default Rating = 1.0
```

While this prevents calculation errors, it may distort predictions for:

- Emerging national teams
- Underrated teams
- Teams with limited historical data

---

# 📝 Final Conclusion

This project demonstrates how historical football data can be combined with statistical modeling to estimate World Cup winning probabilities.

The simulation successfully identifies traditional football powers as the strongest contenders while providing a quantitative framework for tournament prediction.

However, the model should be interpreted as a **statistical simulation rather than an exact prediction system**.

Future improvements could include:

- Elo-based team ratings
- Opponent strength adjustment
- Time-weighted performance metrics
- Player-level statistics
- Realistic penalty shootout models
- Full FIFA 2026 tournament structure simulation

By incorporating these improvements, the model could provide more accurate and realistic football forecasting.
