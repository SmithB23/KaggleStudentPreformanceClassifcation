# **Determine if Questions were Answered Correct in Learning Game**

# **Summary**: 
This repository holds an attempt to use a Gradient Boosted Trees Model to determine correctly answered questions within the Predict Student Performance from Game PLay Kaggle Dataset

https://www.kaggle.com/competitions/predict-student-performance-from-game-play/code


# **Overview**

The goal of the competitionis to use time series data generated by a learning game to determine if a player will answer a question correctly. This repository will be using Gradient Boosted Tree Models from tensor flow in this classification competition. Each question will be used to train its own model. My average accuracy was (unfinished). The best preforming kaggle competitor have an average accuracy of 75.6%.

# **Data**
We were given a test.csv, train.csv, and train_labels.csvfile to work with

The test file consisted of over 3,000 rows and 21 columns of generated data from the game

The train file consisted of over 26,000,000 rows and 20 columns of generated data from the game

The train_labels file consisted of over 400,000 rows and 2 columns of information deteriming right or wrong answers


Very important: There are 3 level groups. 0-4,5-12,13-22 Once a group of levels is finished certain questions will be asked. For example, after completing levels 0-4, you will be asked questions 1-3

Levels 0-4, question 1-3 Levels 5-12, question 4-13 Levels 13-22, question 14-18

There are a total of 18 questions Based on previous information of the session, we need to guess if the user got the question right.

train dataset: There were originally over 26 million rows but I lowered the amount of rows to 10 million as it was easier for my computer to handle. We start with 20 columns but we will be getting rid of columns with way too many missing values as well as values I have deemed not important to the machine-learning algorithm

Removed columns: Due to missing values: 'page', 'hover_duration', 'text', 'fqid', 'text_fqid' Due to my arbitrary reasoning (not being useful to the problem): 'index', 'fullscreen', 'hq', 'music'

Remaining Columns: 'session_id'- numerical(int64), 0 missing value ,the actual range of values not relevant 'elasped_time'- numerical(int32), 0 missing values, range is 1988601973 in milliseconds 'event_name'- categorical, 0 missing values 'name'- categorical, 0 missing values 'level'- numerical(uint8), 0 missing values, range is 22 'room_coor_x'- numerical(float32), 788253 missing values, range is 3249.56787109375 'room_coor_y'- numerical(float32), 788253 missing values, range is 1461.77880859375 'screen_coor_x'- numerical(float32), 788253 missing values, range is 1919.0 'screen_coor_y'- numerical(float32), 788253 missing values, range is 1919.0 'room_fqid'- categorical, 0 missing values 'level_group'- categorical, 0 missing values

Points to discuss: Class imbalances: Most categorical values have a significant imbalance between the categories

Missing values: As you can see with the x and y coordinates, based on the game room and screen, the amount of missing values is the same for each column, upon looking at the data set we see a trend. Whenever one of these is missing, so are all the others. This gives us the option of either removing all the null values or replacing all of them with the knowledge that 4 out of 11 columns would be identical for just under 800,000 of 10,000,000 rows. We have enough data to get rid of these rows. We can compare imputing the missing data and getting rid of the values later on.

Outliers: Upon a quick glance we can see their are some obvious outliers within multiple columns
    elapsed_time
    screen_coor_x
    screen_coor_y
We will scale the numerical columns using z-score and get rid of any values with a magnitude greater than 3
Prior to the removal of outliers, the shape of our dataset is (10000000,11)

train_labels: Gives the session_id along with the question that went along with it. Tells us if the questions were answered correctly Not much change needs to be made to this dataset

There are no missing values in the dataset

For easier use I s the session_id into session and question This will allow us to look at the specific question for each session Id

Columns: 'session_id'- object 'correct'- categorical, 1 or 0 'session'- numerical, range not super relevant 'q'- numerical, question number, range is 18

There is a class imbalance in the correct column (much more correct than incorrect)

No outliers

After splitting up the session_id column the shape is (424116, 4)

First we will look and understand the original training dataset. This is a classification, we will be using a random forest classification algorithm for this problem

# **Data visulaization within the coding segmant**

 **Train Dataset*
For the numerical values, before getting rid of outliers we can see that there are some obvious ones, however, we can seesome normal graphs as well
For the categorical values we can see there are high levels of class imbalance
![image](https://github.com/user-attachments/assets/ad68eaa3-8200-4ff9-aa1e-dbdcb48ab607)


**Train_Labels Dataset**
We can also see some high levels of class imbalance as there were much more correct answers than wrong.

## **Problem Formulation**

## **Training**

## **Performance Comparison**

## **Future Work**

# **How to Reproduce**
I personally wouldnt want to reproduce this

It was all done in one file
