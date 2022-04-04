# Decision Tree Model For Online Shopper Analysis 
## To Predict Which Online Vistors Will Decide to Buy
**Input features of the training dataset**
<br /> The training dataset contains of binary (nominal), discrete and continuous data. It mainly consists of data relating to the website’s users’ usage statistics on the website and whether the usage statistics eventually leads to a purchase being made.
<br />
<br /> **Binary (nominal) data:** Operating systems, Browser, Region, Traffic Type, Visitor Type, Revenue, Weekend
<br /> **Discrete data:** Administrative, Informational, Product Related 
<br /> **Continuous data:** Administrative Duration, Informational Duration, Product Related Duration, Page Values
<br /> **Summary Statistics for Quantitative Variables:**
|Variable|	Min	Max	Mean	Standard Deviation	Variance	Skewness	Kurtosis
Administrative
(Subject Matter)	0	27	2.318	3.328	11.073	1.971	4.7737
Administrative
Duration	0	3398.75	80.426	177.241	31414444	5.807	54.1954
Informational
(Subject Matter)	0	24	0.504	1.264	1.599	4.118	29.258
Informational
Duration	0	2549.375	34.484	142.614	20338.802	7.89	82.3957
Product Related (Subject Matter)	0	705	32.004	45.271	2049.506	4.438	32.2057
Product Related Duration	0	63973.522	1204.488	1961.271	3846583.282	7.774	151.5582
Page Values	0	361.764	5.753	18.354	336.863	6.613	71.594

All the quantitative variables here are positively skewed. Most of the quantitative variables have significant to large amounts of kurtosis. 
Product related duration has the most positively skewed distribution. This is not surprising as users of the website are likely there with the main intention to find out more about the products being sold. It also has the largest figure for kurtosis which suggests it has the largest extreme values, some of which might be outliers.
Administrative (subject matter) has the least positively skewed distribution. It also has the smallest figure for kurtosis which suggest it has the least extreme values.

Pie chart of Purchases (Revenue):
 
The dataset is unbalanced with respect to the target (Revenue). 85% of the users have not made a purchase which is essentially most of the population.
Reasons for choice of Decision Tree
1.	Capable of handling both continuous and binary (categorical) variables
2.	Able to provide a clear indication of which fields are most important for prediction 
Parameter Optimization Details and Findings
Method used: K-Fold Cross-Validation
•	Chosen because this method ensures that every observation from the original dataset has the chance of appearing in both the training and test set.
No. of folds: 10 
•	Too small a number of folds will result in more computation time, whereas the larger the number of folds, the lesser the accuracy. As such, I have chosen 10 because I find it to be a good balance of both efficiency in computation time and accuracy.
Choice of random seed: 1234
Objective Function to Optimize: Maximization of Accuracy 
Optimized Hyper parameter:  29 
•	This is the figure which gives the highest accuracy figure.
Decision Tree
a)	Recall is the preferred performance metric compared to Accuracy as we are more interested in the ability of the decision tree model to correctly predict the number of website users that have made a purchase as opposed to the ability of the decision tree model to make correct predictions (which contains both buying and non-buying website users). 

b)	The accuracy of a dummy model where predicted REVENUE is assigned as FALSE for all records in the test set is 0.855

c)	Accuracy of original decision tree model: 0.9
The accuracy of the original decision tree model is 0.9 which is higher than when we assigned predicted REVENUE as FALSE for all records in the test set where the accuracy is 0.855.

d)	It is still worth as the recall value is 0.64 (where REVENUE = TRUE is taken to be positive) which has reasonable predictive value in whether users have made purchases. More importantly, the model still has higher accuracy in correctly predicting both buying and non-buying website users in comparison to the model just predicting correctly non buying website users. This means the model is better suited to predicting purchase intent rather than just predicting non purchase intent.

Characterization of website users who have a positive purchase intent (REVENUE=TRUE)
 
Users who are looking at pages with values greater than 9.025 are mostly users that have a positive purchase intent. Out of this group of users who are looking at page with values greater than 9.025, most are returning visitors that have a positive purchase intent.  The second most for Page Values > 9.025 with positive purchase intent, are new visitors and the least are other types of visitors. 
Thus, when the users are looking at Page Values > 9.025, it will predict that the users have a positive purchase intent, and that this group of users will be predicted to be returning customers. 

Cost Matrix Scenario
1.	Predicting correctly that a customer will purchase: $8000
•	The website might be correctly able to recommend what the customer seeks or might want to purchase, thus increasing sales.
2.	Predicting incorrectly that a customer will not purchase: $5000
•	The website is not able to correctly predict what the customer seeks to buy and thus is not able to recommend what the customer may additionally seek to buy, thus not being able to generate additional sales.
3.	Predicting correctly that a customer will not purchase: $0
•	There is no cost involved here.
4.	Predicting incorrectly that a customer will purchase: $-50
•	The website might try to entice users that it thinks will purchase by offering free vouchers worth $50 to make purchases, however when such users do not purchase, the free vouchers given are essentially a cost.

Original	Predicted
 	 	TRUE	FALSE
Actual	TRUE	251	141
	FALSE	106	1968

Cost Matrix	Predicted
 	 	TRUE	FALSE
Actual	TRUE	$8000	$5000
	FALSE	$-50	0

REVENUE = FALSE	Predicted
 	 	TRUE	FALSE
Actual	TRUE	0	0
	FALSE	357	2109

Original Model	REVENUE = FALSE
251*$8000 = $2,008,000
141*$5000 = $705,000
106*$-50 = $-5300
1968*$0 = 0
Total = $2,707,700	0*$8000 = 0
0*$5000 = 0 
357*-$50 = -17,850
2109*0 = 0
Total = -17,850

Evaluation
1.	The original model is superior because its predictions result in a profit as opposed to the “REVENUE = FALSE” model where there is a loss.
2.	“REVENUE = FALSE” model is able to classify more users with negative purchase intent overall, but such users do not bring any form of revenue. But in terms of specificity, and not looking at absolute value alone, the original model actually has a higher specificity rate of 0.949 compared to the “REVENUE = FALSE” model’s 0.855.
