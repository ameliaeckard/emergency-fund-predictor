# Predicting Emergency Fund Coverage: Machine Learning Analysis of Financial Fragility

**Author:** Amelia Eckard
**Course:** ITCS 3156 - UNC Charlotte

## Project Overview

This project uses machine learning to predict which Americans can cover a $400 emergency expense with cash or savings. Using data from the Federal Reserve's 2024 Survey of Household Economics and Decisionmaking (SHED), combined with state-level economic indicators, we identify the demographic and economic factors that predict financial fragility.

**Key Findings:**
- Random Forest achieved 59.5% accuracy with 0.512 F1 score
- Only 43.7% of Americans can cover $400 with cash/savings (true financial security)
- 56.3% cannot cover from liquid assets - must use debt, borrow, or cannot pay
- EF1 (3-month emergency fund), age (ppage), and income (ppinc7) are strongest predictors
- Household size (pphhsize) negatively predicts ability to save

## Problem Statement

**56.3% of Americans cannot cover a $400 emergency expense with cash or savings.** This project uses machine learning to predict who faces this financial fragility and why, revealing the invisible barriers that prevent people from achieving financial security.

## Dataset

### Primary Data Sources

1. **SHED 2024 (Survey of Household Economics and Decisionmaking)**
   - Source: Federal Reserve Board
   - Samples: 12,295 U.S. adults
   - Features: Demographics, income, emergency fund access
   - Target: EF3_c - "Can cover $400 with cash/savings/checking"
   - Link: https://www.federalreserve.gov/consumerscommunities/shed.htm

2. **Regional Price Parities 2023**
   - Source: Bureau of Economic Analysis
   - Samples: 51 states (50 states + DC)
   - Features: Real income, personal consumption expenditures, cost of living adjustments
   - Link: https://www.bea.gov/data/prices-inflation/regional-price-parities-state-and-metro-area

3. **State Minimum Wage Data**
   - Source: Federal Reserve Economic Data (FRED)
   - Note: Limited coverage (11 states with distinct minimums reported)

### Features Used (11 total)

**Demographics:**
- `ppage`: Age (years)
- `pphhsize`: Household size (number of people)
- `ppkid017`: Number of children under 18
- `ppeducat`: Education level (1=No HS, 2=HS, 3=Some college, 4=Bachelor's+)
- `ppethm`: Race/ethnicity (1=White NH, 2=Black NH, 3=Other NH, 4=Hispanic, 5=2+ Races NH)
- `ppgender`: Gender (1=Male, 2=Female)
- `ppinc7`: Household income (1=<$10k to 7=$150k+)

**Financial:**
- `EF1`: Has 3-month emergency fund (0=No, 1=Yes)

**State Economic Indicators:**
- `pce_pct_change`: Personal consumption expenditure % change (2022-2023)
- `income_pct_change`: Real income % change (2022-2023)
- `real_income_2023`: State real income adjusted for cost of living

## Target Variable

**can_cover_400** (Binary: 0 or 1)
- **1 = Can cover**: Respondent answered "Yes" to EF3_c - can pay with cash/savings/checking account
- **0 = Cannot cover**: Respondent answered "No" to EF3_c - cannot pay with liquid assets

This definition represents true financial security - having liquid assets available to cover unexpected expenses without going into debt.

**Distribution:**
- Can cover: 5,368 (43.7%)
- Cannot cover: 6,927 (56.3%)

## Methodology

### Machine Learning Algorithms

Three algorithms were selected to compare linear vs. non-linear approaches:

1. **Logistic Regression**
   - Baseline linear model for interpretability
   - Best generalization: No overfitting (learning curves converge)
   - Accuracy: 58.0% | F1: 0.512 | ROC-AUC: 0.639

2. **Random Forest**
   - Ensemble method to capture non-linear relationships
   - Best overall performance across metrics
   - Accuracy: 59.9% | F1: 0.512 | ROC-AUC: 0.639

3. **Gradient Boosting**
   - Sequential ensemble for complex pattern recognition
   - Competitive performance with Random Forest
   - Accuracy: 58.8% | F1: 0.493 | ROC-AUC: Not available

### Key Findings from Analysis

**Feature Importance Consensus (All 3 Models):**
1. **EF1** (3-month emergency fund): 0.26 average importance - strongest predictor
2. **ppage** (Age): 0.18 - older adults more likely to have savings
3. **ppinc7** (Income): 0.13 - higher income enables savings
4. **real_income_2023**: 0.09 - state-level purchasing power matters
5. **ppkid017** (Children): 0.07 - more children reduces savings capacity

**Learning Curve Insights:**
- Logistic Regression: Healthy convergence (no overfitting), reaches ceiling at ~2,000 samples
- Random Forest & Gradient Boosting: Severe overfitting (training F1 ~0.95, validation F1 ~0.52)
- Performance plateau suggests current features capture most learnable patterns
- Further improvement requires new features or external data

**Error Analysis:**
- False Positives (456): Model overestimates ability - predicted CAN cover but actually CANNOT
  - Tend to have moderate income/education but hidden expenses
- False Negatives (538): Model underestimates ability - predicted CANNOT but actually CAN
  - Likely have disciplined savings habits despite lower demographics

### Dependencies
- Python 3.8+
- pandas 2.0.3
- numpy 1.24.3
- scikit-learn 1.3.0
- matplotlib 3.7.2
- seaborn 0.12.2
- shap 0.42.1
- openpyxl 3.1.2

## Key Insights

### What Predicts Financial Security?

**Positive Predictors (help you save):**
- Having a 3-month emergency fund already (EF1)
- Older age (more time to accumulate wealth)
- Higher income and education
- Living in states with higher real income

**Negative Predictors (prevent saving):**
- Larger household size (resources spread thin)
- Having children under 18 (childcare costs)
- Lower income/education levels
- Living in high cost-of-living states without income adjustment

### The Cash/Savings Distinction Matters

- **91% could cover $400** through *some* method (credit cards, loans, borrowing, selling items)
- **Only 44% have liquid cash** available - true financial security
- **56% would go into debt** or cannot pay at all


## Limitations and Future Work

**Current Limitations:**
- Model plateau at ~60% accuracy suggests feature ceiling
- Tree models overfit despite regularization attempts
- State-level economic data doesn't capture individual variation
- Missing minimum wage data for 40 states

**Future Improvements:**
- Add individual-level income (not just categorical)
- Include debt-to-income ratios
- Incorporate housing costs relative to income
- Time-series analysis (track same individuals over years)
- Deep learning approaches for complex interactions
- Collect complete state minimum wage data

## Acknowledgments

**AI Assistance:**
- Claude (Anthropic) was used for:
  - Debugging preprocessing pipeline (categorical encoding, state mapping)
  - Troubleshooting SHAP analysis implementation

**Online Resources:**
- scikit-learn documentation for model implementation
- SHAP library documentation for interpretability analysis
- SHED 2024 codebook for feature definitions
- Stack Overflow for specific error resolutions

## License

This project is for educational purposes. Data sources are publicly available from federal government agencies.
