# DSA-2040-Data-Warehousing-and-Mining-Assignment-Association-Rule-Mining-with-Real-World-Data\
Aaron irakoze 
Id-515
Raw dataset used :https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci
Description: This raw data set contains of online reatail contains all the transactions occurring for a UK-based and registered, non-store online retail between 01/12/2009 and 09/12/2011.The company mainly sells unique all-occasion gift-ware. Many customers of the company are wholesalers



Key Steps

### 1. Importing and Setup
- Imported key Python libraries (pandas, numpy, mlxtend, matplotlib) for data wrangling, analysis, and visualization.  
- Defined file paths and created an "outputs/" folder to store generated CSVs and figures.

### 2. Data Loading
- The dataset **Online Retail II** was loaded from Kaggle as either "online_retail_II.xlsx" (two sheets) or "online_retail_II.csv".
- Combined both years ("2009–2010" and "2010–2011") into a single DataFrame.

### 3. Data Cleaning & Preprocessing
- Standardized column names to lowercase with underscores for consistency.  
- Removed:
  - Duplicate rows  
  - Rows missing key identifiers ("invoice", "stockcode", "description")  
  - Negative or zero "quantity" and "unitprice" values (representing returns).  
- Converted the "invoice" column to string format for transaction IDs.

### 4. Basketization
- Converted data into a **basket (Invoice × Item)** matrix using Pandas `groupby` and `unstack`.  
- Transformed quantities into binary indicators (1 = purchased, 0 = not purchased).  
- This one-hot structure enabled the use of association rule mining algorithms.

#5. Frequent Itemset Mining
- Applied both "Apriori" and "FP-Growth" algorithms from "mlxtend.frequent_patterns".  
 Tested two minimum support thresholds (0.02 and 0.03) to observe differences in runtime and result density.  
- Exported summary results to "algo_comparison.csv".

#Visualization
- Plotted the **Top 10 Frequent Itemsets by Support** using "matplotlib" to highlight common purchase combinations.  
- The figure was saved as "top_itemsets_support.png".

#Association Rules
- Generated association rules from the FP-Growth itemsets using the "association_rules()" function.  
- Calculated and ranked rules using "support", "confidence", and "lift".  
- Exported:
  - All rules to "rules_all.csv"
  - Top 3 strongest rules (based on lift and confidence) to "rules_top3.csv"

#Algorithm Comparison
- Compared Apriori vs FP-Growth for runtime and number of itemsets found.
- FP-Growth proved faster and more scalable for large transaction data.



#Libraries Used

pandas - Data loading, cleaning, and manipulation.
numpy - Numerical support and array operations. 
mlxtend.frequent_patterns -Implements Apriori, FP-Growth, and association rule generation. 
matplotlib - Data visualization (bar charts and plots).
pathlib -File path management for Windows. 


#Interpretations of Results

-Data Insights
- After cleaning, the dataset represented valid customer purchase transactionsa and Top items included household and decorative goods, often purchased together in small bundles.

-Algorithm Findings
- Both Apriori and FP-Growth produced identical frequent itemsets and FP-Growth was significantly faster, confirming its efficiency for large transaction volumes.
At 2% support, FP-Growth found more meaningful patterns with less computation time.

#Association Rule Insights
- Rules with **Lift > 3.0 and Confidence > 0.5 indicate strong item relationships.
- Example: Customers who buy "{Set of Tea Mugs}" are very likely to also purchase "{Teapot}".  
- Such insights can guide:
  - Cross-selling: Suggest complementary items during checkout.  
  - Product placement:Display related items together (both online and in-store).  
  - Bundle promotions: Create combo offers to increase average basket size.
