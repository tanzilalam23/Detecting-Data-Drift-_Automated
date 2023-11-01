# Data Drift Analysis

## Abstract

Data drift refers to a shift in the distribution of unseen input data compared to the training data. In the context of deploying a production pipeline, maintaining similarity between processed reports and the trained data is crucial. Analyzing reports from different domains (e.g., radiotherapy) poses a risk of poor quality abstractions, potentially leading to incorrect clinical inferences and risking patient safety. Data drift may also stem from differences in report layouts. This project aims to assess data drift in unseen reports compared to the training dataset.

## Workflow

The project primarily involves processing OCR reports, converting them into text files, and conducting operations to detect data drift. The pipeline includes the following steps:

1. **Analysis Module**: Imports `datadrift_module`.
2. **Datadrift Module**: Imports `preprocessing_module`. Utilizes `threshold`, `train`, and `model` from `train_module`.
3. **Train Module**: Calculates thresholds, models, train embeddings, and vectors for TF-IDF and Word2Vec vectorization.

## Steps/Operations

This section describes the functions and features of four core modules:

### 1. Train Module

This module calculates and saves thresholds, models, train embeddings, and vectors for TF-IDF and Word2Vec vectorization using the training and validation datasets.

#### a. Word2Vec Function
   - Calculates the Word2Vec vectorizer model and train_embeddings.
   - Computes cosine mean similarity and determines the 10th percentile as the threshold.

#### b. TF-IDF Function
   - Computes TF-IDF vectorization.
   - Calculates cosine mean similarity and establishes the 10th percentile as the threshold.

### 2. Preprocessing Module

This module preprocesses both the training and unseen datasets to prepare the text data for further operations. Customization is possible based on specific requirements.

### 3. Datadrift Module

The central module for data drift calculation. The `predict_data_drift` function takes unseen dataset and a boolean result (for TF-IDF or Word2Vec calculation).

- Preprocesses the unseen dataset and checks if TF-IDF or Word2Vec calculation is required.
- Utilizes previously saved variables (thresholds, vectorizers, train data) from the Train Module to compute data drift.
- Notifies if data drift exists between each unseen document and the training document.

### 4. Analysis Module

Importing the Datadrift Module, this module calls the `predict_data_drift` function with parameters (i.e., location of the unseen dataset) to analyze and report the results.

## Note

Modules can be adapted and customized as needed to fit specific project requirements. The descriptions provide an overview of their responsibilities and intended functionalities.
