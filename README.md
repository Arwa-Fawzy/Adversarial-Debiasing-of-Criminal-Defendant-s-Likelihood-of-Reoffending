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

## Dataset

The dataset used in this project is the COMPAS dataset, which contains demographic and criminal history data on defendants. For more details on the dataset, please refer to the [COMPAS dataset documentation](https://github.com/propublica/compas-analysis).

- **Features**: Demographics, criminal history, and recidivism prediction scores.
- **Target**: Whether the defendant reoffends within two years.

You can download the dataset [here](https://github.com/propublica/compas-analysis/blob/master/compas-scores-two-years.csv).

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
