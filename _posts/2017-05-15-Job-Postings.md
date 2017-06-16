---
layout: post
title:  "Project 4 - Web Scraping Job Postings"
project: true
---

**The aim** of this project is to investigate the trend in Jobs related to Data Science, Data Analysts, Business Intelligence and Business Analysts. The main focus is to find key features that help to distinguish Salary scale, Job Titles , Industry among the different Jobs that have been selected.

[Click here to view on github](https://github.com/roshanlulu/gaProjects/tree/master/gaProject4)

## Problem Statement
1. Determine the industry factors that are most important in predicting the salary amounts for these data.
2. Determine the factors that distinguish job categories and titles from each other. For example, can required skills accurately predict job title?

## Approach
This is a data science problem that required data extraction, data cleaning and data modelling. Hence, I will be dividing this into 3 phases.

### Data extraction
The Job postings were scraped from a Job aggregator called Seek.com.au. Jobs pertaining to NSW, Victoria and Queensland were scraped. The study is based on 2000 Job postings collected during a 24 hour period.

![]({{ site.url }}/assets/project4/seek.png)

1. Collect search url: Generate the job search urls based on the job description and location and save it into a pandas dataframe. [This is the first search result page.]
2. Parse search url: Parse through the generated search urls to get all the search page links till the last one. Since the code looks for the next page link, the no of pages ina  result is not required.
3. Get Job posting urls: Save links to all the job postings in a search result page using scrapy. All individual job postings are available at this stage. This is done using the `requests` library that gets the response text in the url. The `Selector` library from scrapy uses xpath to navigate through the contents. 
4. Extract features from job postings: Extract the title, region,, location, salary, worktype, classification, job description using Scrapy, from the job posting and save it to an SQL database and a csv file. This is required to avoid scrapping the jobs every time.

### Data Cleaning
From the web scraping results, data was stored in a database. Hence, the next step would be to clean the data. The dataset consists of many categorical variables. One of the required feature is Salary. The salary was in an inconsistent format with either textual description, numerical ranges or values. 

First look at the dataset:
- No of datapoints - 2831
- Columns - 'job title', 'region', 'location', 'salary', 'worktype', 'advertised by', 'classification', 'job description'
- Check for null values
    - There is 1 job posting with null value in location, worktype, classification. Since it is not a significant no of datapoints, it can be dropped.
![]({{ site.url }}/assets/project4/nullvalues.png)
- Clean the values in each Columns
    - Job title - There were numerous unique job titles. Using feature extraction Count vectorizer, I extracted the top 20 words found in the job titles. This provided an estimate of the job categories that I wanted to create.
    - Location, Region - This was quite clean. The missing values in the 'region' were put into an unknown category. Since these were categorical variables, I encoded them into numerical classes. These are useful whenplotting
    - Job Classification - At the first look of the unique values, I realized that I had to pick the categories required for the problem statement and the ones with more information. Categories with lesser number of postings were grouped into a separate category.
    - Work Type - This was quite a clean feature. Encoding was done.
    - Advertiser - This was not a very important feature. But since the problem statement had to look at different aspects of the industry, I divided it into jobs posted by consultancy, universities or companies.
    - Job Search keyword - This feature was provided as input, hence was a clean feature
    - Job description - Some text manipulation was required here to remove special charachters and noise that was extracted.
    - Salary - Major cleaning required here to remove text information in between the numbers! **Thanks to regular expressions for manking my life easier**. Extracted values had to be standardized to a yearly rate. With all this done, I was interested to check outliers here. ** Jobs with salary > 350000, Definitely an outlier. Thanks to Box plot!**

- Explore the data  
    - Lot of jobs in Sydney compared to Melbourne and Brisbane
    - In every city the CBD has more jobs compared to suburbs
    - Junior postions are in demand
    - Median salary is higher in sydney except for a Manager position. Interesting!
    - Among Data analyst, Data scientist, Research scientist, Business analysts - Business analysts are the highest paid !
    - Plotting a heat map was not useful in this case.

### Data Modelling

1. What are the factors that impact salary and can be used to predict it?

- Salary is a continuous variable. Hence, I choose to apply a regression model. 
- Risk: The no of valid salaries are a small proportion.
- Approach: Choose a small training set and proceed with regression to check performance of the model.
- The predictors were mostly categorical variables. Tt was convert ed to dummy variables.
- Machine learning models used for regression problem:
    - Stats model - R2 0.244 - The predictors explain 24.7% of the variance, which is not good.
    - Linear Regression model- I tried with different test train splits[70/30,20/80] making the training set slightly larger to check if I was getting better results. But the score remained in the range of 0.2 - 0.3. 
    - The model is bad, but I'd still like to check the cross validation results
    - K-fold Cross validation - A negative R2! 
    - Trying the above methods I could come to a conclusion that the model performed quite bad with all the predictors.
    - Would it be better with selected features? Then I went ahead to try regularization techniques.
    - With Ridge, Lasso and Elastic net regularization techniques the R2 value did not increase much. 
    - In the search for a better performing model, next I'm going to try Feature selection method like kbest and compare it with results from lasso best found above.
    - The best score was still around 0.1 which was not any good at all.
    - I went ahead and tried Gradient descent regressor model to check if the loss function could be reduced.
Inference:
- The Linear Regression is not a good model for predicting the salary. It could be because of the less valid salaries that were available.
- How to make the model better:
    - Try vectorizing the words and add them as features. 
    - Get more valid salary data

2. Discover which features have the greatest importance when determining a low vs. high paying job.

>
- What next?:
    - Due to the less number of valid salaries, it would be easier to convert this into a classification problem.
    - - In order to get the overall features/SKILLS/Keywords that are significant, the target is not the continuous salary anymore.
    - Added a new target that will be 0/1 based on low paying vs high paying jobs!
    - This now becomes a classification problem.
    - What features are good to determine the new target low/high pay jobs!

- Assumption
    - Salary > 120,000 per annum - High paying job
    - With the available data, 120000 looks like the median. I chose this for better segregation of results

- Machine learning models used for classification problem:
    - The all time favourite 'Logistic regression' was applied.
    - It gave a cross validation score of 0.71. That is quite good.
    - The aim is to find features that contribute to predicting the different classification groups. 
    - Using the Grid Search CV for the Decision tree classifier it was found that the key factors that differentiated a low and a high paying job were: 'WorkType_Code_1', 'Title_Code_1', '400 words','Classif_Code_2', 'advanced excel', 'business analyst', 'complex data', 'data science', 'business requirements', 'proven experience', 'big data', 'Region_Code_9', 'apply button', 'Classif_Code_5', 'key stakeholders', 'high performing', 'business intelligence','experience working', 'data analyst', 'management skills', 'Title_Code_5', 'clicking apply', 'Region_Code_12', 'data scientist','tertiary qualifications'.
    - The score was 0.71 again. This model performed quite well.

3. What components of a job posting distinguish data scientists from other data jobs?

    - The Feature KeyJob_Code is the tag that differentiates Data scientists from other jobs. From the data, we know that KeyJobCode = 1/0 is a Data Scientist or Data Analyst ( Choosing both these job codes to get more data points). In order to proceed with a model for this problem, I would have to tweak my feature such that it boils down to a binary classification problem.
    - Creating a dataframe from the ngrams(2,4) and concatenating it as features would be helpful for this problem statement.
    - Again the grid Search cv with a Decision tree classifier gave good results.
    - data science', 'data analyst', 'business intelligence','data analytics', 'data reporting', 'data driven', 'market leader','business data', 'cbd location', 'Title_Code_1', 'best practices',


