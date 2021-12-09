# Predicting-Ames-Housing-Prices

Problem Statement
---
The Bluth Company, a real estate development firm, wants to develop properties in Ames, Iowa, and they want to find out which features of a property helps increase revenue, and to what extent.

In this project, I will be using housing data from Ames, Iowa, collected between 2006 and 2010 to build a Linear Regression model which we can use to interpret which features affect revenue the most. The model will also be able to predict the sale price of a house after the Bluth Company decides on what features to build.

The model will be evaluated by calculating the Root Mean Squared Error (RMSE). RMSE was chosen because we want to penalise large errors, and also for the value to have the same units as the target variable (Sale Price), e.g. if the RMSE is 20,000, it means the predictions are about $20,000 away from the actual value. The lower the RMSE, the more accurate the model.

Executive Summary
---
This project is part of a Kaggle challenge. It explores the housing data of Ames, Iowa, for properties sold between 2006 to 2010. The dataset includes information on various features of the property, and some characteristics of each sale.

First, Exploratory Data Analysis (EDA) was performed to explore the relationship between the various data points in the dataset and the sale price. Using the Pearson's correlation coefficient, we identified 11 features that had a strong correlation to the sale price. Upon analysing the data further, we found out that some of the features were strongly correlated to each other, and this would introduce mutlicollinearity into the model training if not corrected. Such features were therefore dropped to prevent multicollinearity. The feature that was dropped from each pair of highly correlated features is the feature that is less strongly correlated to sale price. Missing values were then imputed with the appropriate values and categorical data was dummy encoded.

Next, as the sale price had a positively skewed distribution, we performed a log transformation to normalize the sale price distribution. Thereafter, the data was split into a train set (80% of data) and a test set (20%). We trained 3 models in total, Linear Regression, Ridge Regression and Lasso Regression. The Linear Regression model's scores indicated that it was not suitable for use, and that regularization via Ridge or Lasso was required. Model selection was then done by comparing the 5-fold cross-validated scores and the Root Mean Square Error (RMSE) between the Ridge Regression and Lasso Regression. The Lasso Regression model was selected despite Ridge Regression having a better RMSE, as the Lasso Regression is able to eliminate unimportant features, and also because the Lasso Regression had a higher 5-fold cross-validated score, which likely indicates that it would more representative of future data than Ridge Regression.

The 5 features that positively affected the sale price the most were found to be the above ground living area, overall quality, year built, overall condition and finished basement area. Not a surprising result, as these 5 features were identified earlier during EDA. Recommendations were then made based on the Lasso Regression coefficients of the top 5 and bottom 5 features.

Data Documentation
---
Data documentation available [here](../datasets/DataDocumentation.txt)

Model Scores
---
| Model                      | 5-fold  Cross-Validated Train score | 5-fold  Cross-Validated Test score | Root Mean  Square Error |
|----------------------------|-------------------------------------|------------------------------------|-------------------------|
| Baseline/Linear regression | -9.10e21                            | -4.17e23                           | NA                      |
| Ridge regression           | 0.909                               | 0.878                              | 18684.45                |
| Lasso regression           | 0.913                               | 0.881                              | 18769.72                |

Conclusion & Recommendation
---
The model we trained is able to predict the sale price of houses within \\$18,769.72. The model does well in predicting sale prices between \\$75,000 and \$300,000. If there is a need to predict prices outside of that range, the model will need to be improved by either providing more training data with prices outside of the range or implementing other models/modelling techniques.

Based on the selected model, we are able to find out the 5 features that positively affects the sale price the most and the 5 features that negatively affects the sale price the most based on the coefficients of the model. The interpretation of the coefficient is as follows: 

Holding everything else constant,<br>
For every unit increase in squarefeet of **Gr Liv Area**, the sale price will **increase** by \$24,955.56<br>
For each grade increase in **Overall Qual**, the sale price will  **increase** by \$15303.41 <br>
For each unit increase in **Year Built**, the sale price will  **increase** by \$9830.00 <br>
For each grade increase in **Overal Cond**, the sale price will **increase** by \$7073.31 <br>
For every unit increase in squarefeet of **BsmtFin SF 1**, the sale price will  **increase** by \$6324.80 <br>
Having the house zoned as Commercial in **MS Zoning**, will **decrease** the sale price by \$3037.59 <br>
Having Wall Furnace **Heating**, will **decrease** the sale price by \$2072.30 <br>
Having the class categorised in **MS SubClass** as a 2-storey planned unit development (PUD), built in 1946 or after, will **decrease** the sale price by \$1858.78 <br>
Having the house in Meadow Village **Neighborhood**, will **decrease** the sale price by \$1737.86 <br>
Having Mansard **Roof Style**, will **decrease** the sale price by \$1617.61

Therefore, for the Bluth Company to maximise revenue, they should develop a property that is/has: <br>
<ul><li>Spacious/large (i.e. large above ground living area, and large finished basement)
<li>Excellent quality
<li>In excellent condition
<li>Built recently (if remodelling)
<li>Non-commercial
</ul>
They should also avoid:
<ul>
<li> Mansard roofs
<li> Wall furnace heating
<li> 2-storey PUD, built in 1946 or after
<li> Meadow Village
</ul>
