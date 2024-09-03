# Human-Resource-Analysis - SQL.

## Table of Contents
 - [Project Overview](#project-overview)
 - [Data Sources](#data-sources)
 - [Tools Used](#tools-used)
 - [Data Preparation](#data-preparation)
 - [Exploratory Data Analysis](#exploratory-data-analysis)

## Project Overview

I use MySQL in MySQL Workbench 8.0 CE to analyze the Human Resource.csv data to reveal key human resource insights that can significantly benefit the company, highlight critical HR metrics such as employee turnover, diversity, recruitment effectiveness, and performance evaluations. They assist HR professionals in making well-informed decisions and in strategic workforce planning.

## Data Sources

 - 'Human Resources.csv' containing 22,000 Human Resource records from year 2000 to year 2020. 

## Tools Used

  - MySQL in MySQL Workbench 8.0 CE.

## Data Preparation

In the initial data preparation phase, I performed the following tasks;

   - Create a database called Human_Resources and import the 'Human Resources.csv' using Table Data Import Wizard.


         CREATE DATABASE Human_Resource;
     
         

     - ![001](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/831dae8a-2445-440a-8101-3ecbf084864c)
    









   
    USE Human_Resource;

     



    SELECT *
    FROM hr;
         


    






- Changed column 'i>>?id to emp_id;



         ALTER TABLE hr
         CHANGE COLUMN  ï>>¿id emp_id VARCHAR(20) NULL;

  

- Using UPDATE and CASE, together with str_to_date() function to convert the str in the 'birthdate' column to a date value and also used date_format() to change the date format from '%m/%d/%Y' to '%Y-%m-%d'. Also I modified the 'birthdate' column data type from text to DATE. 


         UPDATE hr
         SET birthdate = CASE
             WHEN birthdate LIKE '%%' THEN date_format(str_to_date(birthdate, '%m/%d/%Y'), '%Y-%m-%d')
             WHEN birthdate LIKE '%-%' THEN date_format(str_to_date(birthdate, '%m-%d-%Y'), '%Y-%m-%d')
             ELSE NULL
         END;

   
             

          ALTER TABLE hr
          MODIFY COLUMN birthdate DATE;



          DESCRIBE hr;


  
         

 
-  Using UPDATE and CASE, together with str_to_date() function to convert the str in the 'hire_date' column to a date value and also used date_format() to change the date format from '%m/%d/%Y' to '%Y-%m-%d'. Also I modified the 'hire_date' column data type from text to DATE.



          UPDATE hr
          SET hire_date = CASE
             WHEN hire_date LIKE '%%' THEN date_format(str_to_date(hire_date, '%m/%d/%Y'), '%Y-%m-%d')
             WHEN hire_date LIKE '%-%' THEN date_format(str_to_date(hire_date, '%m-%d-%Y'), '%Y-%m-%d')
             ELSE NULL
          END;



          ALTER TABLE hr
          MODIFY COLUMN hire_date DATE;



          DESCRIBE hr;



-   Using UPDATE, IF, date(), str_to_date(), I removed the time aspect of DATETIME to only DATE and I also SET where termdate IS NOT NULL and is not empty to '0000-00-00'.



        UPDATE hr
        SET termdate = IF(termdate IS NOT NULL AND termdate != '', date(str_to_date(termdate, '%Y-%m-%d %H:%i:%s UTC')), '0000-00-00')
        WHERE TRUE;


        SET sql_mode = 'ALLOW_INVALID_DATES';


- I did ALTER the table to include 'age' column and also calculate the difference in-between 'birthdate' and CURDATE() using the timestampdiff() function. I also used the DATE_SUB() with a 100year interval to change birthdate >= 2060 < 2070 to 1960 to 1970, thus clearing the minus error in age.  



          ALTER TABLE hr
          ADD COLUMN age INT;




          UPDATE hr
          SET age = timestampdiff(YEAR, birthdate, CURDATE());


 
     
 
          UPDATE hr
          SET birthdate = DATE_SUB(birthdate, INTERVAL 100 YEAR)
          WHERE birthdate >= '2060-01-01' AND birthdate < '2070-01-01';


   




## Exploratory Data Analysis

   EDA involved exploring the data to answer various stakeholders' questions;

   **1. What is the gender breakdown of employees in the company?**


                SELECT gender, count(*) AS Employees
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY gender;
                
     

   **2. What is the race/ethnicity breakdown of employees in the company?**
    


                SELECT race, count(*) AS Count
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY race
                ORDER BY count(*) DESC;
          
       
   **3. What is the age distribution of employees in the company?**
    


                SELECT 
                    min(age) AS Youngest,
                    max(age) AS Oldest
                FROM hr
                WHERE termdate = '0000-00-00';




                SELECT 
                    CASE
                        WHEN age >= 21 AND age <= 34 THEN 'Millennial'
                        WHEN age >= 35 AND age <= 50 THEn 'Genx'
                        WHEN age >= 51 AND age <= 69 THEN 'Boomer'
                        ELSE 'Silent'
                    END AS age_group, gender, count(*) AS Count
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY age_group, gender
                ORDER BY age_group, gender;
       
                 

       
   **4. How many employees work at headquarters versus remote locations?**
    
        

                SELECT location, count(*) AS Count
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY location
                ORDER BY Count;

                
           
       
   **5. What is the average length of employment for employees who have been terminated?**
    



                SELECT round(avg(datediff(termdate, hire_date)) / 365, 2) AS avg_employment_period
                FROM hr
                WHERE termdate <= CURDATE() AND termdate <> '0000-00-00';


                
       
       
   **6. How does gender distribution vary across departments and job titles?**
    



                SELECT department, gender, count(*) AS count
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY department, gender
                ORDER BY department;

                


   **7. What is the distribution of job titles across the company?**
    



                SELECT jobtitle, count(*) AS Count
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY jobtitle
                ORDER BY jobtitle DESC;



                

     
   **8. Which department has the highest turnover rate?**





                SELECT department, total_count, terminated_count, terminated_count/total_count AS termination_rate
                FROM(
                     SELECT department,
                     count(*) AS total_count,
                     SUM(CASE WHEN termdate <> '0000-00-00' AND termdate <= CURDATE()
                         THEN 1 ELSE 0 END) AS terminated_count
                     FROM hr
                     GROUP BY department) AS subquery
                ORDER BY termination_rate DESC;



                
        
       
       
   **9. What is the distribution of employees across locations by state?**
    



                SELECT location_state, count(*) AS Count
                FROM hr
                WHERE termdate = '0000-00-00'
                GROUP BY location_state
                ORDER BY Count DESC;


                


   **10. How has the company's employee count changed over time based on hire and term dates?**
    



                SELECT year, hires, terminations, hires - terminations AS net_change, round((hires - terminations) / hires * 100, 2) AS net_change_precent
                FROM(
                     SELECT
                          YEAR(hire_date) AS year, count(*) AS hires,
                          SUM(CASE WHEN termdate <> '0000-00-00' AND termdate <= CURDATE()
                              THEN 1 ELSE 0 END) AS terminations
                     FROM hr
                     GROUP BY YEAR(hire_date)
                     ) AS subquery
                ORDER BY year ASC;



                
                
    

   **11.  What is the tenure ditribution for each department?**
    



                SELECT department, round(avg(datediff(termdate, hire_date) / 365), 0) AS avg_tenure
                FROM hr
                WHERE termdate <= CURDATE() AND termdate <> '0000-00-00'
                GROUP BY department;




                
        
   ### FINDINGS:

        1. There are more male employees than female or non-conforming employees
        2. The genders are fairly evenly distributed across departments. There are slightly more male employees overall.
        3. Employees 21-30 years old are the fewest in the company. Most employees are 31-50 years old. Surprisingly, the age group 50+ have the most employees in the                  company.
        4. Caucasian employees are the majority in the company, followed by mixed race, black, Asian, Hispanic, and native Americans. 
        5. The average length of employment is 7 years.
        6. Auditing has the highest turnover rate, followed by Legal, Research & Development and Training. Business Development & Marketing have the lowest turnover                    rates.
        7. Employees tend to stay with the company for 6-8 years. Tenure is quite evenly distributed across departments.
        8. About 25% of employees work remotely.
        9. Most employees are in Ohio (14,788) followed distantly by Pennsylvania (930) and Illinois (730), Indiana (572), Michigan (569), Kentucky (375) and Wisconsin                 (321).
       10. There are 182 job titles in the company, with Research Assistant II taking most of the employees (634) and Assistant Professor, Marketing Manager, Office                    Assistant IV, Associate Professor and VP of Training and Development taking the just 1 employee each.
       11. Employee hire counts have increased over the years.





       




  
  
