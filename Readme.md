# Stroke Prediction Model

## Project Overview

This project develops a machine learning model to predict the likelihood of a stroke. Utilizing the Random Forest classification algorithm, the model processes health-related features to estimate stroke risk. Special attention was given to addressing class imbalance with Synthetic Minority Over-sampling Technique (SMOTE), refining features through selection techniques, and hyperparameter tuning using grid search for optimal model performance.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Development](#development)
- [Data](#data)
- [Model](#model)
- [Contributing](#contributing)
- [License](#license)

## Installation

To set up your local environment to run the model, follow these steps:

```bash
git clone https://github.com/your-username/stroke-prediction-model.git
cd stroke-prediction-model
pip install -r requirements.txt

## Usage
Run the model prediction with the following command:
python predict.py

Development
After cloning the project, create a virtual environment and activate it:

python -m venv venv
source venv/bin/activate # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt

## Data

The dataset comprises various health metrics and demographics to predict stroke occurrences:

- `Age`: Age of the patient.
- `Hypertension`: Indicates if a patient has hypertension.
- `Heart Disease`: Indicates if a patient has any heart diseases.
- `Average Glucose Level`: The average glucose level in blood.
- `BMI`: Body Mass Index of the patient.
- `Smoking Status`: Patient's smoking habits.

The target variable is 'Stroke' with binary outcomes: '1' for Stroke and '0' for No Stroke.

## Model

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

## Contributing

We welcome contributions! Please follow these steps to contribute:

1. Fork the repository.
2. Create a new branch for your feature (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a pull request.




     
