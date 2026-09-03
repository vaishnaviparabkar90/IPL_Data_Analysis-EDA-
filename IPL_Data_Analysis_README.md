# 🏏 IPL Data Analysis

A Python-based exploratory data analysis project using IPL match and ball-by-ball data.  
The project focuses on understanding IPL match statistics, team performance, batting, bowling, toss decisions, venues, and season-wise trends using **Pandas, NumPy and Matplotlib**.

## 📊 Dataset

The project uses two related datasets:

### 1. `matches_df` — Match-level data

Each row represents **one IPL match**.

Important columns:

| Column | Description |
|---|---|
| `id` | Unique match ID |
| `city` | City where the match was played |
| `date` | Match date |
| `player_of_match` | Player who won Player of the Match |
| `venue` | Stadium/venue |
| `neutral_venue` | Whether the match was played at a neutral venue |
| `team1` | First team |
| `team2` | Second team |
| `toss_winner` | Team that won the toss |
| `toss_decision` | Decision after toss: `bat` or `field` |
| `winner` | Match winner |
| `result` | Result type: `runs`, `wickets`, or `tie` |
| `result_margin` | Margin of victory |
| `eliminator` | Whether a Super Over/tiebreaker was used |
| `method` | Method used to determine result, e.g. D/L |
| `umpire1` | First umpire |
| `umpire2` | Second umpire |
| `season` | IPL season |

### 2. `balls_df` — Ball-by-ball data

Each row represents **one delivery** in a match.

Important columns:

| Column | Description |
|---|---|
| `id` | Match ID |
| `inning` | Innings number |
| `over` | Over number |
| `ball` | Ball number |
| `batsman` | Batsman facing the delivery |
| `non_striker` | Batsman at the other end |
| `bowler` | Bowler |
| `batsman_runs` | Runs scored by the batsman |
| `extra_runs` | Runs from extras |
| `total_runs` | Total runs from the delivery |
| `non_boundary` | Indicates whether a 4/6 was not an actual boundary |
| `is_wicket` | Whether a wicket occurred |
| `dismissal_kind` | Type of dismissal |
| `player_dismissed` | Player dismissed |
| `fielder` | Fielder involved in dismissal |
| `extras_type` | Type of extra |
| `batting_team` | Team batting |
| `bowling_team` | Team bowling |

## 🔗 Relationship Between the Datasets

The two datasets are connected using the `id` column.

- `matches_df` → one row per match
- `balls_df` → many rows per match

The `season` column is available in `matches_df`, so it can be added to ball-by-ball data using:

```python
merged_df = balls_df.merge(
    matches_df[['id', 'season']],
    on='id',
    how='left'
)
```

## 🔎 Analysis Performed

The project explores questions such as:

### Match & Season Analysis
- Runs scored per match in different seasons
- Highest team score in a single match
- Biggest win by run margin
- Toss decisions across seasons
- Whether winning the toss leads to winning the match
- Number of matches won by the chasing team

### Team Analysis
- Teams that have won the tournament
- Team with the most matches played
- Team with the most wins
- Team with the highest winning percentage
- Teams scoring 200+ most often
- Teams conceding 200+ most often
- Innings-wise comparison between teams
- Lucky venues for particular teams

### Batting Analysis
- Batsmen who faced the most balls
- Leading run-scorers
- Batsmen with the most fours
- Batsmen with the most sixes
- Highest strike rate
- Season-wise boundary counts
- Runs scored from boundaries in each season
- Boundary run contribution by season

### Bowling & Match Awards
- Leading wicket-takers
- Players with the most Player of the Match awards
- Umpires who have officiated the most matches

### Venue Analysis
- Stadium that has hosted the most matches
- Team performance across different venues

## 🧠 Key Pandas Concepts Used

- `groupby()`
- `size()`
- `sum()`
- `count()`
- `value_counts()`
- `sort_values()`
- `idxmax()`
- `unique()`
- `merge()`
- `concat()`
- `isin()`
- Boolean filtering
- `unstack()`
- `np.where()`

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook / Google Colab

## 📈 Example Analysis

### Leading Run Scorers

```python
balls_df.groupby('batsman')['batsman_runs']     .sum()     .sort_values(ascending=False)
```

### Most Successful Teams

```python
matches_df['winner'].value_counts()
```

### Most Hosted Venue

```python
matches_df['venue'].value_counts().idxmax()
```

### Season-wise Four Count

```python
merged_df[
    (merged_df['batsman_runs'] == 4) &
    (merged_df['non_boundary'] == 0)
].groupby('season').size()
```

## 🎯 Project Goals

The main goal of this project is to practice **real-world data analysis with Pandas** by answering cricket-related business-style questions from raw match and delivery data.

The analysis demonstrates how raw data can be transformed into meaningful insights using filtering, grouping, aggregation, merging, and sorting.

## 🚀 Future Improvements

- Add visualizations for major findings
- Build an interactive IPL dashboard using Power BI
- Perform deeper player and team comparisons
- Analyze season-wise batting and bowling trends
- Build predictive ML models using IPL statistics
