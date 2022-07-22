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
The H1 B visa is the most demanded visa world-wide. The
H1 B visa applications are very heavily varied across many fields i.e. job, job
title, year of petition, accountable wages, city of work etc. The purpose of this
research is to estimate the likelihood of visa approval on the basis of metadata
provided. We shall consider all aspects by which the petition may be approved
or otherwise, strictly working on the data provided in the application. We limit
the dataset to H1-B visas which is most popular work visa for an immigrant,
but it can be extended to other types as well.


## Abstract
The H-1B is a visa in the United States under the Immigration
and Nationality Act, section 101 that allows U.S. employers to temporarily
employ foreign workers in specialty occupations. In March 2021, employers
filed over 300,000 H-1B registrations for only 85,000 petitions available under
the FY 2022 H-1B cap. That means the U.S. government rejected more than
70% of H-1B registrations for high-skilled foreign nationals before an
adjudicator evaluated the applications.
In this project, we predict the approval of work visa(H1-B) based on
company’s attributes.
## Data collection
Dataset consisted of 1048547 rows and 260 columns
. Out of which, we took 20 important features like case_status, visa_class, e
mployee_name, secondary_entity, agent_represnting_employer, job_title, so
c_name and other 12 contextual features.
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
- Naive Bayes : Naïve Bayes Classifier is one of the simple and most
effective Classification algorithms which helps in building the fast
machine learning models that can make quick predictions. It is a
probabilistic classifier, which means it predicts on the basis of the
probability of an object. The Naive Bayes classifier works on the
principle of conditional probability, as given by the Bayes theorem. They
are fast and easy to implement but their biggest disadvantage is that the
requirement of predictors to be independent.


- Decision Tree : Decision Tree is a Supervised learning technique. A
decision tree algorithm will be used to split dataset features through a cost
function. It has a hierarchical, tree structure, which consists of a root
node, branches, internal nodes and leaf nodes. A significant advantage of
a decision tree is that it forces the consideration of all possible outcomes
of a decision and traces each path to a conclusion. It creates a
comprehensive analysis of the consequences along each branch and
identifies decision nodes that need further analysis.



## Data Visualizations
Data visualization is the graphical representation
of information and data in a pictorial or graphical format. Data visualization
tools provide an accessible way to see and understand trends, patterns in
data, and outliers. In this project, we have used different visualization tools.
For correlation we used heatmap. For checking outliers we used boxplot.
Apart from these, we used bar graph for case_status and visa class; barplot
for empoyer_name and job_title; pie chart, subplot, countplot for others. We
used axvline for Wage Distribution of case status CERTIFIED and DENIED
with their Average.
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
We worked on a huge unbalanced dataset. We did data
analysis and feature engineering on data. For model building we worked in
two models: decision tree and naïve bayes. We find that the decision tree
provides us with our best results, consistently across samples. Naïve bayes
also performed very well. In future, we can use more algorithms for dataset
and predict results.
