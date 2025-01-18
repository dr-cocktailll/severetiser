# Maritime Deficiency Severity Prediction Model

This repository contains a machine learning-based approach to predict the severity levels of maritime deficiencies identified during inspections. The model integrates structured and unstructured data to assist inspectors in prioritizing high-risk issues.

---

## Table of Contents

1. [Introduction](#introduction)  
2. [Methodology](#methodology)  
   - [Data Preparation](#data-preparation)  
   - [Feature Engineering](#feature-engineering)  
   - [Weight Optimization](#weight-optimization)  
   - [Text and Feature Combination](#text-and-feature-combination)  
   - [Model Training](#model-training)  
   - [Prediction](#prediction)  
3. [Results](#results)  
4. [Handling Unstructured Text](#handling-unstructured-text)  

---

## Introduction

The model predicts severity levels ("Low," "Medium," or "High") for maritime deficiencies using structured data and unstructured textual descriptions. By balancing interpretability and accuracy, the approach provides actionable insights to prioritize high-risk deficiencies, enhancing safety and compliance in maritime operations.

---

## Methodology

### Data Preparation

The training and test datasets are preprocessed to ensure compatibility with machine learning workflows.

### Feature Engineering

Key features engineered for the model include:

1. **Time Difference Normalization**: Represents time since the last inspection (`time_diff_normalized`).
2. **Vessel Type Weights**: Assigns risk-based weights to vessel categories (e.g., Chemical, Dry Bulk).
3. **Port-Based Risk Scores**: Calculates port risk scores based on the proportion of high-severity incidents.
4. **Authority-Based Risk Scores**: Evaluates inspection authorities based on their historical association with high-severity deficiencies.
5. **Textual Features**: Vectorizes deficiency descriptions (`def_text`) using TF-IDF to extract meaningful patterns.

### Weight Optimization

A linear regression model quantifies the impact of each predictor on severity. The optimized coefficients are normalized into weights, creating a combined feature (`combined_weight`) for severity prediction.

### Text and Feature Combination

Textual features (TF-IDF matrix) are combined with structured numeric features to ensure all data types contribute to predictions.

### Model Training

A Random Forest Classifier is trained to capture nonlinear interactions between features. The model is evaluated using metrics such as accuracy, precision, recall, and F1-scores.

### Prediction

The trained model predicts severity levels for the test dataset, mapping predictions back to "Low," "Medium," or "High."

---

## Results

- **Validation Accuracy**: 98.9%

---

## Handling Unstructured Text

The model processes textual descriptions using NLP, machine learning, and graph database technologies:

1. **Text Severity Analysis**:  
   - Text is tokenized using SpaCy, removing stop words and punctuation.  
   - Tokens are classified using Hugging Face's `distilbert-base-uncased` model, mapping probabilities to severity scores.  
   - A weighted average of token scores determines the overall severity.

2. **Neo4j Knowledge Graph**:  
   - Metadata and severity scores are stored in a Neo4j graph.  
   - Nodes represent entities (e.g., vessels, incidents), while edges capture relationships (e.g., "IMPACTS").  
   - The graph allows contextual queries, such as retrieving high-risk deficiencies by vessel type.
