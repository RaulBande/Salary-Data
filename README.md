# 📊 Salary Data Analysis (SQL)

## 📌 Solution

### 1. First we can search for missing values.

````sql
SELECT 
    SUM(CASE WHEN Age IS NULL THEN 1 ELSE 0 END) AS Missing_Age,
    SUM(CASE WHEN Gender IS NULL THEN 1 ELSE 0 END) AS Missing_Gender,
    SUM(CASE WHEN "Education Level" IS NULL THEN 1 ELSE 0 END) AS Missing_Education,
    SUM(CASE WHEN "Job Title" IS NULL THEN 1 ELSE 0 END) AS Missing_Job_Title,
    SUM(CASE WHEN "Years of Experience" IS NULL THEN 1 ELSE 0 END) AS Missing_Experience,
    SUM(CASE WHEN Salary IS NULL THEN 1 ELSE 0 END) AS Missing_Salary
FROM `idyllic-analyst-449413-g5.1.Salary_data;
`````

**Answer:**

<img width="900" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20093610.png?raw=true">

There are 9 missing values, we can drop them as they dont impact the databse, which has 6705 rows

