# FIFA World Cup 2022: Machine Learning Analysis of Match-Level Predictors of Team Success

This project uses supervised machine learning to uncover which match-level performance metrics best explain team success in the **FIFA World Cup 2022**. This analysis aims to support **strategic improvement for the U.S. Men’s National Team (USMNT)** by identifying critical factors that differentiate winning teams from losing ones on the world stage.

We combine **feature engineering**, **cross-validation**, and **model interpretation** to understand and predict binary match outcomes (win/loss) using performance statistics from each team per match.

## Project Contributors

- **Ryan Cullen**  
- **Alec Zerona**  
- **Warren Paintsil**  
- **Will Hensley**

## Business Objective

The **USMNT has underperformed** at the international level. Our objective is to identify **actionable insights from World Cup data** that can support **performance optimization and tactical adjustments** by:

- Identifying which **key metrics drive match wins**
- Understanding the **relative strengths and weaknesses** between teams
- Evaluating how **machine learning can inform soccer strategy**

## Data Description

### Source
- [Kaggle: Fifa World Cup 2022 Complete Dataset](https://www.kaggle.com/datasets/die9origephit/fifa-world-cup-2022-complete-dataset/data)
- Match-level data with 88+ performance features

### Key Variables
- **Target**: `team1_win` (1 if team1 won the match, 0 if lost)
- **Input Features**: 
  - Goals, possession, passes, crosses, fouls, duels, pressures
  - **Advanced metrics**: line breaks, shot accuracy, contested possession, etc.

## Methodology

### 1. **Data Cleaning & Feature Engineering**
- Created `team1_win` as a binary target (excluding ties)
- Cleaned for nulls, redundancy, and noise
- Derived **relative performance metrics**:  
  `feature_team1 - feature_team2` (i.e. `shots_diff = shots1 - shots2`)
- Focused on **efficiency ratios** (i.e. shot accuracy, pass %)
- Removed highly correlated or duplicate features

### 2. **Modeling Strategy**
Used the `caret` package for a consistent training pipeline across models:
- **Standardized preprocessing**
- **5-fold cross-validation** with consistent resampling
- **Grid search for hyperparameter tuning**

### 3. **Models Developed**
| Model                        | Notes |
|-----------------------------|-------|
| **Logistic Regression**     | Interpretable baseline with LASSO, Ridge, Elastic Net |
| **Random Forest**           | Tree ensemble model with variable importance |
| **Gradient Boosted Model**  | Focused on learning from misclassifications |
| **XGBoost**                 | Tuned for performance and robustness |

## Evaluation Metrics

Each model was evaluated on:
- **Accuracy**
- **Precision**
- **Confusion Matrix**
- **Feature Importance Rankings**
- **Cross-validated performance stability**

## Results Summary

| Model         | Accuracy | Precision | Key Predictors |
|---------------|----------|-----------|----------------|
| **LASSO**     | 0.7308   | 0.80      | Shot accuracy, crosses, passes, line breaks |
| **Random Forest** | 0.7308 | 0.7143  | Cross efficiency, possession difference |
| **GBM**       | 0.6538   | –         | Line breaks, cross efficiency, contested possession |
| **XGBoost**   | 0.6154   | –         | Possession, contested duels, offside efficiency |

## Key Insights

- **Shot accuracy difference** was the most consistent predictor across all models.
- **Cross efficiency** and **line break effectiveness** separated winning teams from losers, indicating that **final third execution** is critical.
- Possession alone was **not** a strong standalone predictor — **how efficiently possession was converted into action** mattered more.
- LASSO and Random Forest produced the **most balanced performance** between interpretability and accuracy.

## Recommendations for USMNT

Based on our findings, the USMNT can improve international competitiveness by:

- **Prioritizing accurate finishing over volume of attempts**
- **Optimizing wing play and crosses into the box**
- **Increasing successful line breaks and dribble penetrations**
- **Focusing on quality possessions** rather than just time on ball

These recommendations emphasize **execution and precision** over passive control.

## What Was Used
- R & RMarkdown
- Caret for modeling and tuning
- ggplot2 for visualization
- XGBoost, randomForest, and glmnet for further modeling

## Limitations
- Small sample size (63 matches, no ties)
- Model performance constrained by class imbalance
- Limited to match-level stats (no player-level or xG data)

## Next Steps
- Integrate player-level, spatial tracking, and more data
- Build a dashboard interface for coaching staff
- Test models on future World Cup qualifiers and matches
