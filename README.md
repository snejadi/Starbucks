# Starbuck promotion strategy

## Summary
<br>The objective of this project is to use the training data and understand what patterns in V1-V7 indicate that a promotion should be provided to a user. Specifically, the goal is to maximize Incremental Response Rate (IRR), and Net Incremental Revenue (NIR).

## The Data
<br>The dataset was originally used as a take-home assignment provided by Starbucks for their job candidates. The data consists of about 120,000 data points split in a 2:1 ratio among training and test files. In the experiment simulated by the data, an advertising promotion was tested to see if it would bring more customers to purchase a specific product priced at $10. Since it costs the company 0.15 to send out each promotion, it would be best to limit that promotion only to those that are most receptive to the promotion. Each data point includes one column indicating whether or not an individual was sent a promotion for the product, and one column indicating whether or not that individual eventually purchased that product. Each individual also has seven additional features associated with them, which are provided abstractly as V1-V7.
<br>
<br>The [Training_data](https://github.com/snejadi/Starbucks/blob/3cd8cd4017e6e10e0eb84f84817ef845f93e012d/training.csv) is included in this github reporitory [Starbucks](https://github.com/snejadi/Starbucks.git).
<br>The [Test_data](https://github.com/snejadi/Starbucks/blob/3cd8cd4017e6e10e0eb84f84817ef845f93e012d/Test.csv) is also included in the github reporitory [Starbucks](https://github.com/snejadi/Starbucks.git).

## Analysis
<br> The analysis includes the following steps:

1- Exploratory data analysis:
- The training data consists of 84,534 data points. The following bar charts show the distribution of data between different groups.

- The data is evenly distrbuted (balanced) between the treatment (who recieved promotion) and control (that did not recieve a promotion) groups.
- The distribution of data is severly imbalanced between the purchase and non-purchase groups. This necessiates implementing over-sampling techniques. Two methodologies were further evaluated : a) pandas.DataFrame.sample to generate random samples, and b) [SMOTE](https://imbalanced-learn.org/stable/references/generated/imblearn.over_sampling.SMOTE.html) (Synthetic Minority Oversampling Technique)

- Scaling the data
- V1-V7


2- Two stage classification:
- Stage 1: The control group (who did not recieve a promotion) was used and a classifier is trained to classify purchase data. The main purpose of this step is to filter/classify the customers who would purchase the product regardless of recieving a promotion.
- Stage 2: Initially the trained classifier in stage 1 is used to remove the customers who would purchase the product regardless of recieving a promotion. Next, the filtered data in treatment group is used to train the second classifier that classifies customers who make a purchase only if they recieve a promotion. 
- The classification includes the following steps: 
a) SMOTE: oversampling imbalaced data
b) MinMaxScaler: Scale and translate each feature between zero and one.
c) PCA: Principal component analysis for dimensionality reduction
d) KNeighborsClassifier: to perform the actual classification
Similar steps are used for both stages of classification. 
GridSearchCV is also used to search over parameter values for SMOTE, PCA, and KNeighborsClassifier.

## File Description
<br>The Jupyter Notebook is used for this study that includes the following steps: data extraction, cleansing, transformation, and analysis. 
<br>../Airbnb_data/Seattle/[listing.csv](https://github.com/snejadi/Airbnb/blob/main/Airbnb_data/Seattle/listings.csv)&emsp;&emsp;Airbnb reference dataset
<br>../Airbnb_analysis/[Seattle.ipynb](https://github.com/snejadi/Airbnb/blob/main/Airbnb_analysis/Seattle.ipynb)&emsp;&emsp;Jupyter Notebook containing the extraction, cleansing, transformation, and analysis.
<br>..[/figures/](https://github.com/snejadi/Airbnb/tree/main/figures)&emsp;&emsp;The figures exported from Jupyter Notebook analysis file.

## Installations
<br>Python 3 is required to run this project. Jupyter Notebook and the following libraries are required to preform the analysis and export the results: pandas, numpy, scipy, statsmodels, os, sklearn, Matplotlib, seaborn, etc.

## How to use the files
<br>The user should start with the [<i>Seattle</i>.ipynb](https://github.com/snejadi/Airbnb/blob/main/Airbnb_analysis/Seattle.ipynb) file. The file loads the [listing](https://github.com/snejadi/Airbnb/blob/main/Airbnb_data/Seattle/listings.csv) dataset.

## Author
<br>Siavash Nejadi