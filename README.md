# Housing-Prediction

Step 1: Reading and Understanding the Data

Let us first import NumPy and Pandas and read the housing dataset

![image-1](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-1.JPG)

Inspect the various aspects of the housing dataframe

![image-2](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-2.JPG)


Step 2: Visualising the Data

Let's now spend some time doing what is arguably the most important step - understanding the data.

If there is some obvious multicollinearity going on, this is the first place to catch it
Here's where you'll also identify if some predictors directly have a strong association with the outcome variable

We'll visualise our data using matplotlib and seaborn.

![image-3](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-3.JPG)


Visualising Categorical Variables

As you might have noticed, there are a few categorical variables as well. Let's make a boxplot for some of these variables.

![image-4](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-4.JPG)

We can also visualise some of these categorical features parallely by using the hue argument. Below is the plot for furnishingstatus with airconditioning as the hue.

![image-5](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-5.JPG)


Step 3: Data Preparation

   You can see that your dataset has many columns with values as 'Yes' or 'No'.

   But in order to fit a regression line, we would need numerical values and not string. Hence, we need to convert them to 1s and 0s, where 1 is a 'Yes' and 0 is a 'No'.

![image-6](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-6.JPG)


Dummy Variables

The variable furnishingstatus has three levels. We need to convert these levels into integer as well.

For this, we will use something called dummy variables.

![image-7](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-7.JPG)

Now, you don't need three columns. You can drop the furnished column, as the type of furnishing can be identified with just the last two columns where —

   00 will correspond to furnished
   01 will correspond to unfurnished
   10 will correspond to semi-furnished

![image-8](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-8.JPG)


Step 4: Splitting the Data into Training and Testing Sets

As you know, the first basic step for regression is performing a train-test split.

![image-9](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-9.JPG)

Rescaling the Features

As you saw in the demonstration for Simple Linear Regression, scaling doesn't impact your model. Here we can see that except for area, all the columns have small integer values. So it is extremely important to rescale the variables so that they have a comparable scale. If we don't have comparable scales, then some of the coefficients as obtained by fitting the regression model might be very large or very small as compared to the other coefficients. This might become very annoying at the time of model evaluation. So it is advised to use standardization or normalization so that the units of the coefficients obtained are all on the same scale. As you know, there are two common ways of rescaling:

   Min-Max scaling
   Standardisation (mean-0, sigma-1)

This time, we will use MinMax scaling.

![image-10](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-10.JPG)

![image-11](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-11.JPG)

![image-12](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-12.JPG)

Dividing into X and Y sets for the model building

![image-13](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-13.JPG)


Step 5: Building a linear model

Fit a regression line through the training data using statsmodels. Remember that in statsmodels, you need to explicitly fit a constant using sm.add_constant(X) because if we don't perform this step, statsmodels fits a regression line passing through the origin, by default.
Adding all the variables to the model

![image-14](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-14.JPG)

![image-15](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-15.JPG)

Looking at the p-values, it looks like some of the variables aren't really significant (in the presence of other variables).

Maybe we could drop some?

We could simply drop the variable with the highest, non-significant p value. A better way would be to supplement this with the VIF information.
Checking VIF

Variance Inflation Factor or VIF, gives a basic quantitative idea about how much the feature variables are correlated with each other. It is an extremely important parameter to test our linear model. The formula for calculating VIF is:

![image-16](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-16.JPG)

We generally want a VIF that is less than 5. So there are clearly some variables we need to drop.

Dropping the variable and updating the model

As you can see from the summary and the VIF dataframe, some variables are still insignificant. One of these variables is, semi-furnished as it has a very high p-value of 0.938. Let's go ahead and drop this variables

![image-17](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-17.JPG)

![image-18](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-18.JPG)

Now as you can see, the VIFs and p-values both are within an acceptable range. So we go ahead and make our predictions using this model only.

Step 7: Residual Analysis of the train data

So, now to check if the error terms are also normally distributed (which is infact, one of the major assumptions of linear regression), let us plot the histogram of the error terms and see what it looks like.

![image-19](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-19.JPG)

Step 8: Making Predictions Using the Final Model

Now that we have fitted the model and checked the normality of error terms, it's time to go ahead and make predictions using the final, i.e. fourth model.

![image-20](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-20.JPG)

Step 9: Model Evaluation

Let's now plot the graph for actual versus predicted values.

![image-21](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-21.JPG)

We can see that the equation of our best fitted line is:

price=0.236×area+0.202×bathrooms+0.11×stories+0.05×mainroad+0.04×guestroom+0.0876×hotwaterheating+0.0682×airconditioning+0.0629×parking+0.0637×prefarea−0.0337×unfurnished

Overall we have a decent model, but we also acknowledge that we could do better.

We have a couple of options:

   Add new features (bathrooms/bedrooms, area/stories, etc.)
   Build a non-linear model
   
![image-22](https://github.com/hemangikinger/Housing-Prediction/blob/master/image-22.JPG)   



The features which affects the Housing Price Prediction:

    area
    bathrooms
    stories
    hotwaterheating
    airconditioning









