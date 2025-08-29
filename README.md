# SQL Project – Data Cleaning

This project focuses on **data cleaning using SQL**. The objective is to demonstrate practical **SQL data cleaning techniques** such as removing duplicates, standardizing values, handling nulls, and preparing the dataset for exploratory data analysis (EDA).
---

## Steps in Data Cleaning  

### 1. Create a Staging Table  
- Kept the **original dataset intact**.  
- Created a `layoffs_staging` table to work on the cleaning process.  
- Copied all raw data into the staging table for further transformations.  

---

### 2. Remove Duplicates  
- Checked for duplicates using `ROW_NUMBER()` with `PARTITION BY`.  
- Created a `layoffs_staging2` table with an extra `row_num` column to identify duplicate rows.  
- Deleted all rows where `row_num >= 2`.  
- Dropped the `row_num` column after cleanup.  

---

### 3. Standardize Data  
- **Industry Column**:  
  - Converted blank strings (`''`) into `NULL`.  
  - Populated missing industries by matching company names with existing rows.  
  - Standardized variations (e.g., `"Crypto Currency"`, `"CryptoCurrency"`) → `"Crypto"`.  

- **Country Column**:  
  - Removed trailing periods (e.g., `"United States."` → `"United States"`).  

- **Date Column**:  
  - Converted text-based dates into proper SQL `DATE` format using `STR_TO_DATE`.  
  - Updated the column type to `DATE`.  

---

### 4. Handle Null Values  
- Decided **not to impute nulls** in `total_laid_off`, `percentage_laid_off`, and `funds_raised_millions`.  
- Keeping them as `NULL` allows better handling during EDA and avoids introducing bias.  

---

### 5. Remove Useless Data  
- Removed rows where both `total_laid_off` and `percentage_laid_off` are `NULL` (since they provide no useful information).  
- Dropped the helper `row_num` column after deduplication.  

---

## Final Clean Dataset  
The cleaned dataset is stored in:  
```
world_layoffs.layoffs_staging2
```

This version of the dataset is:  
- Free of duplicates  
- Standardized across industries, countries, and dates  
- Stripped of useless rows  
- Ready for **Exploratory Data Analysis (EDA)**  
