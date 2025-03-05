
# **Nutrition Data Engineering Project**  

## **Project Overview**  
This project is designed to process, clean, and analyze nutrition data using **Azure Databricks** and **Apache Spark**. The goal is to transform raw nutritional data into structured, meaningful insights that can help in food categorization, calorie density analysis, and health scoring.  

## **Technologies Used**  
- **Azure Databricks**  
- **Apache Spark (PySpark)**  
- **Azure Data Lake Storage (ADLS)**  
- **Databricks Utilities (`dbutils`)**  
- **GitHub for version control**  

## **Project Structure**  
```
nutrition-data-engineering/
│── data/
│   ├── raw/                 # Raw nutrition data
│   ├── transformed/         # Processed and transformed data
│── notebooks/
│   ├── data_ingestion.ipynb  # Notebook for data ingestion
│   ├── data_transformation.ipynb  # Data cleaning & transformation
│   ├── data_analysis.ipynb   # Statistical and exploratory analysis
│── scripts/
│   ├── mount_adls.py        # Script to mount Azure Data Lake
│   ├── transform_data.py    # Script for data processing
│── README.md                # Project documentation
│── requirements.txt         # Python dependencies
│── .gitignore               # Ignore sensitive files
```

## **Data Pipeline**  
1. **Data Ingestion:**  
   - Mounts Azure Data Lake Storage to Databricks.  
   - Reads raw data from the storage.  
2. **Data Transformation:**  
   - Cleans column names (replaces spaces with hyphens).  
   - Computes macronutrient percentages (protein, fat, carbohydrates).  
   - Categorizes food based on nutrition composition.  
   - Adds derived metrics like calorie density and health scores.  
3. **Data Storage & Export:**  
   - Saves transformed data back to Azure Data Lake.  
   - Exports results in CSV format for further use.  

## **Setup & Installation**  

### **1. Clone the Repository**  
```bash
git clone https://github.com/Birktiayele/nutrition-data-engineering.git
cd nutrition-data-engineering
```

### **2. Mount Azure Data Lake in Databricks**  
- Update `mount_adls.py` with the correct **client ID**, **secret**, and **OAuth endpoint** (or use Databricks Secrets).  
- Run the script in a Databricks Notebook:  
```python
%run "./scripts/mount_adls"
```

### **3. Run Data Processing Script**  
- Open **Databricks** and execute `transform_data.py`:
```python
%run "./scripts/transform_data"
```

### **4. Verify Transformed Data**  
To check if the transformation worked correctly, list files in the output directory:  
```python
display(dbutils.fs.ls("/mnt/nutritiondata/transformed-data"))
```

## **Troubleshooting**  

### **1. Unable to Push to GitHub (Blocked Push)**  
If you see an error like:  
```
push declined due to repository rule violations
```
This means **GitHub detected a sensitive credential** in your commit history.  
#### **Solution:**  
1. Remove sensitive information from your code.  
2. Use the command below to **remove secrets** from the commit history:  
```bash
git reset --soft HEAD~1  # Undo last commit
git commit -m "Remove sensitive info"
git push origin main --force
```
3. If needed, use [GitHub’s unblock link](https://docs.github.com/code-security/secret-scanning/working-with-secret-scanning-and-push-protection/working-with-push-protection-from-the-command-line#resolving-a-blocked-push).  

### **2. Issues with Azure Data Lake Mounting**  
If you get an error while mounting, make sure:  
- Your credentials are correct.  
- You have the right permissions in Azure.  
- The storage account name is valid.  

To check existing mounts:  
```python
display(dbutils.fs.mounts())
```

To unmount and retry:  
```python
dbutils.fs.unmount("/mnt/nutritiondata")
```

## **Future Enhancements**  
- Automate the pipeline using **Azure Data Factory**.  
- Implement **unit tests** for data validation.  
- Deploy an **interactive dashboard** using Power BI.  

## **Contributors**  
- **Birkti Ayele**  

## **License**  
This project is licensed under the **MIT License**.  
