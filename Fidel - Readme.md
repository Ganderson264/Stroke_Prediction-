# About the Data
## The original data contained 5,110 records in healthcare-dataset-stroke-data.csv obtained from the Kaggle Website

This data is organized by the following columns and values/value ranges:
- gender : Female, Male, Other
- age : .08 to 82 years
- hypertension : 0 (no), 1 (yes)
- heart_disease : 0 (no), 1 (yes)
- ever_married : no, yes
- work_type : Children, Never worked,​ Self-Employed,​ Govt_job,​ Private​
- Residence_type : Urban, Rural
- avg_glucose_level : 55.12 to 271.74
- bmi : NaN, 10.3​ to 97.6​
- smoking_status : never, Smoked​, unknown​, Formerly smoked​, smokes​
- stroke : 0 (no), 1 (yes)
  
**The dataset is EXTREMELY Inbalanced as less than 5% of the cases show a positive result for stroke**
# Cleaning the Data
**For the "First Model" the data was "cleaned" by:**
- Dropping : 
  - the only record with gender as "Other"
  - records with "NaN" as bmi value
    
- Encoding or replacing columns with 2 possible values :
  - replace "gender" with male values : 0 (no) or 1 (yes)
  - encoded ever_married with values : 0 (no) or 1 (yes)
  - replace Residence_Type with Urban : 0 (no) or 1 (yes)
  
- **Dataset A** set was created by OneHotEncoding or replacing columns with more than 2 possible values as follows:
  - from the work_type column others where created and assigned 0,1 values accordingly as follows:
    - work_type_Govt_job
    - work_type_Never_worked
    - work_type_Private
    - work_type_Self-employed
    - work_type_children
      
  - from the smoking_status column others where created and assigned 0,1 values accordingly as follows:
    - smoking_status_Unknown
    - smoking_status_formerly smoked
    - smoking_status_never smoked
    - smoking_status_smokes
      
- **Dataset B** was created by LabelEncoding values for columns with more than 2 possible values as follows:
  - the work_type column values where replaced based on a perceived stress level as follows:
    - children : 0
    - Never_worked : 1
    - Govt_job : 2
    - Private : 3
    - Self-employed : 4
      
  - the smoking_status column values where replaced based on a perceived health risk level as follows:
    - never smoked : 0
    - Unknown : 1
    - formerly smoked : 2
    - smokes : 3

# Processing the Data
1. Scaled versions of Datasets A and B where created by running them through StandardScaler and MinMaxScaller resulting in:
    - Dataset A StandardScaled
    - Dataset A MinMaxScaled
    - Dataset B StandardScaled
    - Dataset B MinMaxScaled
      
2. From this scaled versions **initially** 3 data sets where created with **ALL** the records with positive results and randomly selected records with negative results:
    1. One to One : Same number of records with positive and negative results.
    2. One to Two : for each record with positive result two records with negative results where added.
    3. One to Three : for each record with positive result three records with negative results where added.

3. Each one of this Datasets was used to train under the models:
    1. LogisticRegresion
    2. RandomForestClassifier
    3. SVC

5. After reviewing the results, RandomForestClassifier would return a high score in training and poor in testing.
    - A "best_depth" function was defined to calculate a best or close to best depth for this model's calculations
    - Code was added to the procedure to run this function for RandomForestClassifier and we repeated all the testing

6. After reviewing the results, some of the values in the **One to Three** dataset returned better results than the other more balanced samples.
    - A function was defined to create **1 balanced and 6 proportionally inbalanced** datasets and name them Ratio 1 to *X* where X was the number of negative same size as positive sets added
    - The procedure code was modified to run the function and create new datasets each time instead of using the initialy predifined Datasets 

7. Each of this Datasets (listed on step 1) where ran 20 times through the 3 models and the following report items where stored:
    - Test Model
    - Model Score
    - Proportion *( 1 to X )*
    - Compression ( Scaled or MinMax )
    - Balanced Accuracy
    - Precision
    - Recall
    - f1-score
    - Confusion metrix TP, FP, TN and FN results
    - Encoding Method

# Analysing the results
- 3360 result records were compiled from the model training runs
- after looking at the metrics collected we decided to focus on the f1-result metric
- Compared Max, Average and Min values:
  - Ratios 1:4, 1:5, 1:6 had high Max spikes with values of 39.85%, 40.22% and 39.66 respectivelly but the average values fell bellow other ratios
  - Ratios 1:2 and 1:3 consistently had the higher mean values of 26.07% and 25.32% respectivelly
  - Out of the records with the top 100 f1-scores for ratios 1:2 and 1:3:
    - A vast mayority (89) where from the RandomForestClassifier method
    - 56 of these where of the 1:3 ratio
    - 29 of these where compressed with MinMaxScaler

# Conclusion

Considering that this part of the project was carried out with 5110 records of medical data and to this data we applied :
  - 3 Encoding Methods
    - Dummies
    - OneHotEncoder
    - LabelEncoder
  - 2 Scaler methods
    - StandardScaler
    - MinMaxScaler
  - Data Sampling
  - 3 Machine Learning (ML) Models
    -  LinearRegression
    -  RandomForestClassifier
    -  SVC
    
We can tell that:
- The best proportion/ratio to train is : **1:3**
- The best ML method is : **RandomForestClassifier**
- There where no significant difference between the results for either compression method or encoding method

**This results are dependant on the available training data. We recommend retraining periodically as more data becomes available**
