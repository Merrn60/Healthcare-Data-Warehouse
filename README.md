# Healthcare Data Warehouse

A data warehouse project developed for the Data Warehouse course at Ahram Canadian University (Year 4, Software Engineering). The project analyzes medical lab results (e.g., Hemoglobin, Glucose, Cholesterol) using Star and Snowflake schemas.

## Overview
This project builds a data warehouse to analyze average lab measurements across patient demographics (Age, Gender) and diseases (e.g., Anemia, Diabetes). It includes:
- **Star Schema**: Fact table (`Fact_Health_Metrics`) with dimensions (`PatientDimension`, `DiseaseDimension`, `Dim_LabResults`).
- **Snowflake Schema**: Normalized version with additional tables (e.g., `GenderType_sf`, `Location_sf`).
- **SQL Queries**: 10 analytical queries to gain insights (e.g., average Hemoglobin by disease risk, patients with high Glucose).

## Setup
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Merrn60/Healthcare-Data-Warehouse.git
   ```
2. **Import Data**:
   - Use `data/laboratory_data.csv` (dataset with 12,009 rows of lab results).
   - Import into MySQL or any SQL database using:
     ```sql
     LOAD DATA INFILE 'laboratory_data.csv' INTO TABLE source_data FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' IGNORE 1 ROWS;
     ```

## Files
- `data/`:
  - `laboratory_data.csv`: Raw dataset with lab results (Gender, Age, Hemoglobin, Glucose, etc.).
- `docs/`:
  - `DWH_project.pdf`: Project documentation (schemas, queries, results).

## Usage
- The project includes 10 analytical SQL queries in the PDF (`docs/DWH_project.pdf`). Examples:
  ```sql
  -- Query 1: Average Hemoglobin by Disease Risk Level
  SELECT dd.RiskLevel, AVG(fhm.Avg_Hemoglobin)
  FROM Fact_Health_Metrics fhm
  JOIN DiseaseDimension dd ON fhm.DiseaseID = dd.DiseaseID
  GROUP BY dd.RiskLevel
  HAVING AVG(fhm.Avg_Hemoglobin) > 12;

  -- Query 2: Patients with High Glucose or Cholesterol
  SELECT pd.PatientID, pd.Age, pd.Gender, fhm.Avg_Glucose, fhm.Avg_Cholesterol
  FROM Fact_Health_Metrics fhm
  JOIN PatientDimension pd ON fhm.PatientID = pd.PatientID
  WHERE fhm.Avg_Glucose > 200 OR fhm.Avg_Cholesterol > 240;
  ```

## Team
- Rawan Elsayed Hisham (Team Leader)
- Salma Abdrabo Abdelbary
- Omar Esam Shokry
- Yassa Khalil Naguip
- Mustafa Safwat
- Abdelwahab Ashraf

## License
MIT License
