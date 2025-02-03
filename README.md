# 📊India Salary Data Analysis (SQL)

## 📌 Solution

###  First we can search for missing values.

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

###  We can delete the missing values.

````sql
DELETE FROM salary_data
WHERE age IS NULL
   OR "Gender" IS NULL
   OR "Education Level" IS NULL
   OR "Job Title" IS NULL
   OR "Years of Experience" IS NULL
   OR "Salary" IS NULL;
````

### 3. The "Education Level" column contains inconsistencies, such as 'PhD' being written as 'phD,' which need to be corrected.

````sql
UPDATE salary_data
SET "Education Level" = CASE
    WHEN "Education Level" ILIKE 'phd' THEN 'Phd'
    WHEN "Education Level" ILIKE 'Master''s' THEN 'Master''s Degree'
    WHEN "Education Level" ILIKE 'Bachelor''s' THEN 'Bachelor''s Degree'
    ELSE "Education Level"
END;
````
<br><br>
### Now it's time to ask questions !
***
<br><br>
### 4. What is the average salary by job title ?

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

### 5. What is the salary distribution by education level ?

````sql
SELECT "Education Level", ROUND(AVG("Salary"),2) AS Avg_Salary
FROM salary_data
GROUP BY "Education Level"
ORDER BY Avg_Salary DESC;
````

**Answer:**

<img width="500" alt="image" src="">

We can conclude that a higher level of education is strongly correlated with a higher average salary. Specifically, the salary difference between individuals with a "High School" education and those holding a "PhD" is ₹128,978.14 INR.

### 6. What seems to be the salary trend based on the years of experience people have ?

````sql
SELECT "Years of Experience", ROUND(AVG("Salary"),2) AS Avg_Salary
FROM salary_data
GROUP BY "Years of Experience"
ORDER BY "Years of Experience" ASC;
````

**Answer:**

<img width="450" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20142629.png?raw=true">              <img width="450" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20142637.png?raw=true">

As the number of years of experience increases, the average salary also tends to rise. However, it appears that once individuals reach 19 years of experience, their salary remains relatively stable, continuing at a similar level until reaching 37 years of experience.

### 7. We can also find the gender distribution for each job title.

````sql
WITH gendercount AS (
    SELECT 
        "Job Title",
        "Gender",
        COUNT(*) AS count_per_gender
    FROM salary_data
    GROUP BY "Job Title", "Gender"
)
SELECT 
    "Job Title",
    "Gender",
    count_per_gender
FROM gendercount
ORDER BY count_per_gender DESC;
````

**Answer:**

<img width="570" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20145516.png?raw=true">             <img width="570" alt="image" src="https://github.com/RaulBande/Salary-Data/blob/main/Screenshot%202025-02-02%20145422.png?raw=true">

The Software Engineer role has the highest number of male employees (325), while the Data Scientist role has the highest number of female employees (202). Using the WHERE clause and the ILIKE operator (WHERE "Gender" ILIKE 'other'), we can determine that the Full Stack Engineer role as well as the Senior Software Engineer role have the highest number of individuals who do not identify as male or female (4).

