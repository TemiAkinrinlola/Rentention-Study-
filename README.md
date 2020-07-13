# Retention-Study-
## Employee Retention Classification Model:Figuring Out Which Employee May Quit


### MOTIVATION
According to Inc.Magazine,employee turnover is a major concern for employers-no matter the state of the economy.It is often disturbing ,time-consuming and expensive to deal with.Several studies have found that the total cost of losing an employee could range from tens of thousands of dollars to 1.5 -2X the position's annual salary.Apart from the price of hiring and on-boarding training ,there is the lost productivity and possible business errors.
As a result of these losses ,it has become imperative for business owner or business supervisor to be aware of the possibility of an employee quitting in order to take the necessary precautions or prepare for the dismissal.

This project investigates an obtained historical HR records datasets,analyses,and builds a predictive model to determine which employee might quit soon.

### DATA DESCRIPTION
The dataset used here is a combination of two seperate datasets (of shape-14999,12)  that cummulatively contain the follwing attributes:
* employee_id:This is a categorical that represents a unique identification number for each employee.
* number_of _projects:This is a numerical variable that describes the number of projects undertaken by individual employees
* average_monthly_hours :This is a numeric variable that describes the average amount of time(in hours) that each employee spent at work every month.
* time_spend_company:This is a numerical variable that represents overall time(in years) spent at the company since initial employment.
* work_accidents:This is a numerical variable that represents the number of accidents that each employee encountered at work.
* left: This is a categorical variable that represents whether an employee has left the company or not.This is indicated as either 1(for those who have left) or 0(for those who have not left).
* promotion_last_5years:This is a numerical variable that represents the the number of promotions that each employee has had in the past year.
* department:This is a categorical variable that describes the department of each employee at work.The unique departments include IT,marketing,accounting,R&D,support,HR,management,sales,product_management,and technical.
* salary: This categorical variable represents the salary of each employee and it could be represented by either of these categories: low,medium and high.
* satisfaction_level:This numerical variable represents the satisfaction level as indicated by each employeee.It is expressed as a percentage.
* last_evaluation :This numerical variable represents the score from the last evaluation of the employee.

### EXPLORATORY DATA ANALYSIS
It is important to note that the "left" attribute will represent the target variable of interest in building this model.

Exploratory analysis of the available dataset revealed some information about the dataset and they include:

*The dataset contains missings values.These exist in the satisfaction_level column and the last_evaluation column. 

![missing values](https://user-images.githubusercontent.com/67794705/87346751-f90ec280-c549-11ea-8f61-9d0bfed1221a.PNG)


* The dataset is imbalanced.This means that there is an unequal distribution of classes within a dataset and it could lead to overfitting in the classification model.This insight informs the choice of machine learning algorithm,evaluation metric or the need for resampling.

![imbalanced target variable](https://user-images.githubusercontent.com/67794705/87345280-c5cb3400-c547-11ea-9a14-4c08e23b0d61.PNG)

* The HR department has the highest number of people who have left in the past.

![retentionbydepartment](https://user-images.githubusercontent.com/67794705/87345284-c663ca80-c547-11ea-8bfa-d74c04facf33.png)

* More low-salary earners have left in the past than the other classes of earners.

![retention by salary](https://user-images.githubusercontent.com/67794705/87345283-c5cb3400-c547-11ea-8616-4a98467cd47e.png)

*There has been a fairly uniform level of satisfaction across the department.

![satisfactionbydepartment](https://user-images.githubusercontent.com/67794705/87345286-c6fc6100-c547-11ea-9db6-0b70aee919ca.png)

*The correlation matrix indicates that 

![correlationmatrix](https://user-images.githubusercontent.com/67794705/87345275-c5329d80-c547-11ea-9f52-103ff5915c35.png)

### DATA PREPARATION

Machine learning models are powerful but they impose certain requirements on the data.They often require data to be in a form that is different from how they are provided naturally,and some conversions will be necessary .Therefore,a data preparation phase often proceeds along with data understanding,in which data are manipulated and converted into forms that yield better results.
The data prepartion tasks involved in this table include:

* Dealing with missing values:Data can have missing values for several reasons such as observations that were not recorded and data corruption. Handling missing data is important as many machine learning algorithms do not support data with missing values.To address this problem,we fill the missing values with the mean values of the attributes.

![fillingup](https://user-images.githubusercontent.com/67794705/87347978-eeedc380-c54b-11ea-977b-226a54c9231d.PNG)

* Categorical Encoding: Most of the Machine learning algorithms can not handle categorical variables unless we convert them to numerical values. Many algorithm’s performances vary based on how Categorical variables are encoded.There are two common ways to perform categorical encoding ;label encoding and one hot encoding.Label encoding works best for ordinal categorical features while the one hot encoder works for non-ordinal categorical data.Given the type of available dataset,I employ the one hot encoding.

![ohe](https://user-images.githubusercontent.com/67794705/87349163-c5359c00-c54d-11ea-915c-7bf00d6d460a.PNG)

* Splitting the datasets into train and test sets:The Test dataset provides the gold standard used to evaluate the model. It is only used once a model is completely trained(using the train and validation sets). The test set is generally what is used to evaluate competing models.

* Feature Scaling(standardization): Since the range of values of the raw data vary widely ,the objective function in classifier will not work properly without some sort of scaling.Here ,I use the standardization or z-normaliztion to scale the features.

![standardization](https://user-images.githubusercontent.com/67794705/87352694-67a44e00-c553-11ea-9d3a-e8fcd0b98bd8.PNG)

### MODEL BUILDING

* Basline model: A baseline is the result of a very basic model/solution. You generally create a baseline and then try to make more complex solutions in order to get a better result. If you achieve a better score than the baseline, it is good.Here ,I used a logistic regression classifier model with default hyperparameters as our baseline.

![LR](https://user-images.githubusercontent.com/67794705/87353069-05981880-c554-11ea-90e4-e4f138813629.PNG)

* Prediction model: The prediction model of choice is the Random Forest Classifier.Random forests classifiers are an ensemble learning method for classification  that operate by constructing a multitude of decision trees at training time and outputting the class that is the mode of the classes (classification) of the individual trees. Random decision forests correct for decision trees' habit of overfitting to their training set.

Some of the RF hyperparameters include:

n_estimators = number of trees in the foreset
max_features = max number of features considered for splitting a node
max_depth = max number of levels in each decision tree
min_samples_split = min number of data points placed in a node before the node is split
min_samples_leaf = min number of data points allowed in a leaf node
bootstrap = method for sampling data points (with or without replacement)

Given the imbalance of the available dataset,RF classifier makes for a great choice.The model's hyperparameters were tuned with GridSearchCV to find the best possible model parameters.

### MODEL EVALUATION 
The model is evaluated on some unseen test data to assess the likely future performance of the model.If the model fits to the training data much better than it does the test data ,overfitting is a likely cause. The most frequent classification evaluation metric that is used is  ‘Accuracy’. You might believe that the model is good when the accuracy rate is 99%! However, it is not always true and can be misleading in some situations epecially in instances of imbalanced classification.F1-score is a better metric when there are imbalanced classes as in the this case.The F score is defined as the weighted harmonic mean of the test’s precision and recall.

The F1-score is used to measure a test’s accuracy, and it balances the use of precision and recall to do it. The F score can provide a more realistic measure of a test’s performance by using both precision and recall.

![PERFORMANCE](https://user-images.githubusercontent.com/67794705/87356505-16e42380-c55a-11ea-8503-a4e6e08af8fe.PNG)

The Random Forest Classifier performed excellently on this classification with a F1-score of 97.06.

### CONCLUSION 




