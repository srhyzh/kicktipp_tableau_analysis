# Kicktipp Tableau Analysis 

A Tableau portfolio project exploring football prediction behavior using data from a private Kicktipp prediction group.

The project goes beyond the traditional leaderboard and investigates questions such as:

* How accurate are individual predictors?
* Is the **wisdom of the crowd** better than the average individual prediction?
* Which matches were the hardest to predict?
* Are predictors biased toward home wins or draws?
* Who is consistently good, rather than occasionally lucky?
* How do the strongest predictors compare over time?

> **Status:**  Work in Progress
> Dashboard 1 and Dashboard 2 are complete. Dashboard 3 is currently planned.

---

## Dataset

The current dataset contains the first **9 rounds** of the competition.

| Metric                | Value |
| --------------------- | ----: |
| Rounds                |     9 |
| Matches               |    54 |
| Participants          |    71 |
| Prediction records    | 3,834 |
| Submitted predictions | 3,752 |

The data is structured in long format, with one row representing one participant's prediction for one match.

This makes it possible to analyze the data at multiple levels, including:

**Match → Round → Participant → Prediction**

---

# Dashboard 1 — Prediction Overview

The first dashboard focuses on the overall prediction behavior of the group.

![Dashboard 1](images/dashboard_01_prediction_overview.png)

### Key questions

**How accurate is the group overall?**

The dashboard compares prediction accuracy across rounds and distinguishes between different types of successful predictions.

**What outcomes do people predict?**

The distribution of predicted outcomes is compared directly with the actual match results.

One interesting pattern in the first nine rounds is a clear **home-win prediction bias**:

| Outcome  | Predictions | Actual Results |
| -------- | ----------: | -------------: |
| Home Win |       57.7% |          38.9% |
| Draw     |       12.2% |          18.5% |
| Away Win |       30.0% |          42.6% |

Predictors therefore selected home wins considerably more often than they actually occurred.

### Current KPIs

* **49.0%** outcome accuracy
* **7.6%** exact score rate
* **97.9%** prediction submission rate

The dashboard also shows how prediction accuracy changed across the nine rounds.

---

# Dashboard 2 — The Tippers

The second dashboard shifts the focus from matches to the individual predictors.

![Dashboard 2](images/dashboard_02_the_tippers.png)

The goal is not only to identify who collected the most points, but to understand **how different predictors perform**.

### Tipper Performance Map

Participants are positioned according to:

**X-axis:** Outcome Accuracy
**Y-axis:** Exact Score Rate

This separates predictors who frequently identify the correct match outcome from those who are particularly successful at predicting exact scores.

A selected participant is highlighted while the other participants remain visible as context.

---

### Performance vs. Consistency

A second scatter plot compares:

**X-axis:** Average Points per Round
**Y-axis:** Standard Deviation of Round Points

This makes an important distinction:

A predictor can be highly consistent without necessarily being highly successful.

The most interesting area is therefore the combination of:

> **High average performance + low variation**

---

### Interactive Tipper Selection

A participant can be selected either through a dropdown or directly from the visualizations.

The selection dynamically updates:

* Total points
* Outcome accuracy
* Exact score rate
* Average points per round
* Highlighting in both scatter plots
* Rank development

---

### Rank Development

The dashboard also tracks the selected participant's ranking across rounds.

For additional context, the rank trajectories of the **current Top 5 predictors** are shown in the background.

This makes it possible to see whether a participant:

* started strongly and declined,
* gradually moved up the ranking,
* remained consistently near the top,
* or experienced large ranking swings.

---

# Dashboard 3 — Prediction Psychology 🚧

The third dashboard is planned as a deeper analysis of collective prediction behavior.

Potential topics include:

**Crowd Prediction**
What outcome did the majority of participants predict, and how accurate was the crowd?

**Crowd Confidence**
Does a stronger consensus actually lead to higher prediction accuracy?

**Match Difficulty**
Which matches produced the lowest average points and lowest prediction accuracy?

**Surprise Index**
Which results contradicted the largest share of predictions?

**Home Bias**
How strongly does the group overestimate home teams?

**Draw Bias**
Are draws systematically underpredicted?

**Scoreline Bias**
Which scorelines are predicted disproportionately often?

**Contrarian Skill**
Which participants perform particularly well when predicting against the majority?

---

# Tableau Concepts Practiced

This project is also intended as a structured Tableau learning exercise.

Techniques used include:

* Calculated Fields
* Table Calculations
* FIXED Level of Detail Expressions
* Parameters
* Parameter Actions
* Dashboard Filter Actions
* Dual-Axis visualizations
* Reference Lines
* Dynamic highlighting
* Interactive dashboards
* Scatter plots
* Ranking and longitudinal analysis
* Dashboard layout and formatting

---

# Example Calculations

### Outcome Accuracy

```tableau
SUM(
    IF [Tip Submitted]
       AND [Correct Outcome]
    THEN 1
    ELSE 0
    END
)
/
SUM(
    IF [Tip Submitted]
    THEN 1
    ELSE 0
    END
)
```

### Exact Score Rate

```tableau
SUM(
    IF [Tip Submitted]
       AND [Exact Score]
    THEN 1
    ELSE 0
    END
)
/
SUM(
    IF [Tip Submitted]
    THEN 1
    ELSE 0
    END
)
```

### Round Performance

```tableau
SUM([Points])
/
COUNTD([Round])
```

### Participant-Round Points

```tableau
{ FIXED [Participant], [Round] :
    MIN([Round Points])
}
```

This field is used as the basis for measuring consistency across rounds.

---

# Project Roadmap

✅ Data preparation
✅ Prediction Overview dashboard
✅ Tipper Performance dashboard
🚧 Crowd & Bias analysis
⬜ Final dashboard refinement
⬜ Final Tableau Public version
⬜ Final project write-up

---

# Tools

**Tableau** — visualization and dashboard development
**Microsoft Excel** — source data and validation
**GitHub** — project documentation and version tracking

---

## About this project

This project was created as a hands-on Tableau learning exercise using real football prediction data.

Rather than focusing only on leaderboard results, the objective is to explore the **behavior, accuracy, consistency, and collective intelligence of football predictors**.

The project will be expanded as additional match rounds become available.
