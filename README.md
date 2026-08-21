# Credit Default Risk Prediction

Predicting the probability that a borrower will experience serious financial 
delinquency within two years, using the "Give Me Some Credit" dataset (2011 
Kaggle competition, 150,000 anonymized borrowers).

## Overview

The data comes from ["Give Me Some Credit"](https://www.kaggle.com/c/GiveMeSomeCredit), 
a 2011 Kaggle competition built around a real, practical problem: banks need 
to estimate the probability that a borrower will default before extending 
credit, and better models mean fewer bad loans without unnecessarily 
rejecting good borrowers. The dataset contains historical data on 150,000 
borrowers, covering their credit card and line of credit usage, mortgage 
and real estate loans, and payment history. These are a realistic 
cross section of the kind of data a bank's risk team would actually work 
with.

Credit risk models like this one are used to assign each borrower a 
predicted probability of default, rather than a simple yes or no decision. 
That probability feeds into decisions banks make daily: whether to approve 
a loan, what interest rate to offer, and how much capital to hold in 
reserve against potential losses. Despite being over a decade old, this 
dataset remains a widely used benchmark for practicing and evaluating 
credit scoring techniques.

## Approach

Real world credit data is rarely clean. This dataset included invalid 
values, extreme outliers, and dataset specific quirks that had to be 
investigated and understood before they could be modeled, since getting 
this right mattered as much as any later modeling choice. The steps below 
trace that process so far, from the raw data to a fully cleaned dataset:

**1. Data Loading and Initial Exploration**
Loaded 150,000 anonymized borrower records and examined the dataset's 
structure, confirming its size and checking each column for missing values 
and correct data types.

**2. Identifying Data Quality Issues**
Found two columns with significant missing data, MonthlyIncome (around 20% 
missing) and NumberOfDependents (around 2.6% missing), to be addressed 
during cleaning.

**3. Target Variable Analysis**
Confirmed a severe class imbalance in the target variable (93.3% non 
default versus 6.7% default), establishing early on that accuracy would be 
a misleading metric and that class imbalance would need explicit handling 
during modeling.

**4. Outlier Investigation**
Used summary statistics and histograms to identify implausible values, 
including an age of 0, a credit utilization ratio as high as 50,708 (should 
realistically be 0 to 2), and a DebtRatio max of 329,664. Investigating 
further showed that most extreme DebtRatio values coincided with missing 
income data, and that a cluster of values in the past due payment columns 
(96 and 98) were dataset specific placeholder codes rather than genuine 
counts.

**5. Data Cleaning**
Rather than deleting problematic rows outright, extreme values were capped 
and flagged to preserve information: the single invalid age of 0 was 
removed, missing income and dependents were imputed with median and mode 
values (with flag columns marking originally missing data), and extreme 
DebtRatio, credit utilization, and sentinel past due values were capped at 
realistic thresholds.

## Status

Feature engineering and modeling are still in progress.
