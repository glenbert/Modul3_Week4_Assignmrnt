# Module 3 Week 4 Assignment
## Getting and Cleanig Data Course Project

This project will present the summarize data in tidy data set. The downloaded zip file has different sets of data and variables needs to be merge with the given conditions to create a clean single data set and a summary. The R script must be called run_analysis.R and must be submitted in your Github repo.

### 1. Merges the training and the test sets to create one data set.

a. In the run_analysis.R create a directory to save the downloaded zip file.
b. Download the zip file and save it in the created directory.
c. unzip the file
d. Read all the following data using the read.table function;
    1. X_test.txt
    2. y_test.txt
    3. subject_test.txt
    4. X_train.txt
    5. X_train.txt
    6. subject_train.txt
    7. features.txt
    8. activity_labels.txt
e. Merge X_test.txt and X_train.txt , y_test.txt and X_train.txt and subject_test.txt and subject_train.txt  using rbind function. After merging the data set merge all the 3 new data set using cbind function. Now all are data are merge into single data set.

### 2. Extracts on the measurements on the mean and standard deviation for each measurement.

a. Extract the mean and standard deviation (std) in features.txt using grep, make sure to extract only the mean and std by using double backward      slash(\\) followed by "b" (ex. fetdt[grep("\\mean\\b|\\std\\b", fetdt[,2]),2])
b. Set the extracted features as character.

### 3. Uses descriptive activity names to name the activities in the data set

a. Rename the first column "act" , second column "sub" and the rest with the extracted measurements.
b. Remove column with "NA" to look more clean.

### 4. Appropriately labels the data set with descriptive variable names.

a. Label the act column with from the activity_labels.txt data set
b. And also set the act column as factor.

### 5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

a. Summarize the final and clean data set using group_by function of the libray "dplyr".
b. Save the summarize data with file name tidy.txt using write.table function.