# US Census Income

The goal of this project is to identify characteristics that are associated with a person earning more than $50K.

## Executive Summary

TBD - please see the attached [slides]().

---- 

The following order is recommended to review the code:
- [notebooks/0-EDA](notebooks/0-EDA.ipynb)
- [recipes/1-Preprocessing](recipes/1-Preprocessing.ipynb)
- [recipes/2-Modeling](recipes/2-Modeling.ipynb)
- [recipes/3-Evaluation](recipes/3-Evaluation.ipynb)
Please see the exported HTML for full outputs (DSS sync clears outputs).

## Reproducibility

To reproduce the results:
1. Create new Project on DSS. 
2. Setup code env using [requirements.txt](requirements.txt)
3. Use the [flow documentation](docs/Dataiku%20Flow%20Documentation%20-%20US_CENSUS_PROJECT.docx) to
  - upload the raw data files under the right name,
  - create and run the end-to-end Flow.

## Workplan

We are aiming to carry out the following main steps:

- **Exploratory Data Analysis:** Numerical and/or graphical representations of the data that
may help inform insights and/or tactics for answering the research question of interest.
- **Data Preparation:** Data cleaning, preprocessing, feature engineering, etc., that may aid in improving data clarity & model generation.
- **Data Modeling:** The building of a few competing models to predict the target variable (earn $50K+).
- **Model Assessment:** A selection of the best model based on performance comparisons.
- **Results:** A concise summary of key findings, recommendations, & future improvements.

## Work Log

- Day 1: setup & baselines.
  - Setup Dataiku DSS: project, resources and custom environemnt, Github integration
  - EDA: research & understand the data, plan for data cleaning and preparation
  - Basic data preprocessing
  - Baseline modeling and evaluation
- Day 2: model optimization.
  - Iterate on data prep to process all features
  - Add HP tuning and address imbalance
  - Improve evaluation and add interpretation
  - Presentation outline
- Day 3: review and refine.
  - Finalize code and sync with Github
  - Finalize and export presentation
  - Finalize Github repo (readme), ensure reproducibility

## Tech Stack & Implementation

We have used Dataiku DSS Cloud to develop the Python notebooks and organize flows for testing, training and evaluation. The recipes and notebooks we created are synced with this current repo. For convenience, we also exported an HTML version of each notebook (the DSS -> Github push does not keep output cells).

Core libraries used:
- Pandas and numpy for processing
- Matplotlib and plotly for visuals
- MLFlow for model tracking and saving
- XGBoost for modelling
- Optuna for HP tuning

We exported the requirements file for easier reproducibility.

**Notes**:
- Our original plan was to use PySpark for data processing and model training to create a scalable flow, however our free-trial DSS subscription did not include the Spark integration.
- The following libraries were not available to install due to "OSError: Permission Denied", likely another limitation of the tree trial:
  - `plotly` for interactive visualization
  - `optuna` for HP tuning
 


## Key Reference

- Dataiku
  - Tracking
    - https://doc.dataiku.com/dss/latest/mlops/experiment-tracking/tracking.html
    - https://doc.dataiku.com/dss/latest/mlops/mlflow-models/limitations.html
- XGBoost
  - https://github.com/optuna/optuna-examples/blob/main/xgboost/xgboost_cv.py
  - https://xgboost.readthedocs.io/en/latest/python/python_api.html