To investigate whether stable working groups affect the outcomes and severity of punishments in Russian courts, I conducted an empirical analysis using court decision data from 2017. The analysis involved data extraction, preprocessing, and applying machine learning models to evaluate the influence of these stable working groups.

**1. Data Collection**

I utilize the 'text' column to extract information about the judges, prosecutors, and defense attorneys involved in each case, along with the case outcomes and the severity of punishments.

The key variables in our study include:

**Independent Variable:**
  - Stable Working Groups: Identifies instances where the same judge, prosecutor, and defense attorney work together on a case.

**Dependent Variables:**
  - Judicial Outcomes: A binary variable indicating whether the defendant was found guilty or not guilty. We'll analyze if stable working groups influence the likelihood of a conviction.
  - Punishment Severity: Quantifies the severity of punishments, including prison sentence lengths, fines, or other penalties. We'll standardize these penalties by converting sentences into years or fines into monetary values adjusted for inflation.
