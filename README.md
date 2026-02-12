# DDS-8555-ChandlerJ-Regression-Analysis

## Methodology
- OLS Baseline: An Ordinary Least Squares model was established but showed signs of severe multicollinearity (Condition Number: 153) and heteroscedasticity.
- Ridge Regularization: To address these diagnostic issues, a Ridge regression model was implemented based on the theoretical frameworks of Hoerl and Kennard (1970) and Friedman et al. (2010).
- Elastic Net Regression (Assignment 3): Implemented to combine L1 and L2 regularization, enabling both coefficient shrinkage and feature selection under strong predictor correlation. Hyperparameters (α and l1_ratio) were selected via cross-validation.
- Principal Components Regression (PCR) (Assignment 3): Applied PCA prior to regression to eliminate multicollinearity through orthogonal transformation. The optimal number of principal components was selected using 5-fold cross-validated RMSE.

## Key Results
- Ridge R-squared: 0.6010.
- RMSE: 2.0245.
- Primary Predictors: Shell weight and Height were identified as the most significant biological indicators of age.
- Elastic Net Validation RMSE: 2.0248
    - Selected an L1-dominant solution (l1_ratio ≈ 1.0), effectively behaving similarly to Lasso.
    - Strongest predictors included Whole weight.1, Shell weight, Whole weight, and Height.
- PCR Validation RMSE: 2.0237
    - Slightly outperformed Elastic Net on validation data.
    - Demonstrated comparable predictive performance while fully eliminating multicollinearity.

# Multiple Linear Regression Analysis: From Theoretical Foundations to Applied Regularization in Biological Data

## Executive Summary
This report evaluates multiple linear regression applications ranging
from theoretical intercept adjustments to high-dimensional biological
data prediction. By analyzing the Carseats and Abalone datasets, this
work explores the balance between model complexity and
statistical stability. Initial findings highlighted the necessity of
diagnostic-driven modeling, where the identification of non-normal
residuals and severe multicollinearity informed a transition from
standard Ordinary Least Squares (OLS) to penalized regression
techniques. The following insights summarize the quantitative results
and the theoretical justifications for the chosen methodologies.

## Key Insights
-   Model Parsimony: In the Carseats analysis, removing the
    insignificant Urban predictor improved the Adjusted $R^2$
    ($0.234 \rightarrow 0.235$), demonstrating that a simpler model can
    be more effective.
-   Multicollinearity Impact: The Abalone dataset exhibited a high
    Condition Number (153), indicating severe multicollinearity among
    physical measurements that destabilized OLS estimates.
-   Regularization Benefits: Ridge Regression successfully addressed
    predictor instability by constraining coefficient magnitudes,
    providing a more theoretically sound model for biological data.
-   Diagnostic Rigor: While OLS achieved a slightly higher $R^2$ (0.607)
    than Ridge (0.601), the presence of heteroscedasticity and
    non-normal residuals in the OLS model necessitated the move toward
    regularization to ensure better generalization.

The progression from textbook examples to the Kaggle competition
reinforces that predictive power cannot be assessed by $R^2$ alone. In
the Carseats model, refining the feature set ensured that every
predictor contributed significantly to the outcome. In the more complex
Abalone analysis, the identification of a Condition Number of 153 served
as a primary indicator for potential coefficient inflation. By
implementing Ridge regression, the model achieved a balance between bias
and variance, addressing the non-orthogonal nature of the physical
measurements. Ultimately, these analyses demonstrate that rigorous
assumption testing and the application of regularization are essential for building robust models.

# Dimensionality Reduction and Regularization in High-Collinearity Regression: A Kaggle Abalone Case Study

## Executive Summary

This analysis evaluated predictive modeling strategies for estimating abalone age (Rings) using morphometric measurements from the Kaggle Abalone regression dataset. Exploratory analysis identified substantial multicollinearity among size and weight-based predictors, with correlations frequently exceeding 0.90. Because high collinearity can inflate variance and destabilize ordinary least squares (OLS) estimates, two variance-control approaches were implemented and compared: Elastic Net regularized regression and Principal Components Regression (PCR). Model performance was evaluated using cross-validated root mean squared error (RMSE).

Both dimensionality-control strategies produced nearly identical validation performance, with Elastic Net yielding a validation RMSE of approximately 2.025 and PCR yielding a validation RMSE of approximately 2.024. The similarity in predictive accuracy suggests that multicollinearity was successfully mitigated in both approaches, though each method achieves stability through a different mechanism: coefficient shrinkage versus orthogonal transformation.

## Key Insights

- Multicollinearity was structurally significant, particularly among shell length, diameter, and weight measurements, justifying the use of shrinkage or dimensionality reduction methods.
- Elastic Net effectively prioritized weight-based predictors, shrinking less informative variables (e.g., Length and Sex_M) toward zero while stabilizing coefficient estimates.
- PCR eliminated collinearity entirely by projecting predictors onto orthogonal components, achieving slightly lower validation RMSE while sacrificing direct interpretability of individual coefficients.
- Predictive performance between methods was statistically similar, indicating that model stability—not model complexity—was the primary determinant of generalization performance.

Overall, the results demonstrate that when predictor correlation is high, regularization or dimensionality reduction materially improves model stability without sacrificing predictive accuracy. For applied deployment, Elastic Net offers greater interpretability and feature-level insight, whereas PCR provides a structurally robust alternative when predictor interdependence is extreme. Both approaches substantially outperform naive OLS baselines in terms of variance control and generalization reliability.

# Repository Structure
```
DDS-8555-ChandlerJ-Regression-Analysis/
├── data/                             # Kaggle dataset files
│   ├── train.csv
│   └── test.csv
├── notebooks/                        # Integrated analysis & modeling
│   └── ChandlerJ_DDS-8555-Assignment2.ipynb
├── submissions/                      # Final model CSV files
│   ├── submission_Kaggle_Chandler_ols.csv
│   └── submission_Kaggle_Chandler_ridge.csv
├── README.md                         # Project overview and documentation
└── requirements.txt                  # Python dependency manifest
```

# References

Friedman, J., Hastie, T., & Tibshirani, R. (2010). Regularization Paths for Generalized Linear Models via Coordinate Descent. 33(1). https://www.jstatsoft.org/article/view/v033i01/

Gray, V. (2017). Principal Component Analysis: Methods, Applications and Technology. Nova Science Publishers, Incorporated. http://ebookcentral.proquest.com/lib/nu/detail.action?docID=4801141

Hoerl, A. E., & Kennard, R. W. (1970). Ridge Regression: Biased Estimation for Nonorthogonal Problems. Technometrics, 12(1). https://homepages.math.uic.edu/~lreyzin/papers/ridge.pdf

Nash, W., Sellers, T. L., Talbot, S. R., Cawthorn, A. J., & Ford, W. B. (1994). The Population Biology of Abalone (Haliotis Species) in Tasmania. I. Blacklip Abalone (H. rubra) from the North Coast and Islands of Bass Strait. Sea Fisheries Division, Technical Report No, 48. https://www.researchgate.net/profile/Warwick-Nash/publication/287546509_7he_Population_Biology_of_Abalone_Haliotis_species_in_Tasmania_I_Blacklip_Abalone_H_rubra_from_the_North_Coast_and_Islands_of_Bass_Strait/links/5d949460458515202b7bf592/7he-Population-Biology-of-Abalone-Haliotis-species-in-Tasmania-I-Blacklip-Abalone-H-rubra-from-the-North-Coast-and-Islands-of-Bass-Strait.pdf

Reade, W., & Chow, A. (2024). Regression with an Abalone Dataset. https://www.kaggle.com/competitions/playground-series-s4e4/overview

Zou, H., & Hastie, T. (2005). Regularization and Variable Selection Via the Elastic Net. Journal of the Royal Statistical Society Series B: Statistical Methodology, 67(2), 301–320. https://doi.org/10.1111/j.1467-9868.2005.00503.x

# AI Disclosure and Usage Statement
In accordance with the course policy on academic integrity, I acknowledge the use of Gemini (a large language model by Google) as a research and brainstorming tool for this assignment. The AI was used to assist in structuring the executive summary, clarifying the theoretical applications of Ridge regression as established by Hoerl and Kennard (1970), and troubleshooting Python syntax for the diagnostic plots in the Abalone analysis. All content suggested by the AI was critically evaluated for accuracy, checked against the provided course datasets (Carseats and Abalone), and significantly rewritten to reflect my own voice and professional interpretation. The final analysis, interpretations of statistical significance, and conclusions represent my own independent scholarship.
