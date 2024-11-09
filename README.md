
# Food Inspections of Dallas and Chicago

## MIDTERM PROJECT - DAMG 7370
**Designing Advanced Data Architectures for Business Intelligence**

### Team Members
- Dharun Karthick Ramaraj
- Nitin Sai Varma Indukuri
- Nikhil Godalla
- Linata Deshmukh

---

## Tools Used

### Part 1: Data Profiling
- **Python**: `ydata_profiling`
- **Staging**:
  - Talend
  - MySQL

### Part 2: Dimensional Modeling
- **E/R Studio Data Architect**

### Part 3: Loading
- Talend
- MySQL

### Part 4: Visualizations
- PowerBI
- Tableau

---

## Dataset: Food Inspections
This dataset includes detailed inspections of food establishments in Chicago and Dallas, reflecting efforts to maintain public health and safety standards. Data points include establishment names, locations, inspection dates, scores, and violations.

- **Chicago**: Data from the Chicago Department of Public Health’s Food Protection Program.
- **Dallas**: Data from the Code Compliance Services Department's Consumer Health Division.

### Key Dataset Information
- **Scope**: Restaurant and Food Establishment Inspections (October 2016 to Present)
- **Attributes**: Establishment name, physical location, inspection date, inspection score, individual violation points.

---

## Project Deliverables

### Staging Tables

#### Chicago Staging Table
```sql
CREATE TABLE `stg_chicago_foodinspection` (
  `ChicagoUID` int NOT NULL,
  `Inspection_ID` int DEFAULT NULL,
  `DBA_Name` varchar(100) DEFAULT NULL,
  ...
);
```

#### Dallas Staging Table
```sql
CREATE TABLE `stg_dallas_foodinspection` (
  `DallasUID` int NOT NULL,
  `Restaurant_Name` varchar(65) DEFAULT NULL,
  ...
);
```

### Data Profiling Analysis

#### Chicago Insights
- **Multi-Valued Attributes**: The 'Violations' column is split into atomic data fields.
- **Data Type Conversions**: Numeric fields and text consistency assessed.
- **Data Imbalance**: Strategies for 'State' field and missing values.

#### Dallas Insights
- **Multi-Valued Attributes**: Separate multi-valued attributes into columns.
- **Data Type Conversions**: Encoding techniques applied as necessary.
- **Handling Missing Values**: Strategies for high missingness and imbalance addressed.

### Dimensional Data Model (ER/Studio)

#### Fact Tables
- **FACT_FoodInspection**: Contains quantitative data for each food inspection.
- **FACT_ViolationInspection**: A bridge table indicating a many-to-many relationship between inspections and violations.

#### Dimension Tables
- **DIM_Date**: Hierarchy for time-based analysis.
- **DIM_Risk**: Categorizes inspections by risk level.
- **DIM_InspectionType**: Categorizes inspection types.
- **DIM_Violation**: Details types of violations.
- **DIM_FoodPlaces**: Information about inspection locations.

---

## SQL DDL Scripts

### Bridge_Violations Table
```sql
CREATE TABLE `bridge_violation` (
  `BridgeSK` int NOT NULL,
  ...
);
```

### Dim_Date Table
```sql
CREATE TABLE `dim_date` (
  `DateSK` int NOT NULL,
  ...
);
```

### Dim_foodplaces Table
```sql
CREATE TABLE `dim_foodplaces` (
  `FoodPlacesSK` int NOT NULL,
  ...
);
```

### Other Tables
SQL scripts for `dim_inspectiontype`, `dim_risk`, `dim_violation`, and `fact_inspection` are also included in this repository.

---

## Talend Jobs and Target Table Row Counts

### Talend Jobs Overview
1. **Stage_ChicagoFoodInspection**
2. **Stage_DallasFoodInspection**
3. **Transform01_ChicagoFoodInspection**
4. **Transform01_DallasFoodInspection**
5. **Transform02_Merge**
6. **Load_DateDimension**
7. **Load_InspectionTypeDimension**
8. **Load_RiskDimension**
9. **Load_ViolationDimension**
10. **Load_BridgeTable**
11. **Load_InspectionFact**

### Target Table Row Counts
1. Bridge Violations
2. DateDimension
3. FoodPlacesDimension
4. InspectionTypeDimension
5. RiskDimension
6. ViolationDimension
7. InspectionFact

---

## Contact
For more information, please contact one of the team members.

