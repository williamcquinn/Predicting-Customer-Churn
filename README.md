# Predicting-Customer-Churn
Building a model to predict customer churn and using the model output to understand the main drivers of churn and generate insights on main drivers to determine actions. Secondly, quantifying the impact of these actions on the probability of churn and deciding which offers and incentives to send to which customers.

**Logistic Regression**

Before building a logistic model, we did exploratory data analysis to understand the distributions of every variable. Although we notice some of the explanatory variables to be skewed, we do not need to transform them for the sake of this logistic model. With the insights from our EDA, we built the baseline logistic model with `churn_yes` as the response variable and all the other variables as explanatory variables with `cweights` of 1:49. Looking at the odds plot for the model showed many variables with OR approximately equal to 1. 

To accurately visualize the odds and look at the importance of the explanatory variables, we used standardized numeric variables as the model input to check the odds plot and importances. Based on this model, we were able to get the importances of all the explanatory variables.

**Gradient Boosted Tree Model**

As an alternative to the logistic regression model, we built both a boosted tree model, which allows for greater hyper parameter tuning, and a tuned logistic regression model, in which we looked at non-linear relationships between the variables with the highest permutation importances from the XGBoost model and churn rate. When we built the boosted tree model, the  top 5 permutation importances varied in order from the importances calculated with the initial (standardized) regression model above. 

This is likely due to the linearity between variables, which the baseline regression model above did not account for. The variable of importance is `overage` in this case. To corroborate this, we tuned the model from above by adding a squared and cubed value of `overage` into the model. And when we did this, we observed that the importance of the cubed term was the highest, followed by the squared `overage` term. This helps confirm that the reason for `overage` having the highest permutation importance above was linearity between the variables. 

**Continuing with Baseline Regression**

With this insight, combined with the fact that interpretability of the results is the most important factor, we are now able to confidently move ahead with the baseline logistic regression model we built above. 

We found the variables with the highest importances to be `occupation`, `highcreditr`, `overage`, and`eqpdays`. 

The two *Partial Dependence Plots* display the partial dependence of the variables `overage` and `eqpdays` on the `churn_yes` rate . 

In the `overage` plot, the variability in dependence suggests a non-linear relationship between the `overage` and churn rate, which we further confirmed with the tuned logistic regression model. This non-linearity can be observed until about 50 minutes of overage and again after the customer reaches around 175 minutes of overage. We reason that at a certain point for many customers, the overage charges become unbearable. 

As for the plot with `eqpdays` on the x-axis, we observe a step-wise relationship between the `eqpdays` variable and churn rate. We reason that this could be that upon the increase of a new device, instead of purchasing a device they choose to switch providers to gain advantage of sign up deals, which is a standard practice in the mobile carrier industry. 

**Discussing Top 5 Motivators for Churn**

Using the output of our final model, we tabulated the importances of the explanatory variables. For simplicity, we are discussing only the top five important variables as per the table as the main drivers of the churn. 

The variables are listed in decreasing order of importance as follows  :
occupation[T.retired](5.422): With odds of 0.184, relative to the user whose occupation is other, the odds of the retired user churning is 81.6% less keeping other variables constant.
highcreditr[T.yes](2.069): With odds of 0.483, a user with high credit rating has 51.7% less odds of churning, keeping other variables constant.
occupation[T.student](1.900):With odds of 1.90, relative to the user whose occupation is other, the odds of a student user churning is 90% higher keeping other variables constant.
eqpdays(1.828): Since the odds-ratio (1.828)  is greater than 1, this means that the odds of a customer churning increases as the value of `eqpdays` increases keeping other variables constant.
overage(1.786):Since the odds-ratio (1.786)  is greater than 1, this means that the odds of a customer churning increases as the value of `overage` increases keeping other variables constant.

Of these 5 variables the two `occupation` variables and `highcreditr` are customer characteristic variables, `eqpdays` is a equipment characteristic variable, and `overage` is a customer usage variable. Churn, as a result from the level of `occupation` and `highcreditr`, is something that we decided was out of scope for customer retention and shall only be useful in the acquisition stages. `Overage` and `epqdays` were the two variables of the highest importance that we see as the controllable factors to reduce churn.

**Proposed Inentives**

From the churn drivers above, we chose to  develop offers/incentives for the controllable variables `overage` and `eqpdays`.

Overage (Customer usage):

`Overage` is a customer usage characteristic, and the action targeting this variable can alter customer behavior with respect to the churn. Looking at fees for higher overages in the bill prompts customers to wonder if they are with the right plan or right company as per their usage.

From the company’s perspective, `overage` generates a lot of profit, and as such, it is one of the most important factors of churn as well. The revenue from `overage` minutes is always impulsive and a strategy should be devised to reduce the `overage` and include it as part of the `mou`. We have decided that retaining the customer will be more profitable for the company in the long-term. To do so, the plan we are offering customers will help subsidize `overage` costs. 

1. For customers whose `overage` is less than 100 minutes, we have decided to completely subsidize `overage` costs. While this means we are taking a hit on our short term profit, we expect to eventually gain profit in the long run. We anticipate this also altering customer behavior by motivating customers to stay under 100 minutes of `overage` minutes in future cycles.
2. For the customers who still have `overage` more than 100 mins, we run a promotional campaign where 100 mins of their total overage will be subsidized at 50%. As an initiative to reduce overage gradually, we decided to provide warnings at 80mins, 90mins and 100 mins with an idea that the frequent warnings will prompt a heavy user to try and upgrade to the higher plan.
3. For customers who have monthly usage, the ratio of their `overage` respective to their `mou` will be considered. By targeting customers who surpass the threshold of 10%, we are subsidizing their costs. We are taking this threshold to likely mean that the `overage` was a genuine mistake or due to emergencies, and are thus willing to overlook it.  

Eqpdays (Equipment characteristic):

Since this variable is an equipment characteristic variable that describes the number of days the user has been using the current device, the action cannot directly alter a behavior. Instead, we will focus on offering an incentive in which the customer has the choice of changing this characteristic, and thus becoming a part of a new subset of customers, one which will likely result in a lower churn rate.

Logically, if a customer owns an older device, they are more likely to churn because they have the chance of being encouraged to switch providers for a new device or exposed to offers to upgrade their device from another carrier. This is the leverage that we will use, and we will expose a subset of customers, who have devices older than a certain threshold, to an upgrade offer.

If the user interacts with the offer and upgrades their device withthe company, they become part of the customer base that have a lower churn rate because they tend to stay longer either by expanding their contract or being less tempted by other competitors' offers. 

Overage: Subsidize Overage costs

• Action/Plan: Subsidize the customer’s overage minutes if the ratio  of `overage` minutes to `mou` is under 10%. 

Equipment Days: 

• Identify customers whose devices are older than 365 days and send a device upgrade offer. As we cannot run the experiment, we assume that, of the customers mailed, 10%  will respond by upgrading the device. 
