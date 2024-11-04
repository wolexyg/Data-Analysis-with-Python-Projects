# Data-Analysis-with-Python-Projects

## Project 1-Python Data Analysis School Project
## Table of Contents
.[Project Overview](project-overview)           
.[Data Source](data-source)         
.[Results](results)       

## Project-Overview
You have become the Chief Data Scientist for your city's school district. In this capacity, you'll be helping the school board and mayor make strategic decisions regarding future school budgets and priorities.              
As a first task, you've been asked to analyze the district-wide standardized test results. You'll be given access to every student's math and reading scores, as well as various information on the schools they attend. Your responsibility is to aggregate the data to and showcase obvious trends in school performance.               
Your final report should include each of the following:           
## District Summary            
Create a high level snapshot (in table form) of the district's key metrics, including:         
-	Calculate the total number of schools      
-	Calculate the total number of students        
-	Calculate the total budget        
-	Calculate the average math score         
-	Calculate the average reading score         
-	Calculate the overall passing rate (overall average score), i.e. (avg. math score + avg. reading score)/2          
-	Calculate the percentage of students with a passing math score (70 or greater)               
-	Calculate the percentage of students with a passing reading score (70 or greater)            
-	Create a dataframe to hold the above results               
-	Optional: give the displayed data cleaner formatting

## Data Sources 
The primary datasets used for thies project was dwonloaded from https://www.kaggle.com/code/jamiedataviz/module4     

## Data Analysis   
Calculate the total number of schools               
ttl_schools = school_data["school_name"].count()      

Calculate the total number of students                   
ttl_students = student_data["student_name"].count()          

Calculate the total budget           
budget = school_data["budget"].sum()                    

Calculate the average math score         
avg_math = school_data_complete["math_score"].mean()                 

Calculate the average reading score         
avg_reading = school_data_complete["reading_score"].mean()                 

Calculate the overall passing rate (overall average score), i.e. (avg. math score + avg. reading score)/2              
overall_pass = (avg_math + avg_reading)/2                   

Calculate the percentage of students with a passing math score (70 or greater)                
passing_math = len(school_data_complete.loc[school_data_complete["math_score"]>=70]["math_score"])/ttl_students*100           

Calculate the percentage of students with a passing reading score (70 or greater)          
passing_reading = len(school_data_complete.loc[school_data_complete["reading_score"]>=70]["reading_score"])/ttl_students*100             

Create a dataframe to hold the above results                 
d = {'Total Schools': [ttl_schools],          
     'Total Students': [ttl_students],            
     'Total Budget': [budget],                      
     'Average Math Score': [avg_math],                  
     'Average Reading Score': [avg_reading],            
     '% Passing Math': [passing_math],         
     '% Passing Reading': [passing_reading],              
     '% Overall Passing Rate': [overall_pass]}            
district_summary_df = pd.DataFrame(data=d)               
district_summary_df  

## Results


