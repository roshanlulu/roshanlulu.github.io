---
layout: post
title:  "Project 4 - Web Scraping Job Postings"
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

### Data cleaning


### Data Modelling