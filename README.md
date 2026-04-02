# Mentor Scoring System (WnCC Assignment - Question 1)

## About this project

In this project, I created a system to score mentors based on how they guide students during SoC.

The idea is to combine different factors like:

* how much students progressed
* how fast mentor replies
* how much interaction happens
* feedback given by students

All these are combined to give a final score and ranking.

---

## Files used

The code uses 3 CSV files from the datasets folder:

* mentors.csv
* students.csv
* interactions.csv

---

## How to run

1. Open the notebook:
   mentor_scoring_que1.ipynb

2. Run all cells

3. Output file will be created:
   mentor_scores.csv

---

## Output

The output file contains:

* Rank
* MentorID
* Name
* Domain
* ProgressScore
* ResponsivenessScore
* EngagementScore
* FeedbackScore
* FinalScore_M

Mentors are sorted from highest score to lowest.

---

## How I calculated scores

### 1. Progress Score (P)

I used a weighted progress system.

Instead of simple ratio, I gave more importance to later milestones using a formula.

Then I averaged this for each mentor.

---

### 2. Responsiveness Score (R)

I used an exponential function:

R = exp(-lambda * avg_response_time)

* Faster response → higher score
* Slow response → quickly reduced score

---

### 3. Engagement Score (E)

I combined:

* meetings
* code reviews
* messages

with weights:

* meetings = 0.4
* code reviews = 0.4
* messages = 0.2

Then I normalised the score between 0 and 1.

---

### 4. Feedback Score (F)

This part has multiple steps:

1. I first removed outliers using IQR method
   (very unusual ratings get less weight)

2. Then I calculated weighted average feedback

3. Then I applied Bayesian averaging:

   * to handle mentors with very few ratings

4. Finally scaled score between 0 and 1

---

## Final Score

Final score is calculated as:

M = w1*P + w2*R + w3*E + w4*F

Where:

* w1 = 0.35
* w2 = 0.20
* w3 = 0.25
* w4 = 0.20

---

## Extra Features

### Score Update Over Time

I used smoothing:

new_score = (1 - alpha)*old + alpha*current

---

### Activity Decay

If mentor is inactive:

new_score = old_score * (1 - decay_rate)

---

## Assumptions

* Data is clean and correct
* Feedback is mostly honest (after removing outliers)
* All interactions are meaningful

---

## Note

This is my first time building a system like this.
I tried to follow logic and improve where possible, especially in feedback handling.

There can be improvements, but I focused on making a clear and working model.

# Tutorial Quality Scorer (WnCC Assignment - Question 3)

## About this project

In this project, I tried to build a system that can judge the quality of coding tutorials.

There are many tutorials online which look attractive but are not actually useful.
So the goal was to predict a **quality score (1–100)** based on different features.

---

## Dataset

I used a CSV file:

* datasets/tutorials.csv

It contains:

* title
* description
* duration
* views
* likes
* comments
* subscriber count
* actual quality score

---

## How to run

1. Open the notebook:
   tutorial_quality_score.ipynb

2. Run all cells

3. Output file generated:
   tutorial_scores.csv

---

## What I did

### 1. Feature Engineering

I created some extra features like:

* engagement rate (likes / views)
* comments related features

These help in better prediction.

---

### 2. Model Used

I used:

* Linear Regression
* Random Forest Regressor

Then I compared their performance.

---

### 3. Evaluation

I used:

* R² score
* Mean Absolute Error (MAE)

to check how good the model is.

---

### 4. Final Output

The model predicts quality score for each tutorial.

Also, I sorted tutorials to get:

* top 10 best tutorials

---

## Observations

* Tutorials with high views but low engagement often have low quality
* Good tutorials usually have better like-to-view ratio
* Comments also help indicate usefulness

---

## Assumptions

* Data is synthetic but follows realistic patterns
* Engagement reflects actual usefulness

---

## Note

This is my first time working on a regression problem like this.
I tried to keep the model simple and understandable.

There is scope for improvement using better models or real data.
