# IG-ads
Analyze the IG ad with the largest expected profit per impression / per user, provided the uplift relative to the runner-up and to control is meaningful (practically relevant) and statistically credible.

Ad B produced the highest conversion rate and profit per user.
After subtracting the $0.20 ad cost, Ad B’s expected profit per user exceeded Control by $0.03 (95 % CI [0.02, 0.04]).
Ads A and C showed smaller or insignificant uplifts.
Therefore, Ad B is recommended for deployment going forward.

## Project Overview

Oz Collectibles ran an A/B/C advertising experiment on Instagram to evaluate which advertisement yields the highest return on investment.  
A total of **100,000 randomly assigned users** were exposed to one of four conditions:

| Condition | Description | Sample Size |
|------------|--------------|-------------|
| Control | No ad exposure | 25,000 |
| Ad A | Instagram Ad A | 25,000 |
| Ad B | Instagram Ad B | 25,000 |
| Ad C | Instagram Ad C | 25,000 |

For each user, two key outcomes were tracked:

- **Conversion** – whether a user made a purchase (binary 0/1)  
- **Revenue** – purchase amount less non-advertising costs  

Each impression cost **\$0.20**.

The goal was to:
1. Identify which ad (if any) should be used going forward.  
2. Evaluate whether a **multi-armed bandit** (MAB) approach could have improved learning efficiency and profitability.

---

## Key Questions

1. **Which ad delivers the highest profit per user?**  
   - Compare conversion rates, average revenue, and expected profit (`Revenue – $0.20`).

2. **Would a multi-armed bandit have performed better?**  
   - Estimate potential reduction in sample size and lost conversions under a smarter allocation strategy.

---

## Analytical Approach

### 1️⃣ Data Preparation
- Load `IGAds.RData` and verify variable structure.  
- Clean and recode variables for `Condition`, `Conversion`, and `Revenue`.  
- Create a derived metric:  
  ```r
  expected_profit_per_user = mean(Revenue) - 0.20

To assess potential efficiency gains, a Thompson Sampling simulation was implemented using observed arm reward distributions.

Simulation setup:

Reward = Revenue – $0.20

4 arms: Control, A, B, C

100 000 total impressions

Normal reward model with empirical means and variances

200 Monte Carlo runs

Metrics:

Average impressions (pulls) per arm under bandit vs. uniform design

Total cumulative reward and regret (difference from oracle and uniform)

Estimate of sample size reduction for equivalent learning
