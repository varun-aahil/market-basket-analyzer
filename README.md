# Market Basket Analysis: Association Rule Mining

## Project Objective
Unlike standard classification or regression tasks, this project focuses on **rule mining**. Using raw, real-world grocery receipts, the goal is to uncover hidden behavioral patterns among shoppers—specifically, calculating the mathematical probability of which items are most frequently purchased together to drive cross-selling strategies.

## Dataset
* **Source:** [Market Basket Optimization (Kaggle)](https://www.kaggle.com/datasets/d4rklucif3r/market-basket-optimisation)
* **Structure:** 7,501 rows of jagged transaction data representing individual store receipts, containing 120 unique items.

## Methodology & Tech Stack
Since standard Scikit-Learn does not support association rule learning natively, this project utilizes `mlxtend`.
* **Data Preprocessing:** Handled the jagged CSV rows by parsing them into a list of lists, then mapped them into a 7501x120 boolean matrix using `TransactionEncoder`.
* **Algorithm:** Applied the **Apriori** algorithm (`min_support=0.01`) to isolate combinations that appear in at least 1% of all store transactions to filter out statistical noise.
* **Rule Generation:** Extracted association rules with a baseline `confidence` threshold of 20%, sorting the final output by **Lift** to identify true purchasing drivers.

## Key Insight: The "Herb & Pepper" Rule
The algorithm successfully extracted high-value business logic from the raw receipts. The most powerful rule discovered was:

**`(herb & pepper) -> (ground beef)`**
* **Confidence (32.3%):** Nearly 1 in 3 customers who buy herbs & pepper will also buy ground beef.
* **Lift (3.29):** Customers buying herbs & pepper are **3.29 times more likely** to buy ground beef compared to the baseline average shopper.
