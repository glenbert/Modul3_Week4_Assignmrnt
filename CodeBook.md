## load library
library(dplyr)

## Create Directory
if (!file.exists("module3")) {
  dir.create("module3")
}

## Download file

url <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"

download.file(url, destfile = "./module3/Data.zip")

##Unzip File
zipF <- "./module3/Data.zip"

outDir <- "./module3/Data"

unzip(zipF, exdir = outDir)

## Read data

xtestdt <- read.table("./module3/Data/UCI HAR Dataset/test/X_test.txt")
ytestdt <- read.table("./module3/Data/UCI HAR Dataset/test/y_test.txt")
subtestdt <- read.table("./module3/Data/UCI HAR Dataset/test/subject_test.txt")


xtraindt <- read.table("./module3/Data/UCI HAR Dataset/train/X_train.txt")
ytraindt <- read.table("./module3/Data/UCI HAR Dataset/train/X_train.txt")
subtraindt <- read.table("./data/sample/UCI HAR Dataset/train/subject_train.txt")

fetdt <- read.table("./module3/Data/UCI HAR Dataset/features.txt")
actdt <- read.table("./module3/Data/UCI HAR Dataset/activity_labels.txt")

## Merge all data

xdt <- rbind(xtestdt, xtraindt)
ydt <- rbind(ytestdt,ytraindt)
subdt <- rbind(subtestdt, subtraindt)
dt <- cbind(ydt, subdt, xdt)

## Extract Measurements
measdt <- fetdt[grep("\\mean\\b|\\std\\b", fetdt[,2]),2]
measdt <- as.character(measdt)

##Rename columns

colnames(dt) <- c("Act", "Sub", measdt )

## Remove "NA" columns
dt <- dt[!is.na(names(dt))]


## Label Activity

dt$Act <- factor(dt$Act, labels = as.character(actdt[,2]))

## Summarize data

meandt <- dt %>% group_by(Act, Sub) %>% summarize_all(funs(mean))

## Write table
write.table(meandt, "./module3/Data/UCI HAR Dataset/tidy.txt", row.names = FALSE, quote = FALSE)


