Getting and Cleaning Data Course Assignment

Companies like FitBit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked are collected from the accelerometers from the Samsung Galaxy S smartphone.
A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The data is available at:
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

The aim of the project is to clean and extract usable data from the above zip file. R script called run_analysis.R that does the following: - Merges the training and the test sets to create one data set. - Extracts only the measurements on the mean and standard deviation for each measurement. - Uses descriptive activity names to name the activities in the data set - Appropriately labels the data set with descriptive variable names. - From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

In this project, you find:

run_analysis.R : the R-code run on the data set

Tidy.txt : the clean data extracted from the original data using run_analysis.R

CodeBook.md : the CodeBook reference to the variables in Tidy.txt

README.md : the analysis of the code in run_analysis.R

------------------------------------

Basic Assumption
The R code in run_analysis.R proceeds under the assumption that the zip file available
at https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip is downloaded and extracted in the R Home Directory.

Libraries Used
The libraries used in this operation are data.table and dplyr. 
We prefer data.table as it is efficient in handling large data as tables. dplyr is used to aggregate variables to create the tidy data.

Read Supporting Metadata
The supporting metadata in this data are the name of the features and the name of the activities. 
They are loaded into variables featureNames and activityLabels.

Format training and test data sets
Both training and test data sets are split up into subject, activity and features. They are present in three different files.

Part 1 - Merge the training and the test sets to create one data set
We can use combine the respective data in training and test data sets corresponding to subject, activity and features. 
The results are stored in subject, activity and features.

Naming the columns
The columns in the features data set can be named from the metadata in featureNames

Merge the data
The data in features,activity and subject are merged and the complete data is now stored in completeData

Part 2 - Extracts only the measurements on the mean and standard deviation for each measurement
Extract the column indices that have either mean or std in them.

dim(completeData)
## [1] 10299   563
Create extractedData with the selected columns in requiredColumns. And again, we look at the dimension of requiredColumns.
dim(extractedData)
## [1] 10299    88

Part 3 - Uses descriptive activity names to name the activities in the data set
The activity field in extractedData is originally of numeric type. 
We need to change its type to character so that it can accept activity names. The activity names are taken from metadata activityLabels.

Part 4 - Appropriately labels the data set with descriptive variable names
Here are the names of the variables in extractedData

names(extractedData)

[1] "tBodyAcc-mean()-X"                    "tBodyAcc-mean()-Y"                    "tBodyAcc-mean()-Z"                   
 [4] "tBodyAcc-std()-X"                     "tBodyAcc-std()-Y"                     "tBodyAcc-std()-Z"                    
 [7] "tGravityAcc-mean()-X"                 "tGravityAcc-mean()-Y"                 "tGravityAcc-mean()-Z"                
[10] "tGravityAcc-std()-X"                  "tGravityAcc-std()-Y"                  "tGravityAcc-std()-Z"                 
[13] "tBodyAccJerk-mean()-X"                "tBodyAccJerk-mean()-Y"                "tBodyAccJerk-mean()-Z"               
[16] "tBodyAccJerk-std()-X"                 "tBodyAccJerk-std()-Y"                 "tBodyAccJerk-std()-Z"                
[19] "tBodyGyro-mean()-X"                   "tBodyGyro-mean()-Y"                   "tBodyGyro-mean()-Z"                  
[22] "tBodyGyro-std()-X"                    "tBodyGyro-std()-Y"                    "tBodyGyro-std()-Z"                   
[25] "tBodyGyroJerk-mean()-X"               "tBodyGyroJerk-mean()-Y"               "tBodyGyroJerk-mean()-Z"              
[28] "tBodyGyroJerk-std()-X"                "tBodyGyroJerk-std()-Y"                "tBodyGyroJerk-std()-Z"               
[31] "tBodyAccMag-mean()"                   "tBodyAccMag-std()"                    "tGravityAccMag-mean()"               
[34] "tGravityAccMag-std()"                 "tBodyAccJerkMag-mean()"               "tBodyAccJerkMag-std()"               
[37] "tBodyGyroMag-mean()"                  "tBodyGyroMag-std()"                   "tBodyGyroJerkMag-mean()"             
[40] "tBodyGyroJerkMag-std()"               "fBodyAcc-mean()-X"                    "fBodyAcc-mean()-Y"                   
[43] "fBodyAcc-mean()-Z"                    "fBodyAcc-std()-X"                     "fBodyAcc-std()-Y"                    
[46] "fBodyAcc-std()-Z"                     "fBodyAcc-meanFreq()-X"                "fBodyAcc-meanFreq()-Y"               
[49] "fBodyAcc-meanFreq()-Z"                "fBodyAccJerk-mean()-X"                "fBodyAccJerk-mean()-Y"               
[52] "fBodyAccJerk-mean()-Z"                "fBodyAccJerk-std()-X"                 "fBodyAccJerk-std()-Y"                
[55] "fBodyAccJerk-std()-Z"                 "fBodyAccJerk-meanFreq()-X"            "fBodyAccJerk-meanFreq()-Y"           
[58] "fBodyAccJerk-meanFreq()-Z"            "fBodyGyro-mean()-X"                   "fBodyGyro-mean()-Y"                  
[61] "fBodyGyro-mean()-Z"                   "fBodyGyro-std()-X"                    "fBodyGyro-std()-Y"                   
[64] "fBodyGyro-std()-Z"                    "fBodyGyro-meanFreq()-X"               "fBodyGyro-meanFreq()-Y"              
[67] "fBodyGyro-meanFreq()-Z"               "fBodyAccMag-mean()"                   "fBodyAccMag-std()"                   
[70] "fBodyAccMag-meanFreq()"               "fBodyBodyAccJerkMag-mean()"           "fBodyBodyAccJerkMag-std()"           
[73] "fBodyBodyAccJerkMag-meanFreq()"       "fBodyBodyGyroMag-mean()"              "fBodyBodyGyroMag-std()"              
[76] "fBodyBodyGyroMag-meanFreq()"          "fBodyBodyGyroJerkMag-mean()"          "fBodyBodyGyroJerkMag-std()"          
[79] "fBodyBodyGyroJerkMag-meanFreq()"      "angle(tBodyAccMean,gravity)"          "angle(tBodyAccJerkMean),gravityMean)"
[82] "angle(tBodyGyroMean,gravityMean)"     "angle(tBodyGyroJerkMean,gravityMean)" "angle(X,gravityMean)"                
[85] "angle(Y,gravityMean)"                 "angle(Z,gravityMean)"                 "Activity"                            
[88] "Subject"                             

By examining extractedData, we can say that the following acronyms can be replaced:

1) Acc can be replaced with Accelerometer
2) Gyro can be replaced with Gyroscope
3) BodyBody can be replaced with Body
4) Mag can be replaced with Magnitude
5) Character f can be replaced with Frequency
6) Character t can be replaced with Time

Here are the names of the variables in extractedData after they are edited

 names(extractedData)
 [1] "TimeBodyAccelerometerMean()-X"                     "TimeBodyAccelerometerMean()-Y"                    
 [3] "TimeBodyAccelerometerMean()-Z"                     "TimeBodyAccelerometerSTD()-X"                     
 [5] "TimeBodyAccelerometerSTD()-Y"                      "TimeBodyAccelerometerSTD()-Z"                     
 [7] "TimeGravityAccelerometerMean()-X"                  "TimeGravityAccelerometerMean()-Y"                 
 [9] "TimeGravityAccelerometerMean()-Z"                  "TimeGravityAccelerometerSTD()-X"                  
[11] "TimeGravityAccelerometerSTD()-Y"                   "TimeGravityAccelerometerSTD()-Z"                  
[13] "TimeBodyAccelerometerJerkMean()-X"                 "TimeBodyAccelerometerJerkMean()-Y"                
[15] "TimeBodyAccelerometerJerkMean()-Z"                 "TimeBodyAccelerometerJerkSTD()-X"                 
[17] "TimeBodyAccelerometerJerkSTD()-Y"                  "TimeBodyAccelerometerJerkSTD()-Z"                 
[19] "TimeBodyGyroscopeMean()-X"                         "TimeBodyGyroscopeMean()-Y"                        
[21] "TimeBodyGyroscopeMean()-Z"                         "TimeBodyGyroscopeSTD()-X"                         
[23] "TimeBodyGyroscopeSTD()-Y"                          "TimeBodyGyroscopeSTD()-Z"                         
[25] "TimeBodyGyroscopeJerkMean()-X"                     "TimeBodyGyroscopeJerkMean()-Y"                    
[27] "TimeBodyGyroscopeJerkMean()-Z"                     "TimeBodyGyroscopeJerkSTD()-X"                     
[29] "TimeBodyGyroscopeJerkSTD()-Y"                      "TimeBodyGyroscopeJerkSTD()-Z"                     
[31] "TimeBodyAccelerometerMagnitudeMean()"              "TimeBodyAccelerometerMagnitudeSTD()"              
[33] "TimeGravityAccelerometerMagnitudeMean()"           "TimeGravityAccelerometerMagnitudeSTD()"           
[35] "TimeBodyAccelerometerJerkMagnitudeMean()"          "TimeBodyAccelerometerJerkMagnitudeSTD()"          
[37] "TimeBodyGyroscopeMagnitudeMean()"                  "TimeBodyGyroscopeMagnitudeSTD()"                  
[39] "TimeBodyGyroscopeJerkMagnitudeMean()"              "TimeBodyGyroscopeJerkMagnitudeSTD()"              
[41] "FrequencyBodyAccelerometerMean()-X"                "FrequencyBodyAccelerometerMean()-Y"               
[43] "FrequencyBodyAccelerometerMean()-Z"                "FrequencyBodyAccelerometerSTD()-X"                
[45] "FrequencyBodyAccelerometerSTD()-Y"                 "FrequencyBodyAccelerometerSTD()-Z"                
[47] "FrequencyBodyAccelerometerMeanFreq()-X"            "FrequencyBodyAccelerometerMeanFreq()-Y"           
[49] "FrequencyBodyAccelerometerMeanFreq()-Z"            "FrequencyBodyAccelerometerJerkMean()-X"           
[51] "FrequencyBodyAccelerometerJerkMean()-Y"            "FrequencyBodyAccelerometerJerkMean()-Z"           
[53] "FrequencyBodyAccelerometerJerkSTD()-X"             "FrequencyBodyAccelerometerJerkSTD()-Y"            
[55] "FrequencyBodyAccelerometerJerkSTD()-Z"             "FrequencyBodyAccelerometerJerkMeanFreq()-X"       
[57] "FrequencyBodyAccelerometerJerkMeanFreq()-Y"        "FrequencyBodyAccelerometerJerkMeanFreq()-Z"       
[59] "FrequencyBodyGyroscopeMean()-X"                    "FrequencyBodyGyroscopeMean()-Y"                   
[61] "FrequencyBodyGyroscopeMean()-Z"                    "FrequencyBodyGyroscopeSTD()-X"                    
[63] "FrequencyBodyGyroscopeSTD()-Y"                     "FrequencyBodyGyroscopeSTD()-Z"                    
[65] "FrequencyBodyGyroscopeMeanFreq()-X"                "FrequencyBodyGyroscopeMeanFreq()-Y"               
[67] "FrequencyBodyGyroscopeMeanFreq()-Z"                "FrequencyBodyAccelerometerMagnitudeMean()"        
[69] "FrequencyBodyAccelerometerMagnitudeSTD()"          "FrequencyBodyAccelerometerMagnitudeMeanFreq()"    
[71] "FrequencyBodyAccelerometerJerkMagnitudeMean()"     "FrequencyBodyAccelerometerJerkMagnitudeSTD()"     
[73] "FrequencyBodyAccelerometerJerkMagnitudeMeanFreq()" "FrequencyBodyGyroscopeMagnitudeMean()"            
[75] "FrequencyBodyGyroscopeMagnitudeSTD()"              "FrequencyBodyGyroscopeMagnitudeMeanFreq()"        
[77] "FrequencyBodyGyroscopeJerkMagnitudeMean()"         "FrequencyBodyGyroscopeJerkMagnitudeSTD()"         
[79] "FrequencyBodyGyroscopeJerkMagnitudeMeanFreq()"     "Angle(TimeBodyAccelerometerMean,Gravity)"         
[81] "Angle(TimeBodyAccelerometerJerkMean),GravityMean)" "Angle(TimeBodyGyroscopeMean,GravityMean)"         
[83] "Angle(TimeBodyGyroscopeJerkMean,GravityMean)"      "Angle(X,GravityMean)"                             
[85] "Angle(Y,GravityMean)"                              "Angle(Z,GravityMean)"                             
[87] "Activity"                                          "Subject"                                

Part 5 - From the data set in step 4, 
creates a second, independent tidy data set with the average of each variable for each activity and each subject

set Subject as a factor variable
extractedData$Subject <- as.factor(extractedData$Subject)
extractedData <- data.table(extractedData)

We create tidyData as a data set with average for each activity and subject. Then, order the enties in tidyData 
and write it into data file Tidy.txt that contains the processed data.

tidyData <- aggregate(. ~Subject + Activity, extractedData, mean)
tidyData <- tidyData[order(tidyData$Subject,tidyData$Activity),]
write.table(tidyData, file = "Tidy.txt", row.names = FALSE)

