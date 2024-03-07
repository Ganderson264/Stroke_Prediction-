# Stroke Prediction Model

## Project Overview

This project develops a machine learning model to predict the likelihood of stroke events. Utilizing a dataset of patient records, the model is trained to recognize patterns and features associated with stroke incidents. Our primary goal is to achieve high recall to ensure maximum identification of true positive stroke cases.

## Data
### The original data contained 5,110 records in healthcare-dataset-stroke-data.csv obtained from the Kaggle Website
The dataset comprises various health metrics and demographics to predict stroke occurrences:

- `Age`: Age of the patient.
- `Hypertension`: Indicates if a patient has hypertension.
- `Heart Disease`: Indicates if a patient has any heart diseases.
- `Average Glucose Level`: The average glucose level in blood.
- `BMI`: Body Mass Index of the patient.
- `Smoking Status`: Patient's smoking habits.
- **The target variable is 'Stroke' with binary outcomes: '1' for Stroke and '0' for No Stroke.**

### Additional Data Information

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

## Preprocessing

Data preprocessing steps can include:
- Handling missing values.
- Encoding categorical variables.
- Scaling numerical features.
- Advanced feature engineering to enhance model performance.

# Three approaches where taken to look for the best model

## Approach #1 suggested by Gabriel Anderson


## Approach #2 suggested by Fidel Lerma

### Cleaning the Data
For this model the data was "cleaned" by:
- Dropping : 
  - the only record with gender as "Other"
  - records with "NaN" as bmi value
    
- Encoding or replacing columns with 2 possible values :
  - replace "gender" with male values : 0 (no) or 1 (yes)
  - encoded ever_married with values : 0 (no) or 1 (yes)
  - replace Residence_Type with Urban : 0 (no) or 1 (yes)

- **Dataset A** was created by OneHotEncoding or replacing columns with more than 2 possible values as follows:
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

### Processing the Data

1. Scaled versions of Datasets A and B where created by running them through StandardScaler and MinMaxScaller resulting in:
    - Dataset A StandardScaled
    - Dataset A MinMaxScaled
    - Dataset B StandardScaled
    - Dataset B MinMaxScaled
      
**Taking in consideration that the dataset is EXTREMELY Imbalanced as less than 5% of the cases show a positive result for stroke**

2. From this scaled versions **initially** 3 data sets where created with **ALL** the records with positive results and randomly selected records with negative results:
     - One to One : Same number of records with positive and negative results.
     - One to Two : for each record with positive result two records with negative results were added
     - One to Three : for each record with positive result three records with negative results were added.

3. Each one of this Datasets was used to train under the models:
    1. LogisticRegresion
    2. RandomForestClassifier
    3. SVC

5. After reviewing the results, RandomForestClassifier would return a high score in training and poor in testing.
    - A "best_depth" function was defined to calculate a best or close to best depth for this model's calculations
    - Code was added to the procedure to run this function for RandomForestClassifier and we repeated all the testing

6. After reviewing the results, some of the values in the **One to Three** dataset returned better results than the other more balanced samples.
    - A function was defined to create **1 balanced and 6 proportionally imbalanced** datasets and name them Ratio 1 to *X* where X was the number of negative same size as positive sets added
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
    - Confusion matrix TP, FP, TN and FN results
    - Encoding Method

### Analysing the results
- 3360 result records were compiled from the model training runs
- after looking at the metrics collected we decided to focus on the f1-score metric
- Compared Max, Average and Min values:
  - Ratios 1:4, 1:5, 1:6 had high Max spikes with values of 39.85%, 40.22% and 39.66 respectively but the average values fell bellow other ratios
  - Ratios 1:2 and 1:3 consistently had the higher mean values of 26.07% and 25.32% respectively
  - Out of the records with the top 100 f1-scores for ratios 1:2 and 1:3:
    - A vast majority (89) where from the RandomForestClassifier method
    - 56 of these where of the 1:3 ratio
    - 29 of these where compressed with MinMaxScaler

### Approach 2 Conclusion

Considering that this part of the project started with with 5110 records that where cleaned down to 4908 records of medical data and to this data we applied :
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
- There were no significant difference between the results for either compression method or encoding method

**This results are dependant on the available training data. We recommend retraining periodically as more data becomes available**


## Approach #3 suggested by Juan Carlos Lavieri
### Feature Engineering

We generate polynomial features and interaction terms to unearth non-linear relationships and intricate interactions among features, aiming to bolster the predictive power of our model.

### Model Training

For the classification task, we employ a Random Forest classifier known for its robustness and efficacy in handling imbalanced datasets. The model training is performed on a balanced dataset achieved via oversampling techniques, specifically SMOTE.

### Hyperparameter Tuning

Hyperparameter optimization is conducted using GridSearchCV. This involves a comprehensive search across a range of parameter combinations, leveraging cross-validation to ascertain the most effective model configuration.

### Model

Our Random Forest model includes key hyperparameters such as:

- `n_estimators`: 200
- `max_depth`: 20
- `min_samples_split`: 5
- `min_samples_leaf`: 3

Performance metrics on the test set:

- **Accuracy**: 94.19%
- **Precision (Stroke class)**: 50%
- **Recall (Stroke class)**: 2%
- **F1-Score (Stroke class)**: 4%

### Evaluation

The model's performance is meticulously evaluated using a confusion matrix. Emphasis is placed on recall to minimize false negatives. We also measure precision, F1 score, and accuracy to gain a holistic view of the model's predictive capacity.

### Best Model Results

The optimal model configuration achieved a recall score of approximately 63.48%, marking a substantial improvement in the identification of actual stroke cases.

## Contributing

We welcome contributions! Please follow these steps to contribute:

1. Fork the repository.
2. Create a new branch for your feature (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a pull request.
