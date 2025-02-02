# 📊India Salary Data Analysis (SQL)

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

### 2. We can delete the missing values.

````sql
DELETE FROM salary_data
WHERE age IS NULL
   OR "Gender" IS NULL
   OR "Education Level" IS NULL
   OR "Job Title" IS NULL
   OR "Years of Experience" IS NULL
   OR "Salary" IS NULL;
````

### 3. What is the average salary by job title ?

````sql
SELECT "Job Title", ROUND(AVG("Salary"),2) AS Avg_Salary
FROM salary_data
GROUP BY "Job Title"
ORDER BY Avg_Salary DESC
limit 10;
````

**Answer:**

<img width="500" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20140343.png?raw=true">

It is evident that the job titles of "Chief Executive Officer (C.E.O.)" and "Chief Technology Officer (C.T.O.)" typically command the highest average salaries among various executive positions (₹250000.00 INR).

### 4. What is the salary distribution by education level ?

````sql
SELECT "Education Level", ROUND(AVG("Salary"),2) AS Avg_Salary
FROM salary_data
GROUP BY "Education Level"
ORDER BY Avg_Salary DESC;
````

**Answer:**

<img width="500" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20140827.png?raw=true">

We can conclude that a higher level of education is strongly correlated with a higher average salary. Specifically, the salary difference between individuals with a "High School" education and those holding a "PhD" is ₹128,978.14 INR.

### 5. 

````sql

````

**Answer:**

<img width="500" alt="image" src=" ">              <img width="500" alt="image" src=" ">


