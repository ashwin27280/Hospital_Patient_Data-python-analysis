# Hospital Patient Data Analysis

This project performs a basic statistical analysis on hospital patient data using Python and the **pandas** library. The goal is to clean, transform, and merge patient records and billing information to create a comprehensive dataset for billing analysis.

## Problem Statement

A hospital has two datasets: one with patient details and another with billing information. The patient dataset contains some missing bill amounts and duplicate records due to follow-up visits. The task is to process these datasets to:

- Clean and preprocess the data.
- Calculate total bill amounts per department.
- Merge patient and billing data.
- Incorporate new patient and billing information.

## Datasets

| File | Description | Columns |
|------|-------------|---------|
| `Patient_Data.csv` | Patient visit and treatment records | `PatientID`, `Name`, `Department`, `Doctor`, `BillAmount`, `ReceptionistID`, `CheckInTime` |
| `Billing_Data.csv` | Insurance and final payment details | `PatientID`, `InsuranceCovered`, `FinalAmount` |

Both files are read into pandas DataFrames and inspected using `.info()`, `.head()`, `.isnull().sum()`, and `.duplicated().sum()` to understand structure, missing values, and duplicate records before any cleaning is done.

## Key Tasks Performed

1. **Data Loading & Initial Exploration**
   Loaded both CSV files into DataFrames and reviewed their shape, data types, missing values, and duplicate rows.

2. **Column Selection**
   Selected only the columns relevant to billing analysis (`PatientID`, `Department`, `Doctor`, `BillAmount`) from the patient dataset.

3. **Dropping Administrative Columns**
   Removed non-essential administrative columns (`ReceptionistID`, `CheckInTime`) from the patient dataset.

4. **Department-wise Billing Summary**
   Used `groupby('Department')['BillAmount'].sum()` to calculate the total bill amount per department.

5. **Duplicate Removal**
   Identified and removed duplicate patient records (caused by follow-up visits) using `drop_duplicates(subset=['PatientID'])`, keeping one record per patient.

6. **Missing Value Handling**
   Filled missing `BillAmount` values with the **mean bill amount** so no patient record is left with incomplete billing data.

7. **Merging Datasets**
   Merged the cleaned patient dataset with the billing dataset on `PatientID` using an inner join, combining treatment details with insurance and final payment information.

8. **Adding New Patients (Row-wise Concatenation)**
   Simulated incoming weekly data by concatenating new patient records (new `PatientID`s, names, departments, doctors, and bill amounts) onto the existing dataset using `pd.concat()`.

9. **Adding New Billing Fields (Column-wise Concatenation)**
   Demonstrated column-wise concatenation by appending additional `InsuranceCovered` and `FinalAmount` columns, and calculated `FinalAmount` as `BillAmount - InsuranceCovered` for the merged dataset.

## Tech Stack

- **Python 3**
- **pandas** – data cleaning, transformation, merging
- **numpy** – numerical operations
- Developed and tested in **Google Colab**

## How to Run

1. Clone this repository.
2. Open `Hospital_patient.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
3. Ensure `Patient_Data.csv` and `Billing_Data.csv` are available (upload them when prompted if using Colab).
4. Run all cells sequentially to reproduce the cleaning, aggregation, and merging steps.

## Project Structure

```
├── Hospital_patient.ipynb   # Main analysis notebook
├── Patient_Data.csv         # Patient records (input)
├── Billing_Data.csv         # Billing records (input)
└── README.md                # Project documentation
```
## Summary
At the end, we get one clean table that combines patient details, department info, and billing info together. It has no missing values and no duplicate patients. This final table is ready to use for reports or further analysis.
