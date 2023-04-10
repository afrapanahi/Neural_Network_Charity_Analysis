# Neural_Network_Charity_Analysis

## Overview of Project 
In this project, I am using neural network to predict success rate for different funding applications. 
## Results
### 1. Data processing 
#### Cleaning the data:
-	Columns EIN and NAME were dropped because they are not correlated with the success rates therefore not features
-	Any application type with less than 526 counts were listed as  “others”
-	Any CLASSIFICATION with less than 1000 counts were considered as others
-	Using the onehot encoder, the categorical columns were converted to numeric values

Outcome:
![res1](/imgs/fig1.png?raw=true)


#### Features and target
-	IS_SUCCESS was chosen as the target
-	All other columns were considered as features
-	The data was scaled using Standardscale
-	The data was separated to training and testing sets
### 2. Compile, train and test the model
-	Model with 2 hidden layers and with 80 and 30 neurons in the first and second hidden layer was composed
Outcome: 
![res2](/imgs/fig2.png?raw=true)

-	The model was trained with 100 epochs
-	Checkpoint were saved every 5 steps
Outcome:
![res3](/imgs/fig3.png?raw=true)
### 3. Optimization
In order to increase the accuracy to 0.75 or higher, I made the following changes:
-	1. I decrease the cutoff for binning from 525 and 1000 to 200
-	2. A closer look at “ASK_AMT” column indicates that the values are heavily skewed. There are 25398 applications for $5000 funding while for other amounts the applications are very sparse (see the image below) Therefore, I decided to use log(‘ASK_AMT’) instead of ‘ASK_AMT’

![res4](/imgs/fig4.png?raw=true)

-	3. There are only 5 zero values in the column “STATUS”. Therefore, I dropped this column (See image below)
![res5](/imgs/fig5.png?raw=true)

-	4. I increased the number of hidden layers to 5
-	5. I increased the number of neurons in each layer
-	6. Given the nature of the data, I decided to use sigmoid activation function.
See image below:

![model](/imgs/opt_model.png?raw=true)

After applying all the changes mentioned above, here are the evaluations of the model for the training set.
1.	Change of accuracy with epoch

![res6](/imgs/fig6.png?raw=true)

2.	Change of loss with epoch

![res7](/imgs/fig7.png?raw=true)

## Summary 
Test set: The accuracy of the prediction for test set is slightly decreased after the optimization! I think making these changes overfitted the model to the training set. 

Before:
268/268 - 0s - loss: 0.5518 - accuracy: 0.7374 - 282ms/epoch - 1ms/step
Loss: 0.5517674684524536, Accuracy: 0.7373760938644409

After:
268/268 - 0s - loss: 0.6434 - accuracy: 0.7311 - 302ms/epoch - 1ms/step
Loss: 0.6433914303779602, Accuracy: 0.7310787439346313
 
To summarize, in this project, I worked with a data set that is very skewed. Perhaps we can pair the neural network model with PCA to reduce the dimensions. Also, perhaps we can use a different network model that adapts to the weight of each column and for those with less diversity, gives smaller weight.
