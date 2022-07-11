# Starbuck promotion strategy

## Summary
<br>The objective of this project is to use the training data and understand what patterns in the training data indicate that a promotion should be provided to a user. Specifically, the goal is to maximize Incremental Response Rate (IRR), and Net Incremental Revenue (NIR).

## The Data
<br>The dataset was originally used as a take-home assignment provided by Starbucks for their job candidates. The data consists of about 120,000 data points split in a 2:1 ratio among training and test files. In the experiment simulated by the data, an advertising promotion was tested to see if it would bring more customers to purchase a specific product priced at $10. Since it costs the company 0.15 to send out each promotion, it would be best to limit that promotion only to those that are most receptive to the promotion. Each data point includes one column indicating whether or not an individual was sent a promotion for the product, and one column indicating whether or not that individual eventually purchased that product. Each individual also has seven additional features associated with them, which are provided abstractly as V1-V7.
<br>
<br>The [Training_data](https://github.com/snejadi/Starbucks/blob/3cd8cd4017e6e10e0eb84f84817ef845f93e012d/training.csv) is included in this github reporitory [Starbucks](https://github.com/snejadi/Starbucks.git).
<br>The [Test_data](https://github.com/snejadi/Starbucks/blob/3cd8cd4017e6e10e0eb84f84817ef845f93e012d/Test.csv) is also included in the github reporitory [Starbucks](https://github.com/snejadi/Starbucks.git).

## Analysis
<br> The analysis includes the following steps:

1- Exploratory data analysis:
- The training data consists of 84,534 data points. The following bar charts show the distribution of data between different groups.
![Figure_01](https://github.com/snejadi/Starbucks/blob/aca62cdb8b8f26d3e5b75340ce27bca5a441dc9a/figures/fig_01.png?raw=true)
- The data is evenly distrbuted (balanced) between the treatment (who recieved promotion) and control (that did not recieve a promotion) groups.
- The distribution of data is severly imbalanced between the purchase and non-purchase groups. This necessiates implementing re-sampling techniques, that is removing samples from the majority class or adding more samples to the minority class. In this example, two methodologies were analysed: a) re-sampling using [pandas.DataFrame.sample](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sample.html), which duplicates random examples of the minority class, and b) Synthetic Minority Oversampling Technique ([SMOTE](https://imbalanced-learn.org/stable/references/generated/imblearn.over_sampling.SMOTE.html)). SMOTE improves the accuracy of classifiers by generating synthesized elements using nearby minority class points ([Chawla et al., 2002](https://www.jair.org/index.php/jair/article/view/10302/24590)). The SMOTE out performed random re-sampling.
- The following bar charts show the range and distribution of features V1 to V7. 
![Figure_02](https://github.com/snejadi/Starbucks/blob/aca62cdb8b8f26d3e5b75340ce27bca5a441dc9a/figures/fig_02_features.png)
- The features have different range and distributions. Transforming and scaling the features is required prior to further analysis and classification. 

2- Two stage classification:
- Stage 1: The control group (who did not recieve a promotion) was used and a classifier is trained to classify purchase data. The main purpose of this step is to filter/classify the customers who would purchase the product regardless of recieving a promotion.
- Stage 2: Initially the trained classifier in stage 1 is used to remove the customers who would have purchased the product regardless of recieving a promotion. Next, the filtered data in treatment group is implemented and a second classifier is trained that classifies customers who make a purchase only if they recieve a promotion. 
- The classification pipeline contains the following steps: 
i) SMOTE: over-sampling minority class
ii) MinMaxScaler: Scale and translate each feature between zero and one
iii) PCA: Principal component analysis for dimensionality reduction
iv) KNeighborsClassifier: to perform the classification
Similar steps are used for both stages of classification, and GridSearchCV is used to facillitate searching over parameter values for SMOTE, PCA, and KNeighborsClassifier.

## File Description
<br> The Jupyter Notebook file ([Starbucks](https://github.com/snejadi/Starbucks/blob/b4b54972423d321e21b006282fb17e10349785dd/Starbucks.ipynb))for Exploratory data analysis, classification, and validating the results. 
<br> The training data ([training.csv](https://github.com/snejadi/Starbucks/blob/b4b54972423d321e21b006282fb17e10349785dd/training.csv)) 
<br> The seperate test data ([Test.csv](https://github.com/snejadi/Starbucks/blob/b4b54972423d321e21b006282fb17e10349785dd/Test.csv)) to validate the results.
<br> [test_results.py](https://github.com/snejadi/Starbucks/blob/b4b54972423d321e21b006282fb17e10349785dd/test_results.py) to compare the results against Test.csv calculating Incremental Response Rate (IRR), and Net Incremental Revenue (NIR). 

## Installations
<br>Python 3 is required to run this project. Jupyter Notebook and the following libraries are required to preform the analysis: numpy, pandas, scipy, sklearn, imblearn, random, pickle, stats, matplotlib, and seaborn.

## Licensing, Acknowledgements
<br> The author wishes to acknowlwdge Udacity and Starbucks. The data, templates, and the python file to validate the results are provided by [Udacity](https://www.udacity.com/).

## Author
<br>[Siavash Nejadi](https://github.com/snejadi/)