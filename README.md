# deep_learning_1

# 🏥 ICU Mortality Prediction with SVM

This project explores whether diagnosis descriptions in ICU admissions can help predict **in-hospital mortality**, using text mining and supervised learning techniques on the **MIMIC** dataset.

## 📚 Overview
We build a prediction model to classify ICU patients based on whether they died during their hospitalization (`HOSPITAL_EXPIRE_FLAG`). The main features include diagnosis descriptions and other structured clinical variables.

## 🧹 Data Understanding and Preprocessing

### Identifiers
- `subject_id`: unique patient
- `hadm_id`: hospital admission (can repeat)
- `icustay_id`: unique ICU stay
- `ICD9_CODE`: diagnosis codes (can repeat across patients)

### Merging and Cleaning
- Merged primary dataset with `MIMIC_metadata_diagnose` to include **long diagnosis descriptions**
- Created a unified diagnosis column aggregating secondary diagnoses

## ✂️ Text Analysis

### Subgrouping
Split the dataset into two groups:
- Deceased patients (`HOSPITAL_EXPIRE_FLAG=1`)
- Surviving patients (`HOSPITAL_EXPIRE_FLAG=0`)

### Document-Term Matrix (DTM)
- Constructed DTMs for `LONG_DESCRIPTION` and `DIAGNOSIS`
- Identified diagnosis-related words **uniquely or more frequently appearing among deceased patients**
- Created a binary feature `selected_words` = 1 if any of these keywords appear in the diagnosis text

> 🧠 Among 913 deceased patients, 418 had `selected_words` = 1. The variable isn't perfectly predictive, but adds meaningful signal.

## 📊 Feature Engineering
- Number of secondary diagnoses
- Frequency of hospitalization per patient
- Simplified and grouped `MARITAL_STATUS` and `ETHNICITY`
- Parsed `ADMITTIME` to extract features like day/month
- Calculated **patient age** from date of birth and admission date

## 📈 Analysis and Modeling

### Exploratory Analysis
- Compared distribution of features (e.g., age, ethnicity, diagnosis patterns) across the two groups (deceased vs. survived)

### Classification Model
- Trained a **Support Vector Machine (SVM)** classifier using the selected features, including `selected_words`, demographics, and counts
- Evaluated model performance and discussed limitations (e.g., imperfect alignment between text and outcome)

## 📂 Files
- `Project1_Noemi.ipynb`: all steps from data merging to classification

## 👤 Author
Noemi Lucchi  
Text Mining Project — BSE 2024–2025
