# Predicting a startup's Acquisition Status

## Table of Contents
    • Introduction
    • Abstract
    • Data collection
    • Dataset Explanation
    • Data preprocessing
    • Modelling
    • Data Visualization
    • Results and Discussion
    • Conclusion
    • References





## Introduction
TEach year, the US Department of Labor releases a dataset for several visa types, including L and H visas as well as PERM applications. The dataset contains information about the employer, such as Name, Address, whether it is H1-B dependent, and employment information, such as Job Title and projected Salary.
We begin by rejecting the null hypothesis that there is a relationship between an employer's profile and the success of a visa application.
In this work, we intend to model that and forecast whether an application will be accepted or refused. But we restrict the dataset.
to additional visa kinds in addition to H1-B visas, the most common type of work visa for immigrants.


## Abstract
The most sought-after non-immigrant visa that enables foreign employees to work in speciality occupations in the United States is the H1-B visa.
More over 1 million people filed for H-1B visas in 2019—this number includes new applications, renewals, and transfers of H-1Bs to other employers. More than 180,000 new candidates for H1-B were received , but only 80,000 of those were chosen in the lottery to move on to the USCIS for approval.
A job applicant's employment and legal status are uncertain due to the H1-B visa application procedure, which also results in expensive legal and visa processing costs for the employer over the course of employment. For 2019, we intend to make use of the anonymized dataset that United Status Department of Labor publishes publicly [4] and apply data science techniques to improve predictability of approval.

## Data collection
Parsing the 2019 excel data into, we found 664616 cases for H1-B applications. The dataset contains features that gives information about employer and visa applicant, and 260 columns are there.

## Data preprocessing
Dataset needed to be preprocessed before modelling was done.

- Features of the Data: CASE_STATUS,VISA_CLASS,EMPLOYER_NAME,SECONDARY_ENTITY_1,AGENT_REPRESENTING_EMPLOYER,JOB_TITLE,SOC_TITLE,SOC_CODE,NAICS_CODE,CONTINUED_EMPLOYMENT,CHANGE_PREVIOUS_EMPLOYMENT,NEW_CONCURRENT_EMPLOYMENT,CHANGE_EMPLOYER,AMENDED_PETITION,H-1B_DEPENDENT,SUPPORT_H1B,WILLFUL_VIOLATOR,WAGE_RATE_OF_PAY_FROM_1,WAGE_UNIT_OF_PAY_1,TOTAL_WORKER_POSITIONS.


- Removal of all the Unwanted Columns. As we can clearly see there were many irrelevant and reductant columns in the dataset which needed to be removed like PW_NON-OES_YEAR_10,PW_SURVEY_NAME_10, PW_OTHER_SOURCE_10, STATUTORY_BASIS, MASTERS_EXEMPTION, PUBLIC_DISCLOSURE etc. These are all the irrelevant columns There were columns with N/A values more than 96% which were also dropped. This was Done due to the fact that those columns will not help regarding the modelling and would only hinder the overall process.


- Treating NULL values: SECONDARY_ENTITY_1, AGENT_REPRESENTING_EMPLOYER, H-1B_DEPENDENT, SUPPORT_H1B, WILLFUL_VIOLATOR for these features what we did we apply *mode* method and rest of the null values we dropped them.


- Outliers:  Removal of all the outliers in  'WAGE_RATE_OF_PAY_FROM_1' as they can Be clearly seen in the boxplot. IQR Method was used in order to drop them. 


- Finding duplicate values and treat it : many duplicates values were there so we replace the duplicate values with original ones. in CONTINUED_EMPLOYMENT and SOC_TITLE we treated the duplicate values.

- Remove unwanted columns :Here we remove VISA CLASS, EMPLOYER_NAME, JOB_TITLE, SOC_CODE, NAICS_CODE

- Encoding : We did label encoding on SOC_TITLE and JOB_TITLE. and for manual replacement for YES or NO values we replaced YES with 1 and NO with 0. we use these features: 'FULL_TIME_POSITION','SECONDARY_ENTITY_1','AGENT_REPRESENTING_EMPLOYER','H-1B_DEPENDENT','WILLFUL_VIOLATOR' 

## Modeling 
e define our task as a binary classification problem where we predict whether the visa status will certified(1) or denied(0).
- Naive Bayes :
Naive Bayes classifiers are a collection of classification algorithms based on Bayes’ Theorem. It is not a single algorithm but a family of algorithms where all of them share a common principle, i.e. every pair of features being classified is independent of each other.
- Decision Tree :
Decision Tree is a Supervised learning technique that can be used for both classification and Regression problems, but mostly it is preferred for solving Classification problems. It is a tree-structured classifier, where internal nodes represent the features of a dataset, branches represent the decision rules and each leaf node represents the outcome.
In a Decision tree, there are two nodes, which are the Decision Node and Leaf Node. Decision nodes are used to make any decision and have multiple branches, whereas Leaf nodes are the output of those decisions and do not contain any further branches.



## Data Visualizations
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data. We have visualize the data check the outliers using boxplot and verified if the data is normalized. Using heatmap ,we found the correlation between each features. These techniques are very much useful when it comes reduce the more correlated variables in the dataset. Inaddition, We have checked the data balance in the dataset. It is clearly indicated that the dataset is imbalanced and the operating class is occred more often as compared to the closed class.

## Results and Discussions
### Model 1: Naive Bayes
Naive Bayes classifiers are a collection of classification algorithms based on Bayes’ Theorem. It is not a single algorithm but a family of algorithms where all of them share a common principle, i.e. every pair of features being classified is independent of each other.
Consider a fictional dataset that describes the weather conditions for visa approval. Given the conditions, each tuple classifies the conditions as certified(“Yes”) or declined(“No”) for visa approval.
here we got 95% of Accuracy
### Model 2: Decision Tree
Decision tree is the most powerful and popular tool for classification and prediction. A Decision tree is a flowchart-like tree structure, where each internal node denotes a test on an attribute, each branch represents an outcome of the test, and each leaf node (terminal node) holds a class label.
A tree can be “learned” by splitting the source set into subsets based on an attribute value test. This process is repeated on each derived subset in a recursive manner called recursive partitioning. The recursion is completed when the subset at a node all has the same value of the target variable, or when splitting no longer adds value to the predictions. The construction of a decision tree classifier does not require any domain knowledge or parameter setting, and therefore is appropriate for exploratory knowledge discovery. Decision trees can handle high-dimensional data. In general decision tree classifier has good accuracy. Decision tree induction is a typical inductive approach to learn knowledge on classification. 
here we got 96% of Accuracy
#  Model Deployment
we used pickle file for both the models LR and RF we developed a webpage with html and backend we used flask and Django python framework.

## Conclusion:
We found the Decision Tree model to be predicting high accuracy but hides the true negatives as it tries to fit the data. So, we believe that
visa outcome is not as dependent on employer and job profile as we presumed in our null hypothesis, it has an element of random
behavior in the decision. We captured individual company names, job titles and job categories to see if they are useful measures in
modelling the accuracy. The result was a drop in total accuracy but higher level of predicting true negatives. We also evaluated
random forest and logistic with modelling more features.
In future, the wage can be made to fit using kernel trick with a higher dimension to evaluate how good it fits the data to predict the
outcome. Neural network and boosting can also be used for stronger learning from logistic, Naïve Bayes, SVM and Random Forest to
predict the outcome.
