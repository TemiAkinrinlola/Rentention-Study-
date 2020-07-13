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

* Feature Scaling(standardization): Since the range of values of the raw data vary widely ,the objective function in classifier will not work properly without some sort of scaling or normalization.
