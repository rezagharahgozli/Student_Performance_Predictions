# Student Performance Data Cleaning
A Python data-cleaning project that inspects and prepares student performance records for downstream analysis and predictive modeling. The workflow is implemented in a Jupyter notebook using pandas and NumPy.
Scope: This repository covers data inspection, quality checks, cleaning, and CSV export. It does not train or evaluate a prediction model.

## Project workflow
The notebook Student_data_cleaning.ipynb performs the following steps:
1. Load and inspect the dataset: Read the input CSV; inspect sample rows, dataset dimensions, column types, summary statistics, duplicate rows, and missing values.
2. Standardize column names and text: Rename selected columns to snake_case; normalize whitespace in names, genders, and parental-support values; inspect unusual names and category distributions.
3. Adjust data types: Convert student_id to pandas' nullable Int64 type and online_classes_taken to boolean.
4. Check invalid values and overlapping fields: Identify negative study_hours and attendance_pct values above 100, replace those invalid values with missing values, compare the overlapping attendance/study-hours columns via correlation and equality counts, and drop attendance_pct and study_hours.
5. Inspect duplicate identifiers: Check for duplicate student IDs and names, add a sequential record_id, and flag duplicated non-null student IDs in id_collision without automatically removing the associated records.
6. Handle missing data: Remove rows missing the target final_grade; fill missing name and gender with unknown; use the mode for parental_support and online_classes_taken; and fill missing numeric values with rounded column medians.
7. Export results: Write the processed dataset to data/student_performance_cleaned.csv.
## Technologies
- Python 3
- pandas
- NumPy
- Matplotlib and Seaborn (imported in the notebook; no plots are generated in the current version)
- Jupyter Notebook
## Repository structure
.
├── Student_data_cleaning.ipynb
├── requirements.txt
├── README.md
└── data/
    ├── student_performance_updated_1000.csv  # Required input (provide separately)
    └── student_performance_cleaned.csv       # Generated output
The data/ directory and input CSV are not included with the provided notebook. You need to supply the source dataset at the expected path before running it.
## Setup and usage
1. Clone or download the repository and navigate to its root.
2. Create and activate a virtual environment (recommended):
   python -m venv .venv
   Windows (PowerShell):
   .\.venv\Scripts\Activate.ps1
   macOS / Linux:
   source .venv/bin/activate
3. Install dependencies:
   python -m pip install -r requirements.txt
4. Create a data folder at the repository root and place the original CSV at:
   data/student_performance_updated_1000.csv
5. Start Jupyter:
   jupyter notebook
6. Open Student_data_cleaning.ipynb and run cells in order, starting from the repository root so the relative CSV paths resolve correctly.
The cleaned file will be saved to data/student_performance_cleaned.csv.
Data fields
The notebook works with student identifiers and names, gender, attendance, weekly study hours, extracurricular activities, parental support, online classes taken, previous grade, and final grade. Some source columns are renamed, while PreviousGrade is retained under its original capitalization.

## The final dataset also contains:
- record_id: Sequential record identifier assigned before rows with missing final grades are dropped.
- id_collision: Boolean flag for student IDs duplicated at the point of checking.
Notes and limitations
- The source dataset is required to reproduce results; the notebook alone does not contain the complete input CSV.
- online_classes_taken is cast to bool before missing-value imputation. Depending on the source values, this conversion may affect the treatment of missing values; review the source encoding before relying on this field.
- Duplicate student IDs are flagged but not resolved or removed.
- Filling missing values with modes or medians is a simple baseline strategy and may not suit every analysis.
- No model training, performance evaluation, or data visualizations are implemented in this notebook.
## License
No license has been specified for this project.

## Author

**Mohammadreza Gharahgozli**

GitHub: [@rezagharahgozli](https://github.com/rezagharahgozli)