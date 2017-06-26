## Feature selection/Dimensionality reduction
Regression is the way in which the model coefficients are determined which makes all the difference.
Regularisation work by penalizing the magnitude of coefficients of features along with minimizing the error between predicted and actual observations. The key difference is in how they assign penalty to the coefficients:
    
1. Libraries
- The classes in the sklearn.feature_selection module
2. Uses
- Either to improve estimators’ accuracy scores
- To boost their performance on very high-dimensional datasets.
3. Different types

A. Removing features with low variance

B. Univariate feature selection
    - Selecting the best features based on univariate statistical tests.
        - SelectKBest
        - SelectPercentile
        - Chi2 test
- For regression: f_regression, mutual_info_regression
- For classification: chi2, f_classif, mutual_info_classif
    Tips
    - If you use sparse data (i.e. data represented as sparse matrices), chi2, mutual_info_regression, mutual_info_classif will deal with the data without making it dense
    - Beware not to use a regression scoring function with a classification problem, you will get useless results.

C. Recursive feature elimination(RFE) and RFE Cross-validation(RFECV)
- Greedy optimization for finding the best performing subset of features.

D. Feature selection using SelectFromModel
- L1-based feature selection
- Randomized sparse models
- Tree-based feature selection

- Lasso picks out the top performing features, while forcing other features to be close to zero. It is clearly useful when reducing the number of features is required, but not necessarily for data interpretation
- Ridge regression forces regressions coefficients to spread out similarly between correlated variables.
- When selecting top features for model performance improvement, it is easy to verify if a particular method works well against alternatives simply by doing cross-validation. 

### Ridge
- Includes all or none of the features in the model

Advantages 
- Coefficient shrinkage
- Reduce model complexity

Disadvantage
- Cannot be used in cases with very high number of features as there will be computation challenge.

Use cases
- Prevents overfitting
- When there are highly correlated features as the coefficients will be distributed among them depending on correlation.

### Lasso

Advantages
- Shrinks coefficients
- Provides sparse solutions
- Computational advantage as it eliminates features with 0 coefficicents
- Selects one feature from the correlated features and reduced the others to 0.
Use cases
- feature selection when millions of features are available

## Selection of alpha
There is no general rule to select an alpha parameter for recovery of non-zero coefficients. It can by set by cross-validation (LassoCV or LassoLarsCV),


## Sparse recovery: feature selection for sparse linear models
Case 1: Small number of observations, Recover which features of X are relevant to explain y. 
- For this sparse linear models can outperform standard statistical tests if the true model is sparse, i.e. if a small fraction of the features are relevant.
- Lasso regularisation

# Selection vs extraction: 
- Selection chooses current features, extraction produces interactions of current features (linear or non-linear combinations)

References:
`http://scikit-learn.org/stable/modules/feature_selection.html`
`http://blog.datadive.net/selecting-good-features-part-iv-stability-selection-rfe-and-everything-side-by-side/`
`https://www.analyticsvidhya.com/blog/2016/01/complete-tutorial-ridge-lasso-regression-python/`
`http://machinelearningmastery.com/feature-selection-machine-learning-python/`