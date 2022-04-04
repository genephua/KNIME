# Decision Tree Model For Online Shopper Analysis 
## To Predict Which Online Vistors Will Decide to Buy
### Input features of the training dataset
The training dataset contains of binary (nominal), discrete and continuous data. It mainly consists of data relating to the website’s users’ usage statistics on the website and whether the usage statistics eventually leads to a purchase being made.
<br />
<br /> **Binary (nominal) data:** Operating systems, Browser, Region, Traffic Type, Visitor Type, Revenue, Weekend
<br /> **Discrete data:** Administrative, Informational, Product Related 
<br /> **Continuous data:** Administrative Duration, Informational Duration, Product Related Duration, Page Values
### Summary Statistics for Quantitative Variables:

![image](https://user-images.githubusercontent.com/102946848/161532861-926a0545-e063-4a11-b7fb-f4fed546fcf9.png)

All the quantitative variables here are positively skewed. Most of the quantitative variables have significant to large amounts of kurtosis. 
Product related duration has the most positively skewed distribution. This is not surprising as users of the website are likely there with the main intention to find out more about the products being sold. It also has the largest figure for kurtosis which suggests it has the largest extreme values, some of which might be outliers.

Administrative (subject matter) has the least positively skewed distribution. It also has the smallest figure for kurtosis which suggest it has the least extreme values.

### Pie chart of Vistors (Buyers & Non Buyers) (Revenue):

![meta-chart](https://user-images.githubusercontent.com/102946848/161533911-14a14b8a-95bc-4de4-b636-6110981e151c.jpeg)

 
The dataset is unbalanced with respect to the target (Revenue). 85% of the users have not made a purchase which is essentially most of the population.
### Reasons for choice of Decision Tree
1. Capable of handling both continuous and binary (categorical) variables
2. Able to provide a clear indication of which fields are most important for prediction 
### Parameter Optimization Details and Findings
**Method used:** K-Fold Cross-Validation
<br /> •Chosen because this method ensures that every observation from the original dataset has the chance of appearing in both the training and test set.

 **No. of folds:**  10 
<br /> •Too small a number of folds will result in more computation time, whereas the larger the number of folds, the lesser the accuracy. As such, I have chosen 10 because I find it to be a good balance of both efficiency in computation time and accuracy.

**Choice of random seed:** 1234

**Objective Function to Optimize:** Maximization of Accuracy 

**Optimized Hyper parameter:**  29 
<br />  •This is the figure which gives the highest accuracy figure.

### Decision Tree
a) Recall is the preferred performance metric compared to Accuracy as we are more interested in the ability of the decision tree model to correctly predict the number of website users that have made a purchase as opposed to the ability of the decision tree model to make correct predictions (which contains both buying and non-buying website users). 

b)The accuracy of a dummy model where predicted REVENUE is assigned as FALSE for all records in the test set is 0.855

c) Accuracy of original decision tree model: 0.9
The accuracy of the original decision tree model is 0.9 which is higher than when we assigned predicted REVENUE as FALSE for all records in the test set where the accuracy is 0.855.

d) It is still worth as the recall value is 0.64 (where REVENUE = TRUE is taken to be positive) which has reasonable predictive value in whether users have made purchases. More importantly, the model still has higher accuracy in correctly predicting both buying and non-buying website users in comparison to the model just predicting correctly non buying website users. This means the model is better suited to predicting purchase intent rather than just predicting non purchase intent.

### Characterization of website users who have a positive purchase intent (REVENUE=TRUE)

![image](https://user-images.githubusercontent.com/102946848/161537611-c087f1ce-5bcc-4585-ac53-9c89e4931190.png)

Users who are looking at pages with values greater than 9.025 are mostly users that have a positive purchase intent. Out of this group of users who are looking at page with values greater than 9.025, most are returning visitors that have a positive purchase intent.  The second most for Page Values > 9.025 with positive purchase intent, are new visitors and the least are other types of visitors. 

Thus, when the users are looking at Page Values > 9.025, it will predict that the users have a positive purchase intent, and that this group of users will be predicted to be returning customers. 

*Analysis powered by KNIME Analytics Platform*
<br /> *Source: Data.xlsx*
