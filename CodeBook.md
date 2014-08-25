getting_and_cleaning_data_project
=================================

This repo contains 1) a tidy data set, 2) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md and, 3) a README.md with the scripts.

Tidy Data Set Description:

There are 99 variables contained in the Data Frame:

[1] "Subject_ID"                      "Activity_ID"                    
 [3] "tBodyAcc-mean()-X"               "tBodyAcc-mean()-Y"              
 [5] "tBodyAcc-mean()-Z"               "tGravityAcc-mean()-X"           
 [7] "tGravityAcc-mean()-Y"            "tGravityAcc-mean()-Z"           
 [9] "tBodyAccJerk-mean()-X"           "tBodyAccJerk-mean()-Y"          
[11] "tBodyAccJerk-mean()-Z"           "tBodyGyro-mean()-X"             
[13] "tBodyGyro-mean()-Y"              "tBodyGyro-mean()-Z"             
[15] "tBodyGyroJerk-mean()-X"          "tBodyGyroJerk-mean()-Y"         
[17] "tBodyGyroJerk-mean()-Z"          "tBodyAccMag-mean()"             
[19] "tGravityAccMag-mean()"           "tBodyAccJerkMag-mean()"         
[21] "tBodyGyroMag-mean()"             "tBodyGyroJerkMag-mean()"        
[23] "fBodyAcc-mean()-X"               "fBodyAcc-mean()-Y"              
[25] "fBodyAcc-mean()-Z"               "fBodyAcc-meanFreq()-X"          
[27] "fBodyAcc-meanFreq()-Y"           "fBodyAcc-meanFreq()-Z"          
[29] "fBodyAccJerk-mean()-X"           "fBodyAccJerk-mean()-Y"          
[31] "fBodyAccJerk-mean()-Z"           "fBodyAccJerk-meanFreq()-X"      
[33] "fBodyAccJerk-meanFreq()-Y"       "fBodyAccJerk-meanFreq()-Z"      
[35] "fBodyGyro-mean()-X"              "fBodyGyro-mean()-Y"             
[37] "fBodyGyro-mean()-Z"              "fBodyGyro-meanFreq()-X"         
[39] "fBodyGyro-meanFreq()-Y"          "fBodyGyro-meanFreq()-Z"         
[41] "fBodyAccMag-mean()"              "fBodyAccMag-meanFreq()"         
[43] "fBodyBodyAccJerkMag-mean()"      "fBodyBodyAccJerkMag-meanFreq()" 
[45] "fBodyBodyGyroMag-mean()"         "fBodyBodyGyroMag-meanFreq()"    
[47] "fBodyBodyGyroJerkMag-mean()"     "fBodyBodyGyroJerkMag-meanFreq()"
[49] "tBodyAcc-std()-X"                "tBodyAcc-std()-Y"               
[51] "tBodyAcc-std()-Z"                "tGravityAcc-std()-X"            
[53] "tGravityAcc-std()-Y"             "tGravityAcc-std()-Z"            
[55] "tBodyAccJerk-std()-X"            "tBodyAccJerk-std()-Y"           
[57] "tBodyAccJerk-std()-Z"            "tBodyGyro-std()-X"              
[59] "tBodyGyro-std()-Y"               "tBodyGyro-std()-Z"              
[61] "tBodyGyroJerk-std()-X"           "tBodyGyroJerk-std()-Y"          
[63] "tBodyGyroJerk-std()-Z"           "tBodyAccMag-std()"              
[65] "tGravityAccMag-std()"            "tBodyAccJerkMag-std()"          
[67] "tBodyGyroMag-std()"              "tBodyGyroJerkMag-std()"         
[69] "fBodyAcc-std()-X"                "fBodyAcc-std()-Y"               
[71] "fBodyAcc-std()-Z"                "fBodyAccJerk-std()-X"           
[73] "fBodyAccJerk-std()-Y"            "fBodyAccJerk-std()-Z"           
[75] "fBodyGyro-std()-X"               "fBodyGyro-std()-Y"              
[77] "fBodyGyro-std()-Z"               "fBodyAccMag-std()"              
[79] "fBodyBodyAccJerkMag-std()"       "fBodyBodyGyroMag-std()"         
[81] "fBodyBodyGyroJerkMag-std()"      "MEAN_body_acc_x"                
[83] "MEAN_body_acc_y"                 "MEAN_body_acc_z"                
[85] "MEAN_body_gyro_x"                "MEAN_body_gyro_y"               
[87] "MEAN_body_gyro_z"                "MEAN_body_total_x"              
[89] "MEAN_body_total_y"               "MEAN_body_total_z"              
[91] "SD_body_acc_x"                   "SD_body_acc_y"                  
[93] "SD_body_acc_z"                   "SD_body_gyro_x"                 
[95] "SD_body_gyro_y"                  "SD_body_gyro_z"                 
[97] "SD_body_total_x"                 "SD_body_total_y"                
[99] "SD_body_total_z"

The main transformations of data were:

1. It was neccesary to paste the features file as the column names of X_test (train and Test, respectively)
2. It was neccesary to average the measurements (128), obtaining means (MEAN_body_acc... etc.) and SD (SD_body_acc... etc.)
