# US Census Income

## Executive Summary

The goal of this project was to identify characteristics that are associated with income, a person earning more than $50K, based a sample dataset from the US Census archive containing detailed, but anonymized, information for ~300,000 individuals.

Our initial data exploration uncovered 
- a number of data quality issues (e.g., null values, duplicate rows),
- major skew in univariate distributions, in particular only 8% of samples are in the high income category after deduplication,
- statistically significant relationship between income and a number of education, employment and family indicators. 

After the preprocessing of a mix of numeric and categorical features, we optimized an XGBoost binary classification model finetuning over a number of hyperparameters. We addressed the data imbalance through using an adequate evaluation metric (AUC-PR) and class weights, to achieve a final predictive model of .50 F1 score (with 74% precision and 38% recall) on the final test set. 

Analysing feature importance highlighted sex, education and employment indicators as most significant, reaffirming a well-know bias in this historical dataset.

Please see the attached [presentation](presentation/US%20Census%20-%20Income%20Prediction.pdf) for a more detailed summary.

**Note**: while being practical in some situations, for this project we chose not to use generative AI (e.g. Cursor, Copilot) in writing the code or the accompanying documentation/materials. We did use the built-in DSS chatbot for Q&A on the Dataiku Python SDK.

## Contents

The following order is recommended to review the code:
- [notebooks/0-EDA](notebooks/0-EDA.ipynb)
- [recipes/1-Preprocessing](recipes/1-Preprocessing.ipynb)
- [recipes/2-Modeling](recipes/2-Modeling.ipynb)
- [recipes/3-Evaluation](recipes/3-Evaluation.ipynb)

Please see the exported HTML for full outputs (DSS sync clears outputs). The `notebooks/` folder holds our standalone exploration, while the `recipes/` folder holds flow recipe notebooks.

## Reproducibility

To reproduce the results on Dataiku DSS Cloud:
1. Create a new Project. 
2. Setup custom code env using [requirements.txt](requirements.txt).
3. Use the [flow documentation](docs/Dataiku%20Flow%20Documentation%20-%20US_CENSUS_PROJECT.docx) to
  - upload the raw data files,
  - create recipes based on the notebooks, and
  - run the end-to-end Flow.

We recommend using at least CPU-2 16Gb instance for running the flow which typically completes around 6-7 minutes for 20 trials on selected features, 80-90% of the run time being the HP tuning.

## Workplan

We are aimed to carry out the following main steps:

- **Exploratory Data Analysis:** Numerical and/or graphical representations of the data that
may help inform insights and/or tactics for answering the research question of interest.
- **Data Preparation:** Data cleaning, preprocessing, feature engineering, etc., that may aid in improving data clarity & model generation.
- **Data Modeling:** The building of a few competing models to predict the target variable (earn $50K+).
- **Model Assessment:** A selection of the best model based on performance comparisons.
- **Results:** A concise summary of key findings, recommendations, & future improvements.

## Work Log

- **Day 1: setup & baselines.**
  - Setup Dataiku DSS: project, resources and custom environemnt, Github integration
  - EDA: research & understand the data, plan for data cleaning and preparation
  - Basic data preprocessing
  - Baseline modeling and evaluation

- **Day 2: model optimization.**
  - Iterate on data prep to process all features
  - Add HP tuning and address imbalance
  - Improve evaluation and add interpretation
  - Presentation outline

- **Day 3: review and refine.**
  - Finalize code and sync with Github
  - Finalize and export presentation
  - Finalize Github repo (readme), ensure reproducibility

## Tech Stack & Implementation

We have used Dataiku DSS Cloud to develop the Python notebooks and organize flows for testing, training and evaluation. The recipes and notebooks we created are synced with this current repo. For convenience, we also exported an HTML version of each notebook with the cell outputs (as the DSS -> Github push does not keep output cells).

Core libraries used:
- Pandas and numpy for processing
- Matplotlib and plotly for visuals
- MLFlow for experiment tracking
- XGBoost for modeling
- Optuna for HP tuning

We exported the requirements file for easier reproducibility.

**Notes**:
- Our original plan was to use PySpark for data processing and model training to create a scalable flow, however our free-trial DSS subscription did not include the Spark integration.
 
## Key References

- Dataiku
  - XP & Model Tracking
    - https://doc.dataiku.com/dss/latest/mlops/experiment-tracking/tracking.html
    - https://doc.dataiku.com/dss/latest/mlops/mlflow-models/limitations.html
  - Spark
    - https://doc.dataiku.com/dss/latest/spark/installation.html#unmanaged-spark-on-kubernetes
    - https://doc.dataiku.com/dss/latest/collaboration/import-notebooks-from-git.html
- XGBoost
  - https://github.com/optuna/optuna-examples/blob/main/xgboost/xgboost_cv.py
  - https://xgboost.readthedocs.io/en/latest/python/python_api.html
  - https://xgboost.readthedocs.io/en/stable/parameter.html
- MLflow and Optuna
  - https://mlflow.org/docs/latest/ml/traditional-ml/tutorials/hyperparameter-tuning/notebooks/hyperparameter-tuning-with-child-runs/
  - https://optuna.readthedocs.io/en/stable/reference/generated/optuna.trial.Trial.html
- Sklearn
  - https://scikit-learn.org/stable/api/index.html