# Human-Resource-Analysis.

## Table of Contents
 - [Project Overview](#project-overview)
 - [Data Sources](#data-sources)
 - [Tools Used](#tools-used)
 - [Data Preparation](#data-preparation)
 - [Exploratory Data Analysis](#exploratory-data-analysis)

## Project Overview

I use MySQL in MySQL Workbench 8.0 CE to analyze the csv data to answer various questions.

## Data Sources

 - 'Human Resources.csv'

## Tools Used

  - MySQL in MySQL Workbench 8.0 CE.

## Data Preparation

In the initial data preparation phase, I performed the following tasks;

   - Create a database called Human_Resources and import the 'Human Resources.csv' using Table Data Import Wizard.

     - ![001](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/831dae8a-2445-440a-8101-3ecbf084864c)
    
     - ![002](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/c3f49194-c6ae-4acf-8568-6287f199ab85)
    
     - ![003](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/84596756-d310-4538-a056-0c415a5fc569)
    

- Changed column 'i>>?id to emp_id;

  - ![004](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/0a8c988a-935f-42ec-974d-d84ed72cfd07)

- Using UPDATE and CASE, together with str_to_date() function to convert the str in the 'birthdate' column to a date value and also used date_format() to change the date format from '%m/%d/%Y' to '%Y-%m-%d'. Also I modified the 'birthdate' column data type from text to DATE. 

  - ![005](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/681fe411-c204-4102-8485-5b58fa6cec77)
  - 
  - ![007](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/dec68792-a8cc-41e4-9b2f-04832e06042d)

 
-  Using UPDATE and CASE, together with str_to_date() function to convert the str in the 'hire_date' column to a date value and also used date_format() to change the date format from '%m/%d/%Y' to '%Y-%m-%d'. Also I modified the 'hire_date' column data type from text to DATE.

  -   ![008](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/9852d7c5-e6c2-4e58-90d7-146943b42bc1)


-   Using UPDATE, IF, date(), str_to_date(), I removed the time aspect of DATETIME to only DATE and I also SET where termdate IS NOT NULL and is not empty to '0000-00-00'.

  -   ![009](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/d527958d-b6f2-4806-a55d-5dff740a3c1d)


- I did ALTER the table to include 'age' column and also calculate the difference in-between 'birthdate' and CURDATE() using the timestampdiff() function. I also used the DATE_SUB() with a 100year interval to change birthdate >= 2060 < 2070 to 1960 to 1970, thus clearing the minus error in age.  

  -  ![012](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/8b610f4c-5630-4ed8-beb0-6c50fa63f7bb)
 
  -  ![013](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/9a209192-6f7a-4b1b-9c77-99284b137df9)




## Exploratory Data Analysis

   EDA involved exploring the data to answer various stakeholders' questions;

   **1. What is the gender breakdown of employees in the company?**

   - ![014](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/98c3cb46-981f-41a3-9be9-1f9ad4b484b1)
     

     **2. What is the race/ethnicity breakdown of employees in the company?**
    
        - ![015](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/7740d00a-c96d-4588-aa8a-912d0d53010e)
          
       
     **3. What is the age distribution of employees in the company?**
    
        - ![016](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/a8798dc4-9ba3-407c-a459-fd0f37d1cc79)
       
        - ![017](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/3d38d47b-ee25-4a69-84ff-9fb3d9721101)

       
     **4. How many employees work at headquarters versus remote locations?**
    
        -  ![018](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/65cba034-253a-492f-b12b-d2500fbaa426)
       
       
     **5. What is the average length of employment for employees who have been terminated?**
    
        - ![019](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/653f7bf0-3be5-47e0-9fde-b770ec1da28f)
       
       
     **6. How does gender distribution vary across departments and job titles?**
    
        - ![020](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/df0c72c6-e767-4285-9e2e-a22c1ef8a6c9)


     **7. What is the distribution of job titles across the company?**
    
        - ![021](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/221d2cbe-74d1-4018-b930-5f371ceeade0)

     
     **8. Which department has the highest turnover rate?**
    
        -  ![022](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/0633512a-e0ba-4ece-9e5d-c51e8a36c18c)
       
       
     **9. What is the distribution of employees across locations by state?**
    
        -  ![023](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/6c3e7ca5-bc94-4189-9a5b-7d439a72bec6)


     **10. How has the company's employee count changed over time based on hire and term dates?**
    
        -  ![024](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/8341325e-b1da-469d-bfa1-f09efbc54c4f)
    

     **11.  What is the tenure ditribution for each department?**
    
        -  ![025](https://github.com/karanja-Muiruri/Human-Resource-Analysis/assets/169806532/af31265b-7de6-4242-940f-6917583d781f)






       




  
  
