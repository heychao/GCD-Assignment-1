# Codebook
EC  
December 26, 2015  

##Getting and Cleaning Data Assignment 1

The *tidydata.txt* file contains information on 30% test subjects, 30 percent of which were subjected to training and 70% to testing activities.


Test subjects for training are identified as: 1, 3, 5, 6, 7, 8, 11, 14, 15, 16, 17, 19, 21, 22, 23, 25, 26, 27, 28, 29, 30.

Test subjects for test are identified as: 2, 4, 9, 10, 12, 13, 18, 20, 24.





There are 81 variables in the data set.  The first two are Subject and Activity, which identify the specific test subject and the mode of activity (described later) that the subject was engaged in.

The other 79 variable names of the data set are listed below:

```
## [1] tBodyAcc-mean()-X
## [1] tBodyAcc-mean()-Y
## [1] tBodyAcc-mean()-Z
## [1] tBodyAcc-std()-X
## [1] tBodyAcc-std()-Y
## [1] tBodyAcc-std()-Z
## [1] tGravityAcc-mean()-X
## [1] tGravityAcc-mean()-Y
## [1] tGravityAcc-mean()-Z
## [1] tGravityAcc-std()-X
## [1] tGravityAcc-std()-Y
## [1] tGravityAcc-std()-Z
## [1] tBodyAccJerk-mean()-X
## [1] tBodyAccJerk-mean()-Y
## [1] tBodyAccJerk-mean()-Z
## [1] tBodyAccJerk-std()-X
## [1] tBodyAccJerk-std()-Y
## [1] tBodyAccJerk-std()-Z
## [1] tBodyGyro-mean()-X
## [1] tBodyGyro-mean()-Y
## [1] tBodyGyro-mean()-Z
## [1] tBodyGyro-std()-X
## [1] tBodyGyro-std()-Y
## [1] tBodyGyro-std()-Z
## [1] tBodyGyroJerk-mean()-X
## [1] tBodyGyroJerk-mean()-Y
## [1] tBodyGyroJerk-mean()-Z
## [1] tBodyGyroJerk-std()-X
## [1] tBodyGyroJerk-std()-Y
## [1] tBodyGyroJerk-std()-Z
## [1] tBodyAccMag-mean()
## [1] tBodyAccMag-std()
## [1] tGravityAccMag-mean()
## [1] tGravityAccMag-std()
## [1] tBodyAccJerkMag-mean()
## [1] tBodyAccJerkMag-std()
## [1] tBodyGyroMag-mean()
## [1] tBodyGyroMag-std()
## [1] tBodyGyroJerkMag-mean()
## [1] tBodyGyroJerkMag-std()
## [1] fBodyAcc-mean()-X
## [1] fBodyAcc-mean()-Y
## [1] fBodyAcc-mean()-Z
## [1] fBodyAcc-std()-X
## [1] fBodyAcc-std()-Y
## [1] fBodyAcc-std()-Z
## [1] fBodyAcc-meanFreq()-X
## [1] fBodyAcc-meanFreq()-Y
## [1] fBodyAcc-meanFreq()-Z
## [1] fBodyAccJerk-mean()-X
## [1] fBodyAccJerk-mean()-Y
## [1] fBodyAccJerk-mean()-Z
## [1] fBodyAccJerk-std()-X
## [1] fBodyAccJerk-std()-Y
## [1] fBodyAccJerk-std()-Z
## [1] fBodyAccJerk-meanFreq()-X
## [1] fBodyAccJerk-meanFreq()-Y
## [1] fBodyAccJerk-meanFreq()-Z
## [1] fBodyGyro-mean()-X
## [1] fBodyGyro-mean()-Y
## [1] fBodyGyro-mean()-Z
## [1] fBodyGyro-std()-X
## [1] fBodyGyro-std()-Y
## [1] fBodyGyro-std()-Z
## [1] fBodyGyro-meanFreq()-X
## [1] fBodyGyro-meanFreq()-Y
## [1] fBodyGyro-meanFreq()-Z
## [1] fBodyAccMag-mean()
## [1] fBodyAccMag-std()
## [1] fBodyAccMag-meanFreq()
## [1] fBodyBodyAccJerkMag-mean()
## [1] fBodyBodyAccJerkMag-std()
## [1] fBodyBodyAccJerkMag-meanFreq()
## [1] fBodyBodyGyroMag-mean()
## [1] fBodyBodyGyroMag-std()
## [1] fBodyBodyGyroMag-meanFreq()
## [1] fBodyBodyGyroJerkMag-mean()
## [1] fBodyBodyGyroJerkMag-std()
## [1] fBodyBodyGyroJerkMag-meanFreq()
```

The average values and standard deviations of the collected data are presented.  

Variable names that start with t denote time domain signals measured at 50Hz sampling, and those that start with f denote frequency domain results of FFT of the t-variables.  

meanFreq(): Weighted average of the frequency components to obtain a mean frequency

The original researches describe the raw variables as:

"The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions."

These variables were obtained for 6 modes of activity:

```
## [1] WALKING
## [1] WALKING_UPSTAIRS
## [1] WALKING_DOWNSTAIRS
## [1] SITTING
## [1] STANDING
## [1] LAYING
```
