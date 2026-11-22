# Predicting Term Deposit Subscriptions: Bank Telemarketing Analysis

A project featuring exploratory data analysis (EDA) and logistic regression modelling to help a Portuguese bank target its telemarketing campaigns more efficiently.

**Languages & Libraries:** Python, pandas, matplotlib, seaborn, scikit-learn, imbalanced-learn (SMOTE)

## Business Problem

A Portuguese bank ran a telemarketing campaign to convince clients to open a new, long-term deposit account. Calling every client is consumes costs in resource effort, for little gain as only a small number of customers say yes. The goal of this project was to:

1. Identify which client and campaign characteristics are associated with a "yes".
2. Build a model that predicts which clients are likely to subscribe, so future campaigns can prioritise the right people.

## Data

- **Source:** Bank Marketing dataset (Moro, Cortez and Rita, 2014), UCI Machine Learning Repository
- **Size:** 4,100 observations, 20 variables, collected from 2008 to 2013
- **Variables:** client demographics, financial status, campaign contact details, previous campaign outcome, and macroeconomic indicators
- **Target:** whether the client subscribed (`yes` = 451, 11%; `no` = 3,649, 89%), a significant class imbalance

## Approach

**1. Exploratory data analysis**
- Profiled numeric and categorical variables, including a custom `quick_summary()` function for categoricals
- Quantified unknown values (`default` had the most, at 799)
- Plotted univariate distributions and handled outliers (e.g. ages over 65, `pdays` = 999 meaning "not previously contacted")
- Wrote a reusable `plot_conversion_rate()` function for bivariate analysis
- Built a correlation matrix, which showed strong multicollinearity between `euribor3m`, `nr.employed` and `emp.var.rate`

**2. Modelling**
- Dummy-encoded categorical variables (`drop_first=True`) and used a stratified train/test split
- Compared two imbalance strategies: `class_weight` (recall 0.86) vs SMOTE (recall 0.57), and chose `class_weight`
- **Model 1:** logistic regression using all variables
- **Model 2:** reduced model dropping `duration`, `nr.employed`, `emp.var.rate`, `poutcome`, `default` and `day_of_week`

**3. Evaluation**
- F1, recall, confusion matrices, and ROC/AUC

## Key Findings

| Factor | Insight |
|---|---|
| **Contact method** | Clients contacted on a mobile (cellular) phone converted at a clearly higher rate than those contacted by landline/telephone |
| **Timing** | Conversion was highest in December, March, September and October. May had the most calls but one of the lowest conversion rates |
| **Previous campaign** | Clients who had subscribed in a previous campaign were far more likely to subscribe again (conversion above 60%) |
| **Economy** | More clients subscribed when interest rates were lower, consistent with research on household saving behaviour |
| **Day of week / default status** | Little variation, so unlikely to be useful predictors |

## Model Results

Metrics below are for the positive class ("yes") on the test set.

| Model | Recall | F1 | AUC |
|---|---|---|---|
| Model 1: all variables | 0.86 | 0.61 | 0.932 |
| Model 2: reduced variables | 0.60 | 0.43 | 0.752 |

Model 1 performs best on paper, but **it cannot not be trusted as is**. It uses `duration` (length of the call), which is only known *after* the call takes place. That is data leakage and inflates its scores, so it could not be used to decide who to call in the first place. Model 2 is a more realistic, though weaker, picture of what can be predicted in advance.

## Business Recommendations

1. **Prioritise mobile contacts.** Mobile calls convert at a much higher rate than landline calls, likely because most clients are employed and unlikely to answer a home phone during the day.
2. **Concentrate calling in high-converting months** such as March and October (September and December also converted well). Review May, where large call volumes produced low conversion.
3. **Target previous subscribers first.** Clients with a successful previous campaign outcome are the warmest leads.
4. **Factor in the economic climate.** Subscription likelihood rises when interest rates are low, so campaign timing and budget can be tied to market conditions.
5. **Do not use call duration to select leads.** It is only known after the fact. The production model must use pre-call information only.

These insights are valuable regardless of model performance, and can save the bank time and money by focusing effort where it is most likely to pay off.

## Limitations and Next Steps

- **Data leakage:** Model 1 relies on `duration`. A model that removes only `duration` and keeps the other predictors would likely perform better than Model 2 without leakage.
- **Time period:** Data spans the global financial crisis and its aftermath, so patterns learned from 2008 - 2013 may not hold in 2026.
- **Non-linear relationships:** A tree-based classifier such as Random Forest could capture interactions that logistic regression cannot.
- **Class imbalance:** Precision for the "yes" class remains modest, meaning many contacted clients would still not convert.

## References

- Moro, S., Cortez, P. and Rita, P. (2014) *Bank Marketing*. UCI Machine Learning Repository. https://doi.org/10.24432/C5K306
- Staal, K. (2023) 'Household Savings and Negative Interest Rates', *International Advances in Economic Research*, 29(1), pp. 1-13.
- Bouke, M.A., Zaid, S.A. and Abdullah, A. (2024) 'Implications of data leakage in machine learning preprocessing: a multi-domain investigation'.
