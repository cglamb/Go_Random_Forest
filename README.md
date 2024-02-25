# Random Forest Analysis in Golang

**Author:** Charles Lamb  
**Contact Info:** charlamb@gmail.com  
**GitHub Project URL:** [Go Random Forest](https://github.com/cglamb/Go_Random_Forest)  
**Git Clone Command:** `git clone https://github.com/cglamb/Go_Random_Forest.git`

## Introduction
This project evaluates the performance of a random forest model across three programming languages: Golang, R, and Python. It aims to compare runtime and resource utilization using identical datasets, tree counts, and features considered at each split. This work extends previous research on voting ensembles found [here](https://github.com/cglamb/Voting_Ensemble_Spam), incorporating EDA, data scrubbing, text preprocessing, and tokenization from that project. The data, a labeled SMS spam dataset from UCI Machine Learning and Esther Kim, is available on [Kaggle](https://www.kaggle.com/datasets/uciml/sms-spam-collection-dataset?resource=download).

## Experiment Design
Data processing is handled in `Data_Prep.ipynb`, producing test and training datasets split 50/50, saved as CSVs in the `/Data` folder for consistency across languages.

## Overall Findings
The table below summarizes the runtime and F-score of five models in Golang, R, and Python, highlighting significant differences in performance and scaling:

| # Trees | Features at Split | Go RunTime (secs) | Go Test F-Score | R RunTime (secs) | R Test F-Score | Python RunTime (secs) | Python Test F-Score |
|---------|-------------------|-------------------|-----------------|------------------|----------------|-----------------------|---------------------|
| 10      | 10                | 4.84              | 0.70            | 57.19            | 0.96           | 2.16                  | 0.73                |
| 100     | 10                | 23.82             | 0.74            | 377.31           | 0.96           | 2.46                  | 0.77                |
| 100     | 50                | 79.75             | 0.85            | 421.15           | 0.98           | 2.57                  | 0.83                |
| 100     | 100               | 128.96            | 0.86            | 374.77           | 0.98           | 2.71                  | 0.84                |
| 1000    | 10                | 299.60            | 0.73            | 3608.73          | 0.96           | 6.89                  | 0.84                |

*Note: Some metrics were not measured.

Despite differences in default parameters and random seeding, the models' similar F-scores suggest comparable effectiveness, with R models outperforming others in F-score, warranting further investigation.

## Recommendation
Python offers better runtime performance and scalability than Go, especially when considering cloud computing costs. This suggests Python's computational efficiency is superior for random forest models, likely due to the robust sklearn library.

## Implementations
- **Golang**: Utilizes Andy Sun's random forest library with concurrent tree calculations.
- **R**: Uses Breiman and Cutler's random forest library, with performance monitored via R Studio.
- **Python**: Employs sklearn's RandomForestClassifier with support for parallel processing.

## Explanation of Files
- `Data.csv` - Raw data, requires manual extraction to a `Data` folder.
- `/Logs/` - Contains logs for Go, R, and Python codes, including data preparation logs.
- `Data_Prep.ipynb` - Jupyter notebook for data preparation.
- `RF.go`, `RF_test.go`, `RF.r`, `RF.py` - Implementation files for Golang, R, and Python.
- `RF_go.exe` - Executable for the Golang implementation.

## Areas of Further Research / Enhancement
Future work could address the imbalance in the dataset, explore alternative libraries in Golang for flexibility in parameter tuning, and evaluate the documentation and functionality of the used Golang library against alternatives like the malaschitz Random Forest library.
