## Code Book for Getting and Cleaning Data Project  

### Overview

[Source] (https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip) of the original data:

	https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

[Full Description]
(http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones) at the site where the data was obtained:

	http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones
	
### Process

The R script `run_analysis.R` performs the following steps to clean up the data
and create a tidy data sets:

#### Download zip file.
`if(!file.exists("D:/Coursera/data.zip")) {
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl, destfile = "D:/Coursera/data.zip")
} else {
  unzip("D:/Coursera/data.zip")
}`

#### Set working directory.
`setwd("D:/Coursera/UCI HAR Dataset/")`

#### Load required packages. 
`library(data.table)
library(reshape2)`

#### Load activity labels. They are stored in column 2 of activity_labels.txt file.
`activity_labels <- read.table("D:/Coursera/UCI HAR Dataset/activity_labels.txt")[,2]`

#### Load data column names. They are stored in column 2 of features.txt file.
`features <- read.table("D:/Coursera/UCI HAR Dataset/features.txt")[,2]`

#### Use grepl() function to extract only the mean and standard deviation measurements.
`mean_std <- grepl("mean|std", features)`

#### Load data from X_test.txt, y_test.txt, and subject_test.txt files.
`X_test <- read.table("D:/Coursera/UCI HAR Dataset/test/X_test.txt")
y_test <- read.table("D:/Coursera/UCI HAR Dataset/test/y_test.txt")
subject_test <- read.table("D:/Coursera/UCI HAR Dataset/test/subject_test.txt")`

#### Use names() function to get the names from features table.
`names(X_test) <- features`

#### Extract only the mean and standard deviation for each measurement.
`X_test <- X_test[ ,mean_std]`

#### Load activity labels from y_test.txt file.
`y_test[ ,2] <- activity_labels[y_test[ ,1]]`

#### Use names() function to set the names. 
`names(y_test) <- c("Activity_ID", "Activity_Label")
names(subject_test) <- "subject"`

#### Use cbind() function to bind data by columns.
`test_data <- cbind(as.data.table(subject_test), y_test, X_test)`

#### Load training data from X_train.txt, y_train.txt, and subject_train.txt files.
`X_train <- read.table("D:/Coursera/UCI HAR Dataset/train/X_train.txt")
y_train <- read.table("D:/Coursera/UCI HAR Dataset/train/y_train.txt")
subject_train <- read.table("D:/Coursera/UCI HAR Dataset/train/subject_train.txt")`

#### Use names() function to get the names from features table.
`names(X_train) <- features`

#### Extract only the mean and standard deviation for each measurement.
`X_train <- X_train[ ,mean_std]`

#### Load activity data.
`y_train[ ,2] <- activity_labels[y_train[ ,1]]`

#### Use names() function to set the names
`names(y_train) <- c("Activity_ID", "Activity_Label")
names(subject_train) <- "subject"`

#### Use cbind() function to bind data by columns.
`train_data <- cbind(as.data.table(subject_train), y_train, X_train)`

#### Use rbind() function to merge test and train data by rows.
`data <- rbind(test_data, train_data)`

#### Use c() function on "subject", "Activity_ID", and "Activity_Label" to create Labels_ID vector.
`Labels_ID <- c("subject", "Activity_ID", "Activity_Label")`

#### Use setdiff() function to set difference of subsets. 
#### The elements of setdiff(colnames(data), Labels_ID) are those elements in colnames(data) but not in Labels_ID.
`labels_data <- setdiff(colnames(data), Labels_ID)`

#### Use melt() function to melt data so that each row is a unique id-variable combination.
#### melt () function takes wide-format data and melts it into long-format data.
`melt_data <- melt(data, id = Labels_ID, measure.vars = labels_data)`

#### Use dcast() function from reshape2 package to apply mean function to dataset to create tidy data.
`tidy_data <- dcast(melt_data, subject + Activity_Label ~ variable, mean)`

#### Use write.table() function to create tidy_data.txt file.
`write.table(tidy_data, file = "D:/Coursera/UCI HAR Dataset/tidy_data.txt", row.name=FALSE)`

#### The data frame X_test consists of 2947 rows and 79 columns.
#### The data frame y_test consists of 2947 rows and 2 columns.
#### The data frame X_train consists of 7352 nrows and 79 columns.
#### The data frame y_train consists of 7352 nrows and 2 columns.
#### The data frame tidy_data consists of 180 rows and 81 columns.
#### The first two column names in tidy_data are: subject and Activity_Label.
