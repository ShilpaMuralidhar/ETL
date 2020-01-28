# Extraction, Transform, Load: ETL REPORT ON VEHICLE-RELATED FATAL ACCIDENTS IN TEXAS

## Team members:  Shilpa Muralidhar, Lisa Cannon

## Overview:

We extracted crash information from the National Highway Traffic Safety Administration’s Fatality Analysis Reporting System (NHTSA-FARS) about fatal accidents that occurred in Texas in 2016.  There are 9,022 fatalities listed and 123 fields of information provided regarding the conditions and details of the traffic incident that resulted in fatality. The information extracted uses a number coding system to identify categories.  The number code is identified in a separate table. We chose fields of our interest and converted their number codes into meaningful text information using the coding tables. 
All these data were then loaded onto SQL for further querying.

### 1. EXTRACTION
We learnt about driving related accidents through Kaggle which linked to FARS (Fatality Analysis Reporting System), https://www-fars.nhtsa.dot.gov. All our data was obtained from https://www-fars.nhtsa.dot.gov website. Our Data set contains vehicle associated fatal incidents with in the state of Texas, in the year 2016. This dataset contains Pre-Crash and Crash relevant information with: State Number, Case number (Case Number represents each fatal accident) and Vehicle Number being common to both Pre-Crash and Crash fields. 
Data within the variables in the Pre-Crash and Crash fields are number coded. Each number code further represents details associated with fatalities. Each representation table has codes in one column and its interpretations as another column. Excel files of field tables and their interpretation tables were first downloaded, cleaned for irrelevant labels, and finally converted to CSV files.

A.	Pre-Crash Information

i.	Variables in Pre-Crash field included: Crash Type, Driver Distracted By, Driver Maneuvered to Avoid, Driver’s Vision Obscured By.


### 2.	TRANSFORM (DATA CLEANING)
All the data cleaning was performed in Jupyter Notebook using Pandas and Excel. Pre-Crash table were imported into Pandas DataFrame.

i.	All Null values were removed using dropna().

ii.	Values of Case Number and Vehicle Number was converted to string, and leading zeros were added using pd.zfill() method.

iii.	Unique VehicleID was then created by combining zfill(ed) Case Number and Vehicle Number.

iv.	Driver Distraction column contained two values for 7 cases.  This meant the driver was distracted by more than one event.  Therefore, this column was duplicated and both columns were cleaned to have only one value in each cell.

v.	To change the values from numeric to its interpreted meaning, specific Code Definition tables were imported and pd.merge () was used to replace the numbers to its interpretation.

vi.	Columns were renamed as State Number, Case Number, Crash Type, First and Second Distraction, Driver Action and Obscured Vision.
  
 
### 3.	LOAD
Transformed Pre_crash_data.ipynb and FARS_data.ipynb in Jupyter NoteBook was later loaded in a Postgres SQL database. Postgres SQL was chosen because the data is organized in a table-based relational format. Two tables named crashinfo and crashdistraction were created in SQL.   The primary key for the crashdistraction table is VehicleID.  This field is used as the foreign key in crashinfo.  The primary key for crashinfo is PersonID.
