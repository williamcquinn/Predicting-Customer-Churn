# Predicting-Customer-Churn
S-Mobile: Building a model to predict customer churn for a leading cellphone carrier in Singapore. Using model output to understand the main drivers of churn  and using insights on churn drivers to develop actions/offers/incentives. Quantifying the impact of these actions/offers/incentives on the probability of churn and deciding which actions/offers/incentives to target to which customers. Evaluating the economics of these actions/offers/incentives. 

Shu Ying Seng was a member of the first graduating class of the new Master’s in Business Analytics 
program of the National University of Singapore (NUS). In contrast to many of her classmates who had 
little prior work experience, Shu Ying had worked for S-Mobile, a leading cellphone carrier in Singapore, 
for 7 years. Because she loved working there and because S-Mobile helped pay for her degree, she 
returned to the company 6 months ago. 
 
Shu Ying’s last job at S-Mobile before she attended NUS was to manage the retention desk at the 
company’s call center. Her team’s task was to persuade customers who called to leave S-Mobile to stay 
with the carrier instead. While Shu Ying’s team could prove high “save” rates, she had always felt uneasy 
about this form of “reactive” churn management – she felt that it trained customers to threaten to leave 
in order to get discounts.  
 
One of the key moments during her master’s program was when Shu Ying discovered that customer 
analytics provided a compelling alternative to reactive churn management: Instead of waiting until a 
customer tried to leave, the company could be proactive and predict each customer’s churn risk – before 
they even threatened to leave. This seemed like a much better approach because it allowed a company 
to act before customers were dissatisfied enough to want to leave, and retention offers had a much better 
chance of delighting customers. After all, how good could a retention offer look if it was given in response 
to a customer’s threat to quit? 
 
Given Shu Ying’s experience in customer relations and the skills she acquired at NUS, she now managed 
an analytics team tasked with decreasing customer churn. She realized this was a big task. In the future, 
she might have to change the data that was collected, how customers were treated, what plans were 
available, etc. 

The first step, however, was to determine if existing data could be used to identify if some customers 
were more likely to churn than others. And if so, what marketing actions and offers could be used to 
reduce churn. 
 
Shu Ying asked her team to pull data on a random sample of customers in order to build a predictive churn 
model. The response variable was whether a customer had churned in the last 30 days. The explanatory 
variables described customer characteristics and behavior over the 4 months preceding that period (i.e., 
the total time period covered in the data was 4 months + 30 days). See the data description at the end of 
this document. 
 
The sample consists of three parts: 
 
1.  A training sample with 27,300 observations and a 50% churn rate (“training == 1”) 
2.  A test sample with 11,700 observations and a 50% churn rate (“training == 0”) 
3.  A representative sample with 30,000 observations and a churn rate of 2%, i.e., the actual 
monthly churn rate for S-mobile (“representative == 1”) 
 
The model would be used to generate churn predictions for 30,000 randomly chosen customers, i.e., the 
“representative sample” in the dataset, for whom Shu Ying had been authorized to evaluate the 
proactive churn management program.  
 
To scale the predicted churn probabilities for use in the representative sample, the team could use 
(case) weights. However, not all models have an option to specify case weights or may even perform 
poorly when weights are applied during estimation. For this reason, a dataset with 1M observations is 
also available through the dropbox link below for training and test and an extra 30,000 for final 
predictions. 
  
The downside to using the dataset with 1M rows is, of course, that estimation time will increase 
substantially. You can use this larger dataset to re-estimate your chosen model and generate predictions 
for the representative sample. 
 
The task 
 
As Shu Ying briefed her team, she laid out what they would have to accomplish: 
 
1.  Develop a model to predict customer churn 
2.  Use model output to understand the main drivers of churn 
3.  Use insights on churn drivers to develop actions/offers/incentives 
4.  Quantify the impact of these actions/offers/incentives on the probability of churn 
5.  Decide which actions/offers/incentives to target to which customers 
6.  Evaluate the economics 
 
Assignment guidelines 
 
1.  Develop a model to predict customer churn
 
•  Feel free to use any technique you like to predict churn. However, make sure that one of 
your models is a logistic regression so that you can use odds ratios for the interpretation 
required in step 2 

•  Build models using the training and test data and explain your modeling choices

•  If you are going to use a Neural Network, Random Forest, or Boosted decision tree you must 
also provide information on: 

a. Variable importance – sklearn.inspection.permutation_importance in python 
b. Partial Dependence Plots – sklearn.inspection.plot_partial_dependence in python 
 
2.  Use the model output from a logistic regression to understand the main drivers of churn and 
report on the key factors that predict customer churn and their relative importance  
 
3.  Use insights on churn drivers to develop actions/offers/incentives 

•  Consider each variable type, e.g. “Equipment characteristic”, “Customer usage”, etc. (see 
the data table at the end of this case) 
   
4.  Quantify the impact of these actions/offers/incentives on the probability of churn 

•  Either (i) predict the effect of a churn driver (similar to what we did for Pentathlon III) or (ii) 
suggest how you might test the action/incentive/offer in the field

•  Generate predictions for the representative sample 

•  Since you can’t actually execute a test, describe how you would set up such a test and then 
make an assumption about the impact on churn that you can use in steps 5 and 6 
 
5.  Decide which actions/offers/incentives to target to which customers
 
•  For each action/offer/incentive specify the criteria used to select customers. Will you apply 
the action/offer/incentive to all customers, or a subset? Motivate your approach 
 
6.  Evaluate the economics: For each action/offer/incentive evaluate the profitability implications 
using a 5-year (60 month) time window 
