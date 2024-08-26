# Adversarial Debiasing of Criminal Defendant's Likelihood of Reoffending

## Overview

This repository contains the implementation of **Adversarial Debiasing** to reduce bias in predicting the likelihood of reoffending (recidivism) using the COMPAS dataset.

COMPAS (Correctional Offender Management Profiling for Alternative Sanctions) is a widely used algorithm that assesses the likelihood of criminal defendants reoffending. However, it has been shown to exhibit bias, particularly with respect to race. This project aims to mitigate that bias using adversarial debiasing techniques.

## Table of Contents

1. [Installation](#installation)
2. [Dataset](#dataset)
3. [Model Description](#model-description)
4. [Usage](#usage)
5. [Results](#results)
6. [Contributing](#contributing)
7. [License](#license)

## Installation

Clone the repository and install the required packages.

```bash
git clone https://github.com/Arwa-Fawzy/Adversarial-Debiasing-of-Criminal-Defendant-s-Likelihood-of-Reoffending.git
cd Adversarial-Debiasing-of-Criminal-Defendant-s-Likelihood-of-Reoffending
pip install -r requirements.txt
```

## Dataset

The dataset used in this project is the COMPAS dataset, which contains demographic and criminal history data on defendants. For more details on the dataset, please refer to the [COMPAS dataset documentation](https://github.com/propublica/compas-analysis).

- **Features**: Demographics, criminal history, and recidivism prediction scores.
- **Target**: Whether the defendant reoffends within two years.

You can download the dataset [here](https://github.com/propublica/compas-analysis/blob/master/compas-scores-two-years.csv).


1. **Person Information**:
   - **Person_ID**: A unique identifier assigned to each individual.
   - **AssessmentID**: A unique identifier for the specific assessment conducted on the individual.
   - **Case_ID**: The identifier for the legal case associated with the individual.

2. **Demographics**:
   - **Agency_Text**: The name of the agency conducting the assessment (e.g., PRETRIAL).
   - **LastName**: The individual's last name.
   - **FirstName**: The individual's first name.
   - **MiddleName**: The individual's middle name (or NULL if not available).
   - **Sex_Code_Text**: The individual's gender (e.g., Male).
   - **Ethnic_Code_Text**: The individual's ethnicity or race (e.g., Caucasian, African-American).
   - **DateOfBirth**: The individual's date of birth.

3. **Assessment Details**:
   - **ScaleSet_ID**: A numeric identifier for the set of scales used in the assessment.
   - **ScaleSet**: Describes the set of scales (e.g., "Risk and Prescreen") used to evaluate the individual.
   - **AssessmentReason**: The reason for the assessment (e.g., Intake).
   - **Language**: The language in which the assessment was conducted (e.g., English).
   - **LegalStatus**: The individual's legal status at the time of assessment (e.g., Pretrial).
   - **CustodyStatus**: The custody status of the individual (e.g., Jail Inmate).
   - **MaritalStatus**: The individual’s marital status (e.g., Single, Married).

4. **Dates and Times**:
   - **Screening_Date**: The date the screening took place.

5. **Risk and Supervision Levels**:
   - **RecSupervisionLevel**: A numeric identifier for the recommended supervision level (e.g., 1 for Low, 4 for High).
   - **RecSupervisionLevelText**: A textual description of the supervision level (e.g., Low, High).

6. **Assessment Scores**:
   - **Scale_ID**: The identifier for the specific scale used in the assessment (e.g., 7 for Risk of Violence).
   - **DisplayText**: The description of the scale being used (e.g., Risk of Violence, Risk of Recidivism).
   - **RawScore**: The raw score produced by the assessment for that specific scale.
   - **DecileScore**: A decile score indicating the severity of risk, ranging from 1 to 10 (higher numbers indicate higher risk).
   - **ScoreText**: A textual description of the risk level (e.g., Low, High).

7. **Assessment Metadata**:
   - **AssessmentType**: Describes the type of assessment (e.g., New for newly conducted assessments).
   - **IsCompleted**: Indicates whether the assessment was completed (1 = Yes, 0 = No).
   - **IsDeleted**: Indicates whether the assessment has been deleted (1 = Yes, 0 = No).
## Model Description

This project implements three models:

1. **Baseline Classifier**: A baseline machine learning model (e.g., Logistic Regression) is used to predict recidivism without any bias reduction techniques.

2. **Regular Classifier**: A neural network model that uses the COMPAS dataset for recidivism prediction. This model doesn't include any debiasing techniques.

3. **Adversarial Debiasing Model**: This model extends the regular classifier by adding an adversarial network to reduce bias. The adversary is trained to predict sensitive attributes (e.g., race) from the hidden layers of the classifier, and the classifier is trained to fool the adversary while making accurate recidivism predictions. This setup encourages the model to make predictions that are less dependent on sensitive features, thus reducing bias.

## Usage

1. **Preprocessing**: First, preprocess the COMPAS dataset by running the `data_preprocessing.py` script.
    ```bash
    python data_preprocessing.py
    ```

2. **Training Baseline Classifier**: Train the baseline model without any debiasing.
    ```bash
    python train_baseline.py
    ```

3. **Training Adversarial Debiasing Model**: Train the model with adversarial debiasing to reduce bias.
    ```bash
    python train_adversarial.py
    ```

4. **Evaluation**: Evaluate the performance and fairness of the models by running the `evaluation.py` script.
    ```bash
    python evaluation.py
    ```

## Results

The adversarial debiasing model aims to balance prediction accuracy with fairness by reducing the dependence of the recidivism predictions on sensitive attributes like race. Results and visualizations are available in the `results/` folder after running the scripts.

Key metrics evaluated include:

- Accuracy
- Fairness metrics (e.g., demographic parity, equal opportunity)

## Contributing

We welcome contributions! Feel free to submit pull requests for new features, bug fixes, or improvements.

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
