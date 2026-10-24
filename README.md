# Medical Appointment Data Cleaning Pipeline

## Overview

This project focuses on cleaning and investigating a medical appointment dataset using **PySpark** in Databricks.

The goal is to explore real-world data quality issues, apply data cleaning techniques, standardize columns and data types, and prepare a cleaner dataset for further analysis.

The project uses the Medical Appointment No-Show dataset, which contains information about patients, scheduled appointments, medical conditions, and whether patients attended their appointments.

## Objectives

- Load a CSV dataset into a PySpark DataFrame.
- Explore inferred and custom schemas.
- Standardize column names.
- Investigate missing and invalid values.
- Create derived columns for appointment status and age groups.
- Cast columns to appropriate data types.
- Investigate duplicate records and appointment IDs.
- Check binary indicator columns for unexpected values.
- Produce a cleaned DataFrame for downstream analysis.

## Dataset

**Dataset:** Medical Appointment No-Show  
**File:** `KaggleV2-May-2016.csv`

The dataset contains appointment information, including:

| Column | Description |
|---|---|
| PatientId | Unique identifier associated with a patient |
| AppointmentID | Appointment identifier |
| Gender | Patient's gender |
| ScheduledDay | Date and time the appointment was scheduled |
| AppointmentDay | Date and time of the appointment |
| Age | Patient's age |
| Neighbourhood | Location of the medical facility |
| Scholarship | Indicates participation in the Bolsa Família program |
| Hipertension | Indicates whether the patient has hypertension |
| Diabetes | Indicates whether the patient has diabetes |
| Alcoholism | Indicates whether the patient has alcoholism |
| Handcap | Indicates disability status |
| SMS_received | Indicates whether an SMS reminder was received |
| No-show | Indicates whether the patient missed the appointment |

The dataset can be obtained from [Kaggle – Medical Appointment No Shows](https://www.kaggle.com/datasets/joniarroba/noshowappointments).

## Tools and Technologies

- **Python**
- **Apache Spark / PySpark**
- **Databricks**
- **PySpark DataFrames**
- **Git and GitHub**

## Project Workflow

### 1. Data Ingestion and Schema Exploration

- Loaded the CSV file into a PySpark DataFrame.
- Inspected the inferred schema.
- Defined a custom schema using `StructType` and `StructField`.
- Compared inferred and custom schemas.

### 2. Column Selection and Renaming

Standardized column names using snake_case.

Examples:

- `PatientId` → `patient_id`
- `AppointmentID` → `appointment_id`
- `ScheduledDay` → `scheduled_day`
- `AppointmentDay` → `appointment_day`
- `No-show` → `no_show`

### 3. Data Investigation

Investigated records based on:

- Negative ages.
- Patients under 18.
- Missed appointments.
- Missed appointments where an SMS was received.
- Missed appointments among patients with scholarships.
- Missed appointments among patients with hypertension and diabetes.
- Null values in age and neighbourhood.

### 4. Column Transformation

Created and modified columns using PySpark functions.

Derived columns include:

- `data_source` — identifies the dataset source.
- `appointment_status` — indicates whether the patient showed up or missed the appointment.
- `age_group` — groups patients into age ranges.

Also standardized gender values to uppercase and renamed `no_show` to `no_show_flag`.

### 5. Data Type Casting and Sorting

- Cast appointment dates to timestamp types.
- Cast age to integer.
- Ensured medical indicator columns use integer types.
- Sorted records by age and appointment date for inspection.

### 6. Duplicate Investigation

- Investigated full-row duplicates.
- Removed exact duplicate records.
- Investigated duplicate `appointment_id` values.
-
