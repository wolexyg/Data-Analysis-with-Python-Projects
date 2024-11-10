# Data-Analysis-with-Python-Projects

## Project 1-Python Data Analysis School Project
## Table of Contents
-  [Project Overview](project-overview)
-  [Data Source](data-source)         
-  [Results](results)       

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
              
## School Summary                 
Create an overview table that summarizes key metrics about each school, including:      

-  School Name           
-  School Type      
-  Total Students      
-  Total School Budget       
-  Per Student Budget        
-  Average Math Score       
-  Average Reading Score        
-  % Passing Math       
-  % Passing Reading         
-  Overall Passing Rate (Average of the above two)       
 --Create a dataframe to hold the above results
   <img src="https://i.ibb.co/Wp4DFT6/Schools-summary.jpg" alt="Schools-summary" border="0">      
              

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
  <img src="https://i.ibb.co/g9VbNzR/District-Summary.jpg" alt="District-Summary" border="0">         

- School Name         
by_school_df = school_data_complete.set_index("school_name").groupby("school_name")  
by_school_df.count()
<img src="https://i.ibb.co/qC0yrhd/By-School-Count.jpg" alt="By-School-Count" border="0">              
-  School Type     
  ## School type         
#sch_type = school_data_complete.set_index("school_name")["type"]              
sch_type = school_data.set_index("school_name")["type"]      
#print(sch_type)           
<img src="https://i.ibb.co/XJyKds8/School-type-score.jpg" alt="School-type-score" border="0">         
## Total Students        
stu_per_sch = by_school_df["student_name"].count()       
#print(stu_per_sch)                     
## Total School budget        
#sch_budget = by_school_df["budget"].value_counts()     
sch_budget = by_school_df["budget"].mean()      
#print(sch_budget)        
## per Student budget     
per_stu_bud = sch_budget / stu_per_sch    
#print (per_stu_bud)     
## Average math and average reading score       
avg_math_sch = by_school_df["math_score"].mean()    
#print(avg_math_sch)    
avg_read_sch = by_school_df["reading_score"].mean()   
#print(avg_read_sch)             
## % Passing math and % passing reading        
#passing_math = len(school_data_complete.loc[school_data_complete["math_score"]>=70]["math_score"])/ttl_students*100     

pass_math_sch = school_data_complete.loc[school_data_complete["math_score"] >= 70].groupby("school_name") ["math_score"].count()/stu_per_sch   
pass_read_sch = school_data_complete.loc[school_data_complete["reading_score"] >= 70].groupby("school_name")  ["reading_score"].count()/stu_per_sch    

#pass_read_sch = school_data_complete[(school_data_complete["reading_score"] >= 70)]  
#pass_math_sch = by_school_df.loc[by_school_df["math_score"] >=70]    
#by_school_df.loc[[by_school_df["math_score"] >=70],['student_name'].count()/stu_per_sch]  
#print(pass_math_sch)  
#pass_read_sch = by_school_df.loc[by_school_df["reading_score"] >=70]['student_name'].count()/stu_per_sch  
#pass_math_sch = by_school_df["math_score"]    
#pass_read_sch = by_school_df["reading_score"]   

#print(pass_math_sch['math_score'].count())   
#print(type(pass_read_sch))   
#print(pass_math_sch, pass_read_sch)   
#pass_math_sch.groupby?    

## Calculate the overall passing rate (overall average score), i.e. (avg. math score + avg. reading score)/2     
overall_pass_sch = (pass_math_sch + pass_read_sch) / 2     
#overall_pass_sch = (avg_math_sch + avg_read_sch) / 2      
#print(overall_pass_sch)       
## Data frame to hold School Summary Info     
 school_summary_df = pd.DataFrame({     
     "School Type": sch_type,    
     "Total Students": stu_per_sch,    
     "Total School Budget": sch_budget,   
     "Per Student Budget": per_stu_bud,    
     "Average Math Score": avg_math_sch,    
     "Average Reading Score": avg_read_sch,    
     "% Passing Math": pass_math_sch,      
     "% Passing Reading": pass_read_sch,    
     "% Overall Passing Rate": overall_pass_sch})             

school_summary_df.style.format({"Total Students": "{:,.0f}",     
                "Total School Budget": "${:,.0f}",        
                "Per Student Budget": "${:,.0f}",        
                "Average Math Score": "{:.2f}",               
                "Average Reading Score": "{:.2f}",        
                "% Passing Math": "{:.2%}",       
                "% Passing Reading": "{:.2%}",      
                "% Overall Passing Rate": "{:.2%}"})      
 <img src="https://i.ibb.co/Wp4DFT6/Schools-summary.jpg" alt="Schools-summary" border="0">      

 ## Top 5 Schools        
 <img src="https://i.ibb.co/Fn5smhk/Top-s-CHOOLS.jpg" alt="Top-s-CHOOLS" border="0"> 
 
 ## Bottom 5 schools     
 <img src="https://i.ibb.co/s6JkGZV/Bottom-Schools.jpg" alt="Bottom-Schools" border="0">          

## Maths By Grade      
<img src="https://i.ibb.co/kgSLqrR/Maths-by-grade.jpg" alt="Maths-by-grade" border="0">          

## Reading Score By Grade    
<img src="https://i.ibb.co/kS52pc3/Reading-Score-by-Grade.jpg" alt="Reading-Score-by-Grade" border="0">      

## Spendings per Student   
<img src="https://i.ibb.co/xfMqSQj/Spendings-Per-Student.jpg" alt="Spendings-Per-Student" border="0">    

## Spendings By Student based on School size   
<img src="https://i.ibb.co/kK740C1/students-spend-based-on-school-size.jpg" alt="students-spend-based-on-school-size" border="0">      

## School Type      
<img src="https://i.ibb.co/XJyKds8/School-type-score.jpg" alt="School-type-score" border="0">     


## Results  
-  Total number of schools is 15
-  Total Students-39170
-  Total Budget is $24,649,428
-  Bailey High came first with a total number of 4976 students,a total school budget of $3,124,928
-  Cabrera High School came first as the top 5 Schools with overall passing rate of 95.59%.
-  Rodriguez High School came as the least 5 schools with an overall passing rate of 73.29%
-  Shelton High School had the highest Reading Score By grade for the 9th grade(84.12) and 11th grade(84.37),Cabrera High School had the higest for the 10th grade(84.25) and Holden High School had the highest Reading Score by grade for 12th grade(84.70)..
-  Charter School type had the highest overall percentage passing rate of 95.10%.           
  





## Project 2-Student Scores Analysis     
This project is designed to analyze student score using Python and data analysis techniques. It aims to provide insights into gender    distribution,ethnic groups,relationship between Parent education and Student scores. identify areas needing improvement, and promote     data-driven decisions in educational environments.   

## Tools
-  Python 3.9 or higher
-  Jupyter notebook

  ## Results    
 ## Gender Distribution based on Student's scores      
   
<img src="https://i.ibb.co/c1Dg0ZV/Gender-distribution-based-on-sttudent-scores.jpg" alt="Gender-distribution-based-on-student-scores" border="0">          

## Distribution of Ethnic groups based on students scores    
<img src="https://i.ibb.co/Y7Rd0fH/Dustribution-of-Ethnic-groups-based-on-student-score.jpg" alt="Dustribution-of-Ethnic-groups-based-on-student-score" border="0">  

## Number of Ethnic groups based on Student's scores    
<img src="https://i.ibb.co/JKDcFqx/Number-of-Ethnic-groups-based-on-student-score.jpg" alt="Number-of-Ethnic-groups-based-on-student-score" border="0">          




