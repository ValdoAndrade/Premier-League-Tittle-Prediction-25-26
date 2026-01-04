# Premier-League-Tittle-Prediction-25-26 (Python)
A Data-Driven Approach Using xG and Match Simulation to predict the Premier League winner

## Project Objective 🎯
This project evaluate team strenght and performance-based metrics to predict the Premier League tiltle winner among Arsenal, Manchester City and Aston Vills. This project consist in predicting the reamining match fixtures only for these 3 tittle contenders.


## Data Section (Data Sources) 📊
 https://fbref.com/en/ and
 https://www.premierleague.com/en

The perfomance based metrics for all premier league teams including average points per game, expected goals (xG), expected goals against (xGA), and goals scored/conceded per game was collected from fbref. Furthermore, the remaining match fixtures was collected from the premier league official website. 

![Team Metrics]


<img width="1052" height="592" alt="image" src="https://github.com/user-attachments/assets/3b077586-8306-4664-8ac6-ea2343c20b02" />



![Fixtures]

<img width="531" height="678" alt="image" src="https://github.com/user-attachments/assets/3b1b7ac9-00aa-4908-ba70-744f84d2bf4d" />


## Tools Used

Excel for initial data prep

Python (Google colab) for the prediction, cleaning and analysis

## Methodology Overview

- Team strength is calculated using a weighted composite score:
  - 45% Expected Goals Difference (xG − xGA)
  - 40% Points Per Game
  - 15% Goal Difference Per Game

```python
teams["strength"] = (
    0.45 * teams["xg_diff_pg_z"] +
    0.40 * teams["ppg_z"] +
    0.15 * teams["gd_pg_z"]
)
```

    
- All metrics are standardised using z-scores.
- Match outcomes are predicted deterministically using team strength differences.
- A home advantage factor of 0.25 is applied to the home team’s strength.
  

```python
THRESHOLD = 0.25
HOME_ADV = 0.25

def predict_result(home_team, away_team):
    diff = (strength_map[home_team] + HOME_ADV) - strength_map[away_team]
    if diff > THRESHOLD:
        return "H"
    elif diff < -THRESHOLD:
        return "A"
    else:
        return "D"
```

  
- Points are assigned using official Premier League rules (3–1–0).
- Predicted points from remaining fixtures are added to current league points to project final standings.


## Insights 

The results reflects strong performance by Aston Villa against mid-table teams but an inability to consistently match the top two across high-difficulty fixtures.
Both Arsenal and Manchester City win the majority of their remaining fixtures in the deterministic model, and they demonstrated their dominance at home and away games.
 Manchester City ranked slightly higher in team strength due to superior underlying xG metrics reaching a team strenght of 1.96.
 Arsenal team strenght is 1.76 and Aston Villa is 0.31. Aston Villa registered a low team srtrenght mainly because of their start of the season as they they did not win a single game in the first 5 games and scored only 1 goal.
 Despite being one of the top 3 teams Aston Villa based on te performance metrics from this model they rank 7th in terms of team strenght across the league, which highlights the amazing season they are doing and that the team overachieved.
 Arsenal win the premier legue with 99 final points, following Manchster City with 98 and Aston Villa reached 79 points.
 Manchester City won the match against Arsenal at home.



<img width="582" height="160" alt="image" src="https://github.com/user-attachments/assets/b1424c8b-ebf1-4c5c-a842-910dd97381b0" />




<img width="751" height="621" alt="image" src="https://github.com/user-attachments/assets/65d4f365-02f2-438c-b9b1-e7ca8cd4aa4e" />





<img width="843" height="607" alt="image" src="https://github.com/user-attachments/assets/4a4b3d5c-db14-4ad3-aa2d-acdf18e8d922" />





## Final standings (Top 3)

<img width="330" height="172" alt="image" src="https://github.com/user-attachments/assets/46675194-9a1f-4e73-9516-ae03edf2a938" />


### Limitations 

-Team strength assumed to be constant over remaining fixtures.

-Injuries, suspensions, tactical matchups and recent forms are not modelled.

-Deterministic model does not capture randomness.

-The model predicts match outcomes (win, draw, loss) but does not predict scorelines or goal counts. As a result, it does not capture the magnitude of wins or losses,
which can impact goal difference, relevant stats and the perceived dominance of teams.



## Conclusion

Based on predicted points from remaining fixtures, Arsenal emerged as the most likely title winner among the three contenders. Arsenal and Manchester City demonstrated great dominance in their final fixtures as they won a significant amount of games.On the other hand, Aston Villa revealed more struggles in their fixtures as they registered losses and several draws. Consequently Aston Villa finished the league in the third position.

## How to use 
1. Start with the README
   Read THE README to understand the project.
   
   2.Go to  see the Python script used to do the predictions.
   3. Review the findings
   Check the Insights sections in this README for a summary of key observations.
