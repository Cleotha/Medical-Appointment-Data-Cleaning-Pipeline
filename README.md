# Medical Appointment Data Cleaning Pipeline

## Project Overview

This project focuses on cleaning and validating a medical appointment dataset using **PySpark in Databricks**.

The dataset contains information about medical appointments, including patient demographics, appointment dates, health indicators, scholarship status, SMS notifications, and whether a patient attended their appointment.

The goal is to investigate data quality issues, standardize the dataset, and prepare it for reliable downstream analysis.

## Dataset

- **Dataset:** Medical Appointment No-Show
- **Source:** [Kaggle – Medical Appointment No Shows](https://www.kaggle.com/datasets/joniarroba/noshowappointments)
- **File:** `KaggleV2-May-2016.csv`

The dataset includes fields such as:

- Patient ID
- Appointment ID
- Gender
- Scheduled Day
- Appointment Day
- Age
- Neighbourhood
- Scholarship
- Hypertension
- Diabetes
- Alcoholism
- Handicap
- SMS Received
- No-show status

## Tools and Technologies

- Python
- Apache Spark
- PySpark
- Databricks
- CSV
- Git and GitHub

## Project Workflow

### 1. Data Ingestion and Schema Definition

- Loaded the medical appointment dataset into a PySpark DataFrame.
- Explored the inferred schema.
- Defined a custom schema using PySpark data types.
- Compared the inferred schema with the custom schema.

### 2. Column Selection and Standardization

- Renamed columns to lowercase snake_case.
- Standardized column names for easier access and consistency.
- Created an alias for the patient identifier during column selection.

### 3. Data Exploration and Filtering

Investigated records based on:

- Negative patient ages.
- Patients under 18.
- Patients who missed appointments.
- No-shows among patients who received SMS notifications.
- No-shows among patients with scholarship status.
- No-shows among patients with selected health conditions.
- Missing values in age and neighbourhood columns.

### 4. Creating and Modifying Columns

Created additional fields to support analysis:

- `data_source`: Identifies the dataset source.
- `appointment_status`: Categorizes appointments as Show or No-show.
- `age_group`: Groups patients into age categories.
- `no_show_flag`: Standardized no-show field.
- `age_validation_status`: Flags unusual age values for further investigation.

Also standardized gender values to uppercase.

### 5. Data Type Casting and Sorting

- Cast appointment dates to timestamp data types.
- Cast age and health indicator columns to integer types.
- Sorted records by age and appointment date.
- Used row limits to inspect manageable samples of the dataset.

### 6. Duplicate Investigation

- Identified duplicate rows using all dataset columns.
- Removed exact duplicate records.
- Investigated duplicate appointment IDs.
- Examined repeated patient IDs.

Repeated patient IDs were investigated separately because one patient may have multiple appointments.

### 7. Data Quality Validation

#### Date Validation

Investigated:

- Appointments scheduled before the appointment date.
- Missing appointment or scheduled dates.
- Appointments occurring on the same calendar day.

Date records were inspected before making cleaning decisions.

#### Age Validation

Investigated:

- Negative ages.
- Ages above 100.
- Null ages.
- Age-zero records.

Created an `age_validation_status` column to classify age values as:

- `valid`
- `invalid_age`
- `review_age`

Unusual values were flagged for investigation rather than automatically removed.

#### Indicator Validation

Checked the following columns for values outside the expected binary range of 0 and 1:

- `scholarship`
- `hypertension`
- `diabetes`
- `alcoholism`
- `handicap`
- `sms_received`

## Key Data Engineering Concepts Practiced

- PySpark DataFrame operations
- Schema definition and data type casting
- Data profiling and exploration
- Column standardization
- Duplicate detection and removal
- Date validation
- Data quality checks
- Conditional column creation
- Data validation and record flagging
- Preparing datasets for downstream analytics

## Project Outcome

The project demonstrates how PySpark can be used to investigate and improve the quality of a real-world dataset.

Rather than automatically deleting unusual records, the pipeline emphasizes data profiling, validation, and informed cleaning decisions. This helps preserve potentially useful information while making data quality issues visible.

## Future Improvements

- Add automated data quality tests.
- Build a reusable validation function for indicator columns.
- Investigate duplicate appointment IDs and determine appropriate handling.
- Handle invalid age and date records based on documented business rules.
- Save the cleaned dataset in Parquet or Delta format.
- Add logging to track pipeline execution and data quality results.
- Schedule the pipeline using Apache Airflow.

## Author

**Marydoris Chidiebere**

Aspiring Data Engineer | Mathematics Student | PySpark & Databricks
