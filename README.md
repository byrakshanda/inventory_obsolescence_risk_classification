# Inventory Obsolescence Risk Classification (Decision Tree)

## What this project does
Classifies retail inventory items into Low, Medium, or High obsolescence risk 
(the risk that stock expires or goes unsold), using a Decision Tree Classifier.

## Dataset
Retail inventory dataset with 1,000 items and 19 columns, including brand, category, 
store location, stock quantity, daily sales, days until expiry, promotion status, 
and temperature sensitivity.

## Tools Used
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Jupyter Notebook

## What I did
- Checked data quality (no missing values or duplicates)
- Created the target variable `Obsolescence_Risk` from business logic: 
  Stock Coverage Days ÷ Days Until Expiry, split into Low / Medium / High 
  using the 25th and 75th percentiles
- Ran EDA on stock levels, expiry, sales, category, store location, promotions, 
  and temperature sensitivity against risk level
- Removed the columns used to build the target from the model inputs, 
  to avoid data leakage
- Encoded categorical columns with Label Encoding
- Trained a basic Decision Tree and checked for overfitting 
  (train 97.4% vs test 89.5%)
- Tuned the tree using GridSearchCV with 5-fold cross-validation
- Compared basic vs tuned models and analysed feature importance

## Results
| Model               | Training Accuracy | Testing Accuracy |
|---------------------|-------------------|------------------|
| Basic Decision Tree | 0.974             | 0.895            |
| Tuned Decision Tree | 0.889             | 0.895            |

**Final model:** Tuned Decision Tree (max_depth=10, min_samples_leaf=4, 
min_samples_split=10). It matches the basic model's test accuracy with a much 
smaller overfitting gap.

## Key Insights
- High-risk items have far less shelf life left (0.5 days on average vs 4.4 for Low-risk)
- High-risk items carry larger stock (average 225 units vs 125 for Low-risk) 
  and sell more slowly
- Produce has the highest share of High-risk items (67.7%)
- Brand and Store Location were the strongest features in the final model

## Note
The risk label was derived from inventory rules, not taken from real recorded 
outcomes, so these results show the method works on this data rather than 
proving real-world performance.

## How to run it
Open `inventory_obsolescence_risk_classification.ipynb` in Jupyter Notebook or 
Google Colab and run all cells. Requires `enhanced_smart_waste_dataset_v1.csv` 
in the same folder.
