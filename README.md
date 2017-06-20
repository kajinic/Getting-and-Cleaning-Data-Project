# Getting-and-Cleaning-Data-Project
Data Science Course 3

## Overview
　
- The purpose of this project is to demonstrate the ability to collect, work
with, and clean a data set. The goal is to prepare tidy data that can be used
for later analysis.  A code book called `CodeBook.md` describes the variables,
the data, and any transformations or work that were performed to clean up the
data. 

- One of the most exciting areas in all of data science right now is wearable
computing. Companies like Fitbit, Nike, and Jawbone Up are racing to develop 
the most advanced algorithms to attract new users. The data linked to from the
course website represent data collected from the accelerometers from the 
Samsung Galaxy S smartphone. 

- A full description is available at the site where the data was obtained:  
　
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones
　

- Here are the data for the project:  

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
　
　
## Input
　
　
Data set: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 
　
　
## A Brief descriptioon of the R Script
　
　
`run_analysis.R`: this script takes the input data, and creates the output file 
　
The R script downloads and unzips the dataset from the above given URL.  The R script reads the test and training sets and merges them.  The mean and std features are extracted. The activity names for the activities are merged. A series of labeled columns to represent single variables from the feature are built up. The average of each variable is calculated and written into `tidy_data.txt`.
　
　
## Output
　
　
The output is written into a tidy dataset called `tidy_data.txt`.
　
　
## Code Book
　
`CodeBook.md` describes the variables, the data, and any transformation or work performed to clean up the original data.
