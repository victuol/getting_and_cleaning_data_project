getting_and_cleaning_data_project
=================================

This is the script used to create the tidy data set.

run_analysis<-function(){

		##First: we create a tidy data frame for the test part
			DF_TEST<-read_txt_files()

		##Second: we create a tidy data frame for the train part
			DF_TRAIN<-read_txt_files_train()

		##Third: we merge both of the data frames
			mergeDF<-rbind(DF_TEST,DF_TRAIN)

		##Fourth: We take the means of each row of the merged data frame
			final_table<-sapply(mergeDF,mean)

		##Fifth: We write a table with the tidy data frame
			write.table(final_table,"finaltable.txt",row.name=FALSE)
			

				}


read_txt_files<-function(){

##This function reads each .txt file, stores it as separate data frames, makes them tidy and finally, creates a tidy data frame

TEST_features<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/features.txt")

##Reading "test" folder

TEST_subject_test<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/subject_test.txt", sep="\t")
TEST_X_test<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/X_test.txt")
TEST_Y_test<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/y_test.txt")



##Reading "test->Intertial Signals" folder

TEST_Inertials_body_acc_x<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/body_acc_x_test.txt")
TEST_Inertials_body_acc_y<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/body_acc_y_test.txt")
TEST_Inertials_body_acc_z<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/body_acc_z_test.txt")

TEST_Inertials_body_gyro_x<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/body_gyro_x_test.txt")
TEST_Inertials_body_gyro_y<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/body_gyro_y_test.txt")
TEST_Inertials_body_gyro_z<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/body_gyro_z_test.txt")

TEST_Inertials_body_total_x<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/total_acc_x_test.txt")
TEST_Inertials_body_total_y<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/total_acc_y_test.txt")
TEST_Inertials_body_total_z<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/test/Inertial Signals/total_acc_z_test.txt")


##Naming each data frame
colnames(TEST_subject_test)<-"Subject_ID"
colnames(TEST_Y_test)<-"Activity_ID"
colnames(TEST_X_test)<-TEST_features$V2


##Extracting the Means and SD of X Test

index_Mean<-which(grepl("mean()",TEST_features$V2))
index_SD<-which(grepl("std()",TEST_features$V2))


names_Mean<-subsetStatsNames(index_Mean,as.character(TEST_features$V2))
names_SD<-subsetStatsNames(index_SD,as.character(TEST_features$V2))

DF_Mean<-subset(TEST_X_test,select=names_Mean)
DF_SD<-subset(TEST_X_test,select=names_SD)



##Making the list of data frames
TEST_Inertials_List<-list(TEST_Inertials_body_acc_x,TEST_Inertials_body_acc_y,TEST_Inertials_body_acc_z,TEST_Inertials_body_gyro_x,TEST_Inertials_body_gyro_y,TEST_Inertials_body_gyro_z,TEST_Inertials_body_total_x,TEST_Inertials_body_total_y,TEST_Inertials_body_total_z)


##Producing lists for means and SD of 128 signals in each measurement (body_acc_x, body_acc_y, etc.)
TEST_Inertials_List_mean<-lapply(TEST_Inertials_List,rowMeans)
TEST_Inertials_List_sd<-lapply(TEST_Inertials_List,rowSds)


##Doing data frames for means and sd of each measurement
dataframeMeans<-as.data.frame(TEST_Inertials_List_mean)
dataframeSD<-as.data.frame(TEST_Inertials_List_sd)

##Naming each column of the data frames of Means and SD of measurements
colnames(dataframeMeans)<-c("MEAN_body_acc_x","MEAN_body_acc_y","MEAN_body_acc_z","MEAN_body_gyro_x","MEAN_body_gyro_y","MEAN_body_gyro_z","MEAN_body_total_x","MEAN_body_total_y","MEAN_body_total_z")
colnames(dataframeSD)<-c("SD_body_acc_x","SD_body_acc_y","SD_body_acc_z","SD_body_gyro_x","SD_body_gyro_y","SD_body_gyro_z","SD_body_total_x","SD_body_total_y","SD_body_total_z")

			
##Making the new data frame for TEST part
TEST_DF<-cbind(TEST_subject_test,TEST_Y_test,DF_Mean,DF_SD,dataframeMeans,dataframeSD) 


return(TEST_DF)

##return (FINAL_DF)




}	



subsetStatsNames<-function(index,names){
			i<-1
			largo<-length(index)
			x<-vector("character", largo)
			while(i<=largo)
					{
					x[i]<-names[index[i]]
					i<-i+1
					}
			return (x)
			}

							
			

replaceActivityID<-function(Activity_ID){
				
				c<-c("WALKING","WALKING_UPSTAIRS","WALKING_DOWNSTAIRS","SITTING","STANDING","LAYING")
				
				largo<-length(Activity_ID)
				y<-vector("numeric", largo)
				i<-1
				
				while(i<=largo)
					{
						if(Activity_ID[i]==1)
						{
						y[i]<-c[1]
						}

						if(Activity_ID[i]==2)
						{
						y[i]<-c[2]
						}

						if(Activity_ID[i]==3)
						{
						y[i]<-c[3]
						}
				
						if(Activity_ID[i]==4)
						{
						y[i]<-c[4]
						}

						if(Activity_ID[i]==5)
						{
						y[i]<-c[5]
						}


						if(Activity_ID[i]==6)
						{
						y[i]<-c[6]
						}

					i<-i+1

					}
				return (y)
				}



read_txt_files_train<-function(){

##This function reads each .txt file and stores it as separate data frames in R

TRAIN_features<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/features.txt")

##Reading "train" folder

TRAIN_subject_test<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/subject_train.txt", sep="\t")
TRAIN_X_test<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/X_train.txt")
TRAIN_Y_test<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/y_train.txt")



##Reading "train->Intertial Signals" folder

TRAIN_Inertials_body_acc_x<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/body_acc_x_train.txt")
TRAIN_Inertials_body_acc_y<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/body_acc_y_train.txt")
TRAIN_Inertials_body_acc_z<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/body_acc_z_train.txt")

TRAIN_Inertials_body_gyro_x<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/body_gyro_x_train.txt")
TRAIN_Inertials_body_gyro_y<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/body_gyro_y_train.txt")
TRAIN_Inertials_body_gyro_z<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/body_gyro_z_train.txt")

TRAIN_Inertials_body_total_x<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/total_acc_x_train.txt")
TRAIN_Inertials_body_total_y<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/total_acc_y_train.txt")
TRAIN_Inertials_body_total_z<-read.table("C:/Users/MI PC/Desktop/Data Science/Getting and Cleaning Data/Course Project/UCI HAR Dataset/train/Inertial Signals/total_acc_z_train.txt")


##Naming each data frame
colnames(TRAIN_subject_test)<-"Subject_ID"
colnames(TRAIN_Y_test)<-"Activity_ID"
colnames(TRAIN_X_test)<-TRAIN_features$V2


##Selecting the Means and SD of X Test

index_Mean<-which(grepl("mean()",TRAIN_features$V2))
index_SD<-which(grepl("std()",TRAIN_features$V2))


names_Mean<-subsetStatsNames(index_Mean,as.character(TRAIN_features$V2))
names_SD<-subsetStatsNames(index_SD,as.character(TRAIN_features$V2))

DF_Mean<-subset(TRAIN_X_test,select=names_Mean)
DF_SD<-subset(TRAIN_X_test,select=names_SD)



##Making the list of data frames
TRAIN_Inertials_List<-list(TRAIN_Inertials_body_acc_x,TRAIN_Inertials_body_acc_y,TRAIN_Inertials_body_acc_z,TRAIN_Inertials_body_gyro_x,TRAIN_Inertials_body_gyro_y,TRAIN_Inertials_body_gyro_z,TRAIN_Inertials_body_total_x,TRAIN_Inertials_body_total_y,TRAIN_Inertials_body_total_z)


##Producing lists for means and SD of 128 signals in each measurement (body_acc_x, body_acc_y, etc.)
TRAIN_Inertials_List_mean<-lapply(TRAIN_Inertials_List,rowMeans)
TRAIN_Inertials_List_sd<-lapply(TRAIN_Inertials_List,rowSds)


##Doing data frames for means and sd of each measurement
dataframeMeans<-as.data.frame(TRAIN_Inertials_List_mean)
dataframeSD<-as.data.frame(TRAIN_Inertials_List_sd)

##Naming each column of the data frames of Means and SD of measurements
colnames(dataframeMeans)<-c("MEAN_body_acc_x","MEAN_body_acc_y","MEAN_body_acc_z","MEAN_body_gyro_x","MEAN_body_gyro_y","MEAN_body_gyro_z","MEAN_body_total_x","MEAN_body_total_y","MEAN_body_total_z")
colnames(dataframeSD)<-c("SD_body_acc_x","SD_body_acc_y","SD_body_acc_z","SD_body_gyro_x","SD_body_gyro_y","SD_body_gyro_z","SD_body_total_x","SD_body_total_y","SD_body_total_z")

			
##Making the new data frame for TRAIN part
TRAIN_DF<-cbind(TRAIN_subject_test,TRAIN_Y_test,DF_Mean,DF_SD,dataframeMeans,dataframeSD)



##Creating an Activity_Name vector to include in the data frame

##Activity_Class<-as.integer(TRAIN_DF$Activity_ID)
##Activity_Name<-replaceActivityID(Activity_Class)

##FINAL_DF<-cbind(Activity_Name,TRAIN_DF)


##return(TRAIN_DF)

##return (FINAL_DF)
 



return(TRAIN_DF)

##return(TEST_Inertials_List_sd)




}	



subsetStatsNames<-function(index,names){
			i<-1
			largo<-length(index)
			x<-vector("character", largo)
			while(i<=largo)
					{
					x[i]<-names[index[i]]
					i<-i+1
					}
			return (x)
			}			
							
			




				

