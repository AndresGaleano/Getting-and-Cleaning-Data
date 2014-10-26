R Code: This file contains the R Code used for transforming the original Data Set (not provided) into the submitted Data Frame.

#### In this code, we will put together a collection of data bases and name them accordingly.
library(dplyr) ### We load al the required libraries, in this case only one

#### We set the working path, where all the data is located and load all the information we need
setwd("C:\\Users\\Andres\\Desktop\\U\\2014-2\\Data Science Specialization\\Getting and Cleaning Data\\UCI HAR Dataset\\")
Train<-read.table("X_train.txt") ### The measures extracted in each observation
Test<-read.table("X_test.txt")
Y_Train<-read.table("y_train.txt") ### The activity performed in each observation, not the name, only the id of the activity
Y_Test<-read.table("y_test.txt")
S_Train<-read.table("subject_train.txt") ### The subject of each observation
S_Test<-read.table("subject_test.txt")
Features<-read.table("features.txt") ### The name of each measures
Activities<-read.table("activity_labels.txt") ### The link between activity id and name


#### Next, we construct a data set which contains all the data of the subjects (measures, activity and subject ID)
#### We also label the activity ID with the activity names, provided in the Code Book
Data_set=rbind(cbind(S_Train,Y_Train,Train),cbind(S_Test,Y_Test,Test))
colnames(Data_set)[-c(1:2)]=as.character(Features[,"V2"])
colnames(Data_set)[1]=c("Subject")
Data_set=merge(Activities,Data_set,by="V1")
colnames(Data_set)[1:2]=c("Activity ID","ActivityName")

#### Afterwards, we create a Data Set with only the columns containing the mean and standard deviation of measures
Mean_SD=Data_set[,c(2,3,grep("mean()",colnames(Data_set),fixed=T),grep("std()",colnames(Data_set),fixed=T))]

#### We use the table data fram command to make it easier to work with
DF_Mean_SD=tbl_df(Mean_SD)

#### Finnally, we average each measure of mean and standard deaviation by subject and activity.
#### We also store the resulting data frame in a file called "FINAL_DF.txt".
FINAL_DF=group_by(DF_Mean_SD,Subject,ActivityName) %>% summarise_each("mean")
write.table(FINAL_DF,"FINAL_DF.txt",sep=";",row.name=FALSE)