# load libraries
library(data.table)
library(dplyr)

filename <- "getdata_dataset.zip"

# downloading the data
if (!file.exists(filename)){
  fileURL <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip "
  download.file(fileURL, filename, method="curl")
}  
if (!file.exists("UCI HAR Dataset")) { 
  unzip(filename) 
}

subjectTrain <- read.table("UCI HAR Dataset/train/subject_train.txt", header = FALSE)
yTrain <- read.table("UCI HAR Dataset/train/y_train.txt", header = FALSE)
xTrain <- read.table("UCI HAR Dataset/train/X_train.txt", header = FALSE)

subjectTest <- read.table("UCI HAR Dataset/test/subject_test.txt", header = FALSE)
xTest <- read.table("UCI HAR Dataset/test/y_test.txt", header = FALSE)
yTest <- read.table("UCI HAR Dataset/test/X_test.txt", header = FALSE)

features <- rbind(xTrain, xTest)
subject <- rbind(subjectTrain, subjectTest)
activity <- rbind(yTrain, yTest)

# Merging the training and the test sets to create one data set
colnames(subject) <- "Subject"
colnames(activity) <- "Activity"
FinalData <- cbind(features,activity,subject)

# Extracting only the measurements on the mean and standard deviation for each measurement
head(select(mean|SD,names(FinalData)), na.rm = TRUE
 
# create second independent tiny data
extractedData$Subject <- as.factor(extractedData$Subject)
extractedData <- data.table(extractedData)

tidyData <- aggregate(. ~Subject + Activity, extractedData, mean)
tidyData <- tidyData[order(tidyData$Subject,tidyData$Activity),]
write.table(tidyData, file = "Tidy.txt", row.names = FALSE)
