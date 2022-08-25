# Project 2
# Ames Housing Dataset and Multivariate Regression

## Contents
##### - Problem Statement
##### - Data Description
##### - Data Cleaning/Feature Engineering
##### - Preliminary Modeling
##### - Final Model/Conclusion


### Problem Statement
Accurately pricing a home is critical for listing agents, as overpricing a home can result in that house sitting unsold on the market for extended periods of time, and underpricing a home can result in unrealized gains for the seller. Our goal is to create a model that will accurately price a home in Ames, Iowa so that listing agents can quickly and easily obtain a base price for listing the properties that they are responsible for based on the physical characteristics of the property. 


### Data Description
We were provided with a dataset by the Ames Assessor's Office, which details physical characteristics of homes sold in Ames, Iowa between 2006 and 2010. The dataset includes 82 columns and 2930 observations with 23 nominal variables, 23 ordinal variables, 14 discrete variables, and 20 continuous variables (data dictionary here: http://jse.amstat.org/v19n3/decock/DataDocumentation.txt). 


### Data Cleaning and Feature Engineering
When I received this dataset, there were 13,993 observations across the 82 columns that were either missing, or null. After examining the data dictionary, it became apparent that many of the "null" values actually indicated that a specific property did not have the feature that the column was indicating. After remedying this, I went on to consolidate like variables, for example Bsmt Full Bath (Which indicates the number of full bathrooms in the basement) and Full Bath (which represents the number of full bathrooms in the houseabove grade). For many of the ordinal categorical variables, if the variable appeared to have an impact on housing price, I would assign the observation a 1 if the property had received a grade better than "Typical/Average". Once the dataset had been cleaned and all variables consolidated and converted to numeric type, I moved on to modeling. 


### Preliminary Modeling
The first model that I created included all of the cleaned/feature engineered variables I had created in order to get a baseline performance to compare all future models to. This model predicted sale price based on 74 input variables. with 95% confidence, the testing R2 value for this model is between 0.87 and 0.91. This was a relatively high R2 value for the initial model, but the model consitently undervalued more expensive houses. 

For the second model, I ussed Lasso regression to identify unnecessary variables and zero out the coefficients associated with those variables. This model zeroed out 9 terms, leaving us with 65 predictors of sale price. This model performed similarly to the initial model, with 95% confidence the R2 value for this model is between 0.88 and 0.91

For the third model I used Ridge regression, including all of the initial 74 variables. This model displayed the best performance so far in terms of its RMSE score on the testing data, but left far too many variables in play to be a particularly useful model for wider application. With 95% confidence, the R2 value for this model is between 0.88 and 0.91.

Next I wanted to see what happened if I manually dropped all variables with low correlation values (arbitrarily selected |0.2| as the cutoff). This left me with 28 input variables, and with 95% confidence the R2 value for this model is between 0.86 and 0.90. This model performed slightly worse than the Ridge model in terms of its RMSE score on the testing data, but after dropping more than half of my variables and only seeing a slight decrease in performance in terms of R2, I was interested in exploring this new reduced model further. 


### Conclusions (Final Model) and Next Steps
For my final model, I elected to utilize interaction terms between the 5 variables with the highest correlation with sale price. This added 15 variables, increasing my number of input variables to 43. This model, with 95% confidence, has a R2 value of between 0.89 and 0.93. Most importantly, once I included the interaction terms the model no longer consistently undervalued the most expensive houses in the dataset. When applied to the testing data, this model models predictions were on average $23,300 off of the actual sale price. 

This model performed well on the majority the testing data, and while the predictions were not 100% accurate, this model would be useful for listing agents seeking to select an initial listing price for their properties. It should be noted that this model performs slightly worse on houses in Ames that sell for an excess of $450,000.

Perhaps the largest shortcoming of this model is that it does not account for three of the biggest contributors to sale price: location, location, and location. While the dataset does denote what neighborhood each observation is in, it lacks a lot of the specifics that contribute to housing price. The closest it comes is the "Condition 1" and "Condition 2" variables which indicate whether a house is close to a large street, a railroad, or a park. Homebuyers frequently consider whether a house is close to a grocery store, parks, public transit, and many other features that might increase or decrease the value of a home substantially. 

While difficult, if I were to continue this project I would like to do some research and attempt to include some more specific location variables that might improve the accuracy of my predictions. Additionally, there are a large variety of combinations of interaction terms that I was unable to consider given the limited time I was able to spend on the modeling section of this project. I would like to examine more potential interaction terms and see if there are any that help to explain the high sale prices that certain houses fetch. 