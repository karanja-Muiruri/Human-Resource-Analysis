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

  -   


       




  
  
