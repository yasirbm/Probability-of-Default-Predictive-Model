# Credit Line Increase Model Card

### Important Note on Our Model(s)
Our group has built 2 models. 1 using Python, and another using R. Since the model built on Python performs better, this model card corresponds primarily to the Python Model. However, an R markdown file which summarizes the model and some of the key observations we made is available here: [R Markdown File](https://rpubs.com/yasirbm/803122)

### Basic Information

* **Persons involved in developing model**: Yasir Mohammad - `yasir@gwu.edu`, Katherine Scheuer - `kscheuer@gwu.edu`, Sadman Noor - `snoor11@gwu.edu`, Somender Chaudhary - `somender@gwu.edu` 
* **Model date**: August, 2021
* **Model version**: 1.0
* **License**: MIT License
* **Model implementation code**:
  * **Python Model**: [Credit_Line_Increase_Project_Python_Model.ipynb](https://github.com/yasirbm/DNSC6301---Analytics-Edge/blob/main/Python_Model/Credit_Line_Increase_Project_Python_Model.ipynb)
  * **R Model Markdown**: [R Markdown File](https://rpubs.com/yasirbm/803122)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Other students or professors assosciated with DNSC6301 - Analytics Edge and Data Ethics at the George Washington University School of Business.
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* Data dictionary:

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: GWU Blackboard, email one of the authors above for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, email one of the authors listed above for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model Details
* **Columns used as inputs in the final model**: 
  * Limit_BAL
  * PAY_0, PAY_2, PAY_3, PAY_4, PAY_5, PAY_6
  * BILL_AMT1, BILL_AMT2, BILL_AMT3, BILL_AMT4, BILL_AMT5, BILL_AMT6
  * PAY_AMT1, PAY_AMT2, PAY_AMT3, PAY_AMT4, PAY_AMT5, PAY_AMT6
* **Columns used as targets in the final model**: DELINQ_NEXT
* **Type of Model**: Supervised Learning - Decision Tree Model
* **Software used to train the Model**: Python via Google Colab
* **Version of the Software used to train the Model**: Python 3.6.9
* **Hyperparameters or other settings of the model**: ccp_alpha=0.0, class_weight=None, criterion='gini', max_depth=6, max_features=None, max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None, min_samples_leaf=1, min_samples_split=2, min_weight_fraction_leaf=0.0, presort='deprecated', random_state=12345, splitter='best'

### Quantitative Analysis
* **Metrics used to evaluate the model and final figures**:
  * **Training AUC**: 0.78
  * **Validation AUC**: 0.75
  * **Test AUC**: 0.74
  * **Asian-to-White AIR**: 1.00
  * **Black-to-White AIR**: 0.85
  * **Female-to-Male AIR**: 1.02
  * **Hispanic-to-White AIR**: 0.83

* **Correlation Heat Map (Python)**:

 ![corr heat map](https://user-images.githubusercontent.com/89418186/131205390-7b8b4da4-3972-403d-bea3-ac775cf11447.png)
 
* **Variable Importance Chart (Python)**:

 ![variable importance](https://user-images.githubusercontent.com/89418186/131205409-30556aa7-ce8c-474c-b67e-9e586ad561bb.png)
 
* **Iteration Plot of the final model (Python)**:
 
* ![download](https://user-images.githubusercontent.com/89418186/131016505-362577e1-9d0a-4196-9fda-056a8cd8c486.png)

* **Delinquency by Gender (R)**:

 ![image](https://user-images.githubusercontent.com/89418186/131267216-35b0cca4-6923-498d-a260-1d96814ff227.png)
 
* **Delinquency by Race (R)**:

 ![image](https://user-images.githubusercontent.com/89418186/131267224-69d9b364-5b30-48e9-b00e-c38a69aba149.png)
 
### Ethical Considerations
* **Potential negative impacts of the model**:
  * **Math/Software Problems**: As we can see in the variable importance plot above, the model is overdependant on the PAY_0 variable (which refers to the most recent repayment status). This could cause serious problems if we were to see a situation in which recent repayment behaviour drastically changes (i.e. - recession).
  * **Real world risks**: 
    * The Hispanic-to-White AIR is 0.83. Whilst this is above the minimum acceptable AIR (0.8) defined by the Equal Employment Opportunity Commission (EEOC), this figure is still relatively low.
    * This model doesn't consider factors (X_variables) such as employment and family history which would likely have a significant impact on the probability of deliquency in the real world.
* **Potential uncertainties relating to the impact of using the model**:
  * **Math/Software Problems**:
    * It is possible we could see differential validity as the model is deployed in the real world. To mitigate this risk, the model would need to be actively monitored even post deployment.
    * The data in this model was predominantly those of white consumers. Whilst this may be proportionate to the current demographic landscape of the USA, this is projected to decrease in the coming years. A better model might account for such projections when choosing the original dataset. 
  * **Real world risks**:
    * Possible risks of disparate impact due to relatively low Hispanic to White and Black to White AIR's (even though they are both above 0.8)
    * This sample is very specific to the USA. If this model was used outside the USA, there could be many undesired consequences as other countries would have compeltely different consumer behaviour, demographics etc.
* **Other unexpected results**: 
  * As the model is deployed in the real word, it is possible that we will see a drop in the AUC with all groups, but particularly with demographics that are slightly underrepresented in the training data (i.e. - Hispanic and Black).
  * The plots above (delinquency by gender and delinquency by race) show potentially problematic issues straight off the bat. This could have negative implications from an algorithmic bias perspective
  * It was surprising for the PAY_0 X Variable to be so strongly correlated to probablity of delinquency compared to other "PAY" X_Variables.
