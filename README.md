# Social Media & Wellbeing Dashboard

An interactive Power BI dashboard exploring how digital habits relate to psychological wellbeing, built on a synthetic survey dataset of 6,827 respondents. Designed as a companion piece to a parallel Python/scikit-learn analysis (EDA + leakage-aware machine learning) of the same data.

## The dataset

6,827 synthetic survey responses covering:
- **Demographics**: age, age group, gender, occupation, region
- **Digital behavior**: screen time, platform used, daily notifications, time to first check after waking, night-time use, primary purpose of use, screen time limits, digital detox attempts
- **Psychological scores**: anxiety, low mood, life satisfaction, loneliness, self-esteem, FOMO, social comparison
- **Target variable**: `wellbeing_band` (Good / Moderate / At-risk) — a composite label derived from the psychological scores

## Dashboard structure

Three pages, each with a clear focus — *who the respondents are → what they do online → how they feel, and why*:

### 1. Overview
Who the sample is made up of. KPIs (total respondents, % Good / Moderate / At-risk), where respondents are from, most used platforms, and wellbeing distribution by age group.

### 2. Digital Behaviour
What people actually do online. KPIs on average screen time, notifications, morning check time, and sleep. Breakdown of usage purpose by age group, screen time limits and digital detox attempts, and a scatter plot of daily notifications vs. screen hours, colored by wellbeing band.

### 3. Psychological Wellness
How people feel, and how it connects to behavior. KPIs on life satisfaction, anxiety, and FOMO; an **interactive boxplot** (pick a psychological score from the dropdown — Anxiety, Low Mood, Life Satisfaction, Loneliness, or Self-Esteem — and compare its distribution across wellbeing bands); and a breakdown of who seeks mental health support, by wellbeing band.

## The story

**The expected pattern holds — and the data backs it up quantitatively.** A Random Forest model trained separately in Python (see the companion notebook) confirms what the scatter plot on page 2 suggests visually: `daily_screen_hours`, `daily_notifications`, and `avg_sleep_hours` alone account for roughly 63% of the model's predictive importance for wellbeing. Behavior, not demographics or platform choice, is what drives the signal.

**The pattern that doesn't show up in raw numbers.** Seniors are the smallest group in the sample by far (just 119 out of 6,827 respondents), and in a chart of raw counts they barely register. But looked at proportionally, Seniors have the *highest* at-risk rate of any age group — 18.5%, compared to 12–14% for every other group. It's an insight that only surfaces once you stop looking at headcounts and start looking at rates within each group.

**A quieter story about help-seeking.** 61% of respondents say they do not seek mental health support, and a further 21% say they're only considering it — regardless of which wellbeing band they fall into. This dashboard doesn't attempt to explain *why* (stigma, access, awareness are all plausible, untestable with this data), but it's a pattern worth sitting with rather than glossing over.

## Methodology note

`wellbeing_band` is very likely a composite constructed from the five psychological scores themselves — the boxplots in this dashboard confirm it, with near-complete separation between bands on each score. For that reason, the companion Python analysis deliberately **excludes** those psychological scores when training predictive models, keeping only behavioral and demographic variables. The "what drives wellbeing" insight above comes from that leakage-free ("honest") model, not from a model that could trivially decode the label from its own ingredients.

The dataset is synthetic. The patterns here demonstrate a workflow — EDA, dashboard design, leakage-aware modeling — rather than real-world claims about social media and mental health.

## Tools

- **Power BI**: data modeling, DAX measures, field-parameter-driven interactive boxplot
- **Python** (pandas, scikit-learn): EDA, preprocessing, Logistic Regression / Random Forest comparison, permutation importance

## Author

Fortuna
