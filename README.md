![King County](/images/King_County_Landscape.jpeg)
# Title

**Authors**: Dermot O'Brien, Eddie Juarez, Eliot Kmiec

## Overview

Flatiron Insurance Agency offers a wide variety of property insurance solutions giving a hommeowner the best coverage needed at great prices. Flatiron Insurance Agency is currently dominating the East coast insurance market and wants to make a statement when entering the West Coast market.

## Business Problem

In order to help Flatiron Insurance provide the best coverage to their customers, they need to know what features of their customer's homes impact the home's value. Knowing these features allows our client to accurately estimate how much it will cost to insure the home, and overall helps them protect their bottom line. DEE Analytics will construct a multiple linear regression model as part of an inferential analysis on features of houses in King County. Our team will then use this model to find features that have the strongest impact on house sale price to determine which aspects of a house most strongly affect its value.

## Data

Data has been collected by the King County Assessor's office, which we are using to construct our model. The data is a set of tabular data containing characteristics of homes that were assessed as part of a property sale between May 2014 and May 2015. The dataset contains over 21,000 entries and roughly 20 features that we will be evaluating. (See project workflow pdf)

## Methods

The general approach to this project follows the CRISP-DM process with the end goal being to produce a multiple linear regression model that will be used to identify the strongest predictors of home value for houses in our dataset. 

The first step is to explore the data and determine whether the features present in our dataset are categorical in nature or continuous. This will determine how those features are prepared for use in our model, and potentially whether that feature is recorded reliably enough to be used for modelling. 

The second step is to clean the data feature by feature, ensuring that each one is formatted correctly to be passed into the linear regression model. Log transformations and encoding of categorical features are the primary methods used to accomplished this. 

The third step is to scale the data for comparison and construct the model we seek to iterate on. We chose to use the Robust Scaler from the sklearn package to scale our features by interquartile range and centered on the median rather than the mean. Scaling in this manner offers a benefit over standard scaling methods when handling outliers, as the center of the distribution is no longer affected as severely by outliers and skew. 

Using ordinary least squares to construct our model and the Robust Scaler, we constructed a single linear regression using the strongest independently positive correlated feature, and began to iterate on that model by adding features one by one and evaluating their impact on the model. Features that improved the model were retained, and features that did not improve the model were dropped before the next iteration. 

The 8 features that remained in the model following 14 iterations on our OLS multiple linear regression model were then subject to another evaluation of normality, correlation strength, and skew/presence of outliers. One last feature was dropped due to non-normality, and some data points were removed due to being extreme outliers. The final model was then reevaluated and final results were generated.

## Results

Our final model was a multiple linear regression model using ordinary least squares, which, included seven features that had a significant p-value and did not cause our model to violate assumptions of linear regression. Each of these features was included for consideration based on the strength of its correlation with home sale price, and then was retained or dropped from the final model based on its effects on the model's performance.

The results we obtained for our model generally indicate that it will be an effective tool for our client, and the transformations we performed ensure that the model retains accuracy for homes in all value ranges. In turn, this means that the features we have indicated to our client as being the best ones to model on will perform equally well for the wide variety of homes they insure.

Linear regression models rely on 4 key assumptions: Linearity, Independence, Normality of Errors, and Homoskedasticity.

Early on, several of our underlying features displayed a non-linear relationship to our target due to skew in their distributions. We addressed this issue via log transformation of our target, home sale price, as well as some of our features.

Independence was assessed via the Condition Number, which, for our final model, was 8.17. While this does indicate a small degree of multicollinearity, this is within the expected limits for this metric and a model of this type. Independence is also assessed via the Durbin-Watson score, which, is ideally a value of 2 on a scale from 0 to 4. Our Durbin-Watson score is 1.97, thus confirming that our features are independent.

Normality of Errors was assessed via two different metrics: Jarque-Bera probability, and Quantile-Quantile plotting. Due to the non-continuous nature of some features, as well as the degree of skew in the features available to us, we were unable to satisfy the Jarque-Bera probability test, however, this test is known to be extremely sensitive. Quantile-Quantile plotting showed our features to be relatively normal, and our scaler was chosen specifically due to its use of the median for its center to increase the normality of the features in our final model. Although we did not successfully pass the Jarque-Bera test, significant improvement was made over the course of our model development, and features that violated both tests were removed before constructing the final model.

Homoskedasticity was measured using the Goldfeldt-Quandt test. This test measures heteroskedasticity against a null hypothesis of homoskedasticity. Our p-value was ~0.99, so we fail to reject the null and find our model is homoskedastic.

Our R^2 value is 0.577, indicating that our model explains approximately 57.7% of the variance in house sale price. This is a significant model with an overall p-value less than 0.001, and an effective method for identifying key features for predicting home sale price.

One feature we suspect would improve the accuracy of our model was home location, however, based on domain knowledge about the relationship between location and several other features in our model, we also suspected that this feature would share a high degree of multicollinearity with the rest of our model. Obtaining additional data to explore interactions between location and other features is potentially an area for further research that could yield further improvements to the model we have developed here, while simultaneously addressing the problem of multicollinearity.

## Conclusions

We have developed a robust multiple linear regression model that provides our client with several powerful predictors of home value in a potential new market that they are looking to enter. Using this information, we believe that Flatiron Insurance will have gained key insights that will improve their ability to provide insurance to homeowners in King County, thus giving them a competitive edge. With further development to our model, we believe it has the potential to provide our client with powerful predictive estimates of their customer's property values that will have a significant impact on the prices Flatiron Insurance can offer and the coverage they can provide.

## For More Information

Please review our full analysis in [our Jupyter Notebook](./Final_Deliverable_Notebook.ipynb) or our [presentation](./King_County_Presentation.pdf).

For any additional questions, please contact **Dermot O'Brien & dermot.obri@gmail.com, Eddie Juarez & mr.eduardjuarez@gmail.com, Elito Kmiec & eliotkmiec@gmail.com**

## Repository Structure

Describe the structure of your repository and its contents, for example:

```
├── README.md                           <- The top-level summary README for reviewers of this project
├── Final_Deliverable_Notebook.ipynb    <- Narrative documentation of analysis in Jupyter notebook
├── King_County_Presentation.pdf        <- PDF version of project presentation
├── data                                <- Both sourced externally and generated from code
└── images                              <- Both sourced externally and generated from code
├── Results                             <- Visuals stored as pdfs
└── working_notebooks                   <- Scratch notebooks of code for our analysis
```
