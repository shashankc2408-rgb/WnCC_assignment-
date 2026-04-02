# Ideation Document – Mentor Scoring System (Question 1)

## 1. Goal

The goal of this project is to evaluate how effective a mentor is during SoC.

Instead of using a single metric, I combined multiple factors like:

* student progress
* mentor responsiveness
* interaction level
* student feedback

---

## 2. Mentor Score Formula

Final score is calculated as:

M = w1 * P + w2 * R + w3 * E + w4 * F

Where:

* P = Progress Score
* R = Responsiveness Score
* E = Engagement Score
* F = Feedback Score

Weights used:

* w1 = 0.35
* w2 = 0.20
* w3 = 0.25
* w4 = 0.20

Reason:
I gave more importance to student progress because actual outcomes matter the most.

---

## 3. Progress Score (P)

Instead of using a simple ratio, I used a weighted progress system.

Idea:

* Later milestones are more important than initial ones
* So I gave slightly higher weight to later milestones

Then I averaged progress across all students under a mentor.

---

## 4. Responsiveness Score (R)

I used an exponential decay function:

R = exp(-lambda * t_avg)

Where:

* t_avg = average response time

Reason:

* Fast responses → high score
* Slow responses → score drops quickly

This keeps the value between 0 and 1.

---

## 5. Engagement Score (E)

I used:

* meetings
* code reviews
* messages

Weights used:

* meetings = 0.4
* code reviews = 0.4
* messages = 0.2

Then I normalised the score so all mentors are comparable.

Reason:
Meetings and reviews are more meaningful than just messages.

---

## 6. Feedback Score (F)

This was the most complex part.

### Step 1: Remove outliers

I used IQR method to detect very unusual ratings.

These ratings were reduced or ignored to avoid bias.

---

### Step 2: Weighted Average

More number of ratings → more reliable score

---

### Step 3: Bayesian Averaging

Used to handle mentors with very few ratings.

This prevents:

* one bad rating → very low score
* one good rating → very high score

---

### Step 4: Scaling

Final feedback score was scaled between 0 and 1.

---

## 7. Score Evolution Over Time

I used exponential smoothing:

M_new = (1 - alpha) * M_old + alpha * M_current

* alpha = 0.6

Reason:
Recent performance should matter more, but past should not be ignored.

---

## 8. Activity Decay

If a mentor becomes inactive:

M_new = M_old * (1 - d)

* d = 0.1

Reason:
Inactive mentors should slowly lose score but not immediately.

---

## 9. Normalisation

To ensure fairness:

* Engagement is divided per mentee
* Progress is ratio-based
* Feedback considers number of ratings

This avoids unfair advantage for mentors with more students.

---

## 10. Assumptions

* Data is clean and complete
* Feedback is mostly honest after removing outliers
* All interactions are meaningful

---

## 11. Possible Improvements

* Use ML model for better feedback analysis
* Dynamic weights instead of fixed ones
* Domain-based scoring (ML vs Web vs CP)

---

## Final Note

This system tries to balance different aspects of mentoring.

I focused more on logic and fairness rather than complexity, and tried to handle edge cases like biased feedback.

# Ideation Document – Tutorial Quality Scorer (Question 3)

## 1. Goal

The goal of this project is to evaluate the actual quality of coding tutorials.

Many tutorials online are clickbait (high views but low learning value).
So I tried to build a system that predicts a **quality score (1–100)** using available data.

---

## 2. Dataset

Since real data was not used, I created a synthetic dataset.

The dataset includes:

* title
* description
* duration
* views
* likes
* comments
* subscriber count
* actual quality score

While generating data, I tried to keep realistic patterns like:

* high views but low likes → low quality
* good tutorials → better engagement

---

## 3. Feature Engineering

I created some additional features to improve prediction:

### Engagement Rate

likes / views

Reason:
Good tutorials usually have higher engagement.

---

### Comment-based Signals

More comments may indicate:

* better discussion
* more usefulness

---

## 4. Model Selection

I used two models:

### 1. Linear Regression

* Simple model
* Helps understand relationship between features and quality

---

### 2. Random Forest Regressor

* More powerful model
* Handles non-linear relationships better

---

## 5. Evaluation Metrics

I used:

* R² Score → how well model explains data
* Mean Absolute Error (MAE) → average prediction error

---

## 6. Observations

* Tutorials with high views but low engagement often have low quality
* Engagement rate is an important factor
* Comments also give useful signal

---

## 7. Output

The model predicts quality score for each tutorial.

Then I sorted tutorials to get:

* top 10 best tutorials

---

## 8. Assumptions

* Synthetic data represents real-world patterns
* Engagement reflects actual usefulness

---

## 9. Possible Improvements

* Use real YouTube API data
* Use NLP on title and description
* Use advanced models like XGBoost

---

## Final Note

This project is a simple attempt to understand how tutorial quality can be estimated using data.

I focused on keeping the model simple and understandable rather than very complex.

