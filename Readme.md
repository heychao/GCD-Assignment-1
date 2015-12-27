# Readme
EC  
December 26, 2015  

##Getting and Cleaning Data Assignment 1

The run_analysis.R script uses **dplyr** and **tidyr** packages.


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(tidyr)
```

```
## Warning: package 'tidyr' was built under R version 3.2.3
```


First, the files with the dataset, the test subjects, and the activity labels are read into separate files.  Test and Training subjects are treate separately at first, and merged later.


```r
# read in data
x_test <- read.csv("./UCI HAR Dataset/test/X_test.txt", sep="", header=F)
y_test <- read.csv("./UCI HAR Dataset/test/Y_test.txt", sep="", header=F)
s_test <- read.csv("./UCI HAR Dataset/test/subject_test.txt", sep="", header=F)
      s_test <- rename(s_test,Subject=V1)
x_train <- read.csv("./UCI HAR Dataset/train/X_train.txt", sep="", header=F)
y_train <- read.csv("./UCI HAR Dataset/train/Y_train.txt", sep="", header=F)
s_train <- read.csv("./UCI HAR Dataset/train/subject_train.txt", sep="", header=F)
      s_train <- rename(s_train,Subject=V1)
```

The features (variables are read in from the supplied files) and activity coding table are read into separte files, each named accordingly.

```r
# read file that contains the names of all the columns
features <- read.csv("./UCI HAR Dataset/features.txt",sep="", header=F)
features$v2 <- as.character(features$V2)

# read file that defines activity codes
activity <- read.csv("./UCI HAR Dataset/activity_labels.txt", sep="", header=F)
```

The code below identify the column numbers of the variables that include mean and standard deviation in the variable names:

```r
# create a vector of columns of interest (mean and std)
mean_var <- grep("mean", features$v2)
std_var <- grep("std", features$v2)
mean_std <- c(mean_var, std_var) # combining into one vector
column_list <- sort(mean_std) # sorting to preserve original order 
```

Using the above derived data, we can put the appropriate names on the columns of the dataset.

```r
test_df <- data.frame("col1"=x_test[,column_list[1]])
train_df <- data.frame("col1"=x_train[,column_list[1]])

# create subset data tables for test and train sets
for(i in 2:length(column_list)){
      test_df <- cbind(test_df, x_test[,column_list[i]])
      train_df <- cbind(train_df, x_train[,column_list[i]])
}  

# apply features to variable names in the x... sets
      for(i in 1:length(column_list)){
            names(test_df)[i] <- features$v2[column_list[i]]
            names(train_df)[i] <- features$v2[column_list[i]]}
```

Next, we translate the numeric activity identifiers into corresponding text lables, based on the coding table contents:

```r
# translate activity codes into activity labels
      y_test_lab <- vector()
      y_train_lab <- vector()
     
      activity$V2 <-as.character(activity$V2)

      for(i in 1:nrow(y_test)){
            y_test_lab[i] <- activity$V2[y_test[i,1]]
      }

      for(i in 1:nrow(y_train)){
            y_train_lab[i] <- activity$V2[y_train[i,1]]
      }
```

Next, we combine the data frames containing subject, activity, and measurement data for each of the modes, training and test:

```r
# create dataframes containing activity labels and test/train modes 
      temp_y_df <-NULL
      temp_y_df <-data.frame (Activity=y_test_lab)
      test <- cbind(s_test, temp_y_df, test_df)
      
      temp_y_df <-NULL
      temp_y_df <-data.frame (Activity=y_train_lab)
      train <- cbind(s_train, temp_y_df, train_df)
```

Lastly, we combine the test and training tables:

```r
# Combining test and training datasets      
      samsung_df <-rbind(test,train)      
```

However, it turns out the the researcher supplied variable names contain characters that are confusing to R, so they cannot be efficiently used for referencin purposes.  We then rename all the measurement columns with names easier to deal with, coding-wise.

An ordered vector of alphanumeric names is generated to be used as temporary replacement names, and assigned to the combined data set:

```r
# Researcher generated variables are confusing R, so renaming with names easier to interpret
      
      # create a vector of temp variable names
            AlphaNumSeq <- function(alpha, start, end){
                  numvect <- c(start:end)
                  paste(alpha, numvect, sep="")
            }
      
            temp_var <- AlphaNumSeq("a", 1, length(column_list))
                              
      # apply temp variables to variable names in the samsung set
            for(i in 1:length(column_list)){
                  names(samsung_df)[i+2] <- temp_var[i]
            }
```

Next, we convert the data frame into a data frame tbl, to take advantage of the features of the dplyr package:

```r
      # transforming into a data frame tbl
      stbl <- tbl_df(samsung_df)
      
      # group by subject and activity
      by_sub_act <- group_by(samsung_df, Subject, Activity)
```

There are 79 data columns to take the mean of, so instead of typing all of them, we use a script to generate the string. The original data set had only 7 decimal places, so the tidy data set will be set to the same through the **round** function.

```r
      # use this expression to generate the columns of interest to calculate mean
      # (cut and paste the printed output into the summarise argument)
      # rounding to 7 digits, equal to those of the dataset elements
      
      means <- paste("round(mean(", temp_var, "),7), ", sep="")
      paste(means, collapse="")
```

```
## [1] "round(mean(a1),7), round(mean(a2),7), round(mean(a3),7), round(mean(a4),7), round(mean(a5),7), round(mean(a6),7), round(mean(a7),7), round(mean(a8),7), round(mean(a9),7), round(mean(a10),7), round(mean(a11),7), round(mean(a12),7), round(mean(a13),7), round(mean(a14),7), round(mean(a15),7), round(mean(a16),7), round(mean(a17),7), round(mean(a18),7), round(mean(a19),7), round(mean(a20),7), round(mean(a21),7), round(mean(a22),7), round(mean(a23),7), round(mean(a24),7), round(mean(a25),7), round(mean(a26),7), round(mean(a27),7), round(mean(a28),7), round(mean(a29),7), round(mean(a30),7), round(mean(a31),7), round(mean(a32),7), round(mean(a33),7), round(mean(a34),7), round(mean(a35),7), round(mean(a36),7), round(mean(a37),7), round(mean(a38),7), round(mean(a39),7), round(mean(a40),7), round(mean(a41),7), round(mean(a42),7), round(mean(a43),7), round(mean(a44),7), round(mean(a45),7), round(mean(a46),7), round(mean(a47),7), round(mean(a48),7), round(mean(a49),7), round(mean(a50),7), round(mean(a51),7), round(mean(a52),7), round(mean(a53),7), round(mean(a54),7), round(mean(a55),7), round(mean(a56),7), round(mean(a57),7), round(mean(a58),7), round(mean(a59),7), round(mean(a60),7), round(mean(a61),7), round(mean(a62),7), round(mean(a63),7), round(mean(a64),7), round(mean(a65),7), round(mean(a66),7), round(mean(a67),7), round(mean(a68),7), round(mean(a69),7), round(mean(a70),7), round(mean(a71),7), round(mean(a72),7), round(mean(a73),7), round(mean(a74),7), round(mean(a75),7), round(mean(a76),7), round(mean(a77),7), round(mean(a78),7), round(mean(a79),7), "
```
The string is then manually copied and pasted into the expression below to generate the calculations for the final table.

```r
      # generate the tidyset table
      tidyset <- summarise(by_sub_act, round(mean(a1),7), round(mean(a2),7), 
                           round(mean(a3),7), round(mean(a4),7), round(mean(a5),7), 
                           round(mean(a6),7), round(mean(a7),7), round(mean(a8),7), 
                           round(mean(a9),7), round(mean(a10),7), round(mean(a11),7), 
                           round(mean(a12),7), round(mean(a13),7), round(mean(a14),7), 
                           round(mean(a15),7), round(mean(a16),7), round(mean(a17),7), 
                           round(mean(a18),7), round(mean(a19),7), round(mean(a20),7), 
                           round(mean(a21),7), round(mean(a22),7), round(mean(a23),7), 
                           round(mean(a24),7), round(mean(a25),7), round(mean(a26),7), 
                           round(mean(a27),7), round(mean(a28),7), round(mean(a29),7), 
                           round(mean(a30),7), round(mean(a31),7), round(mean(a32),7), 
                           round(mean(a33),7), round(mean(a34),7), round(mean(a35),7), 
                           round(mean(a36),7), round(mean(a37),7), round(mean(a38),7), 
                           round(mean(a39),7), round(mean(a40),7), round(mean(a41),7), 
                           round(mean(a42),7), round(mean(a43),7), round(mean(a44),7), 
                           round(mean(a45),7), round(mean(a46),7), round(mean(a47),7), 
                           round(mean(a48),7), round(mean(a49),7), round(mean(a50),7), 
                           round(mean(a51),7), round(mean(a52),7), round(mean(a53),7), 
                           round(mean(a54),7), round(mean(a55),7), round(mean(a56),7), 
                           round(mean(a57),7), round(mean(a58),7), round(mean(a59),7), 
                           round(mean(a60),7), round(mean(a61),7), round(mean(a62),7), 
                           round(mean(a63),7), round(mean(a64),7), round(mean(a65),7), 
                           round(mean(a66),7), round(mean(a67),7), round(mean(a68),7), 
                           round(mean(a69),7), round(mean(a70),7), round(mean(a71),7), 
                           round(mean(a72),7), round(mean(a73),7), round(mean(a74),7), 
                           round(mean(a75),7), round(mean(a76),7), round(mean(a77),7), 
                           round(mean(a78),7), round(mean(a79),7))
```

Finally, the original variable names assigned by the researchers are put back into the table, replacing the temporary variable names for earlier.


```r
      # put the crazy variable names back into the table
      
      for(i in 1:length(column_list)){
            names(tidyset)[i+2] <- features$v2[column_list[i]]
      }
```

The contents of tidyset is saved into file tidydata.txt using the write.table function

```r
      write.table(tidyset, file="tidydata.txt", row.names=FALSE)
```
