# School_District_Analysis
Using JupyterNotebook to generate a comprehensive report of the school district. 

## Overview 
Client requires help with analyzing key metrics of a school district's data. The data will be presented during the district's board meeting to help allocate future funding for each school within the district. The data presented focuses on quantifying the performance of each school within the district, by visualizing the relationship between student test scores and the schools' three key metrics: the size of its student poulation, its budget per student and its type. To accomplish this, the client had asked to deliver data tables containing the following analyses:  
- A high-level snapshot of the district's key metrics. 
- An overview of the key metrics of each school. 
- The top 5 and bottom 5 performing schools, based on the overall passing rate.
- The average math score of each student in each grade level at each school. 
- The average reading score each student in each grade level at each school. 
- School performance based on the budget per student. 
- School performance base on the school size.
- School performance based on the type of school. 

### Challenge Analysis
The data will be cleaned to account for academic dishonesty of the 9th grade class in Thomas High School. Then the same analysis will be performed using the updated data set. Finally, a comparative analysis on the impact of dropping the math and reading scores of the 9th grade class of Thomas High School will be assessed, using the same criteria mentioned above. It is important to note that only the test scores of the 9th grade class are dropped, the population of the 9th grade class itself will be used calculations not involving test scores such as determining the budget per school based on total student population.

## Software
- Anaconda - 4.11.0
- Jupyter Notebook - 6.4.8
- Python - 3.7.11

### Highlight of Key Dependencies in Python 
- Pandas - 1.4.1 
- NumPy - 1.22.0

## Results 
- In the **District Summary** tables, the total amounts of schools, student size and budget did not change. Globally, there were negligable decreases in the score metrics. There was a 0.1 point decrease in the average math score for the entire district but the average reading score remained unchanged. The percent passing scores for math decreased by 0.2% and by 0.1% for reading. Overall passing percentage decreased by 0.3%. 

  - **Original District Summary**
  ![Original District Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_district_summary_df.png) 
  
  - **Updated District Summary**
  ![Updated District Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_district_summary_df.png)

- In the **School Summary** tables, the differences were negligable as well. The order of the top 5 schools and the bottom 5 schools remained the same. Thomas High School still maintained its position as second in the school rankings with minor decreases across almost all score metrics. The updated school ranking summary showed a decrease in the average math score by 0.7 points but an increase in the average reading score by 0.5 points. The percentage of students passing math decreased by 0.8% and by 0.3% for students passing reading. Overall passing percentage showed a 0.3% decrease. It is worth mentioning that the bottom 5 schools all had high *Total Student* populations relative to the top 5 schools. This can be attributed to the capped admissions associated with charter schools. Additionally, the charters schools all ranked higher than district schools. 

  - **Original School Summary Arranged in Descending Order Based on Overall Passing Percentage**
  ![Original School Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_topschools_summary_df.png) 
  
  - **Updated School Summary Arranged in Descending Order Based on Overall Passing Percentage**
  ![Updated School Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_topschools_summary_df.png)
  
- There were virtually no differences in Thomas High School's performance between the **Original School Summary** and the **Updated School Summary**, suggesting that the impact of dropping the 9th grade class was negligable. A possible way to visualize a siginificant imapct of this action is to assess the data produced with the original code that does not account for the *nan* in the 9th grade class's scores. The **Updated School Summary** table was produced by editing the Thomas High School's values in the **Raw Updated School Summary** table using a *Boolean Mask*; this discounted the 9th grade population from the total student population of Thomas Highschool in calculations involving the students' scores: 
  ```
  # Boolean Mask for THS students without Cheaters 
  
  ths_grades = school_data_complete_df["grade"] != '9th'
  ths_name = school_data_complete_df["school_name"] == 'Thomas High School'
  ths = ths_name & ths_grades
  ```
  - **Raw Updated School Summary Arranged in Descending Order Based on Overall Passing Percentage** 
  ![Raw Updated School Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/R_topschools_summary_df.png)
  
  From the **Raw Updated School Summary** table to the **Updated School Summary** table, the Thomas High School's position shifted from the 8th to the 2nd position since the percent passing values across all metrics went up significantly, averaging at approximately 20%. By discounting the 9th grade class population, the scores of the remaining grades (10th to 12th) in Thomas High School were accurately presented. There was no difference between the average math and reading scores of the two tables. This is attributed to the default parameters of the `.mean( )` function, employed in both the original and the updated calculations, which excludes NA/null values as it computes the output (Source:[pandas.pydata.org](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.mean.html)).   

- The negligable impact of dropping the math and reading scores of the 9th grade Thomas High School class can be justified by the average scores of the 9th grade class being extremely similar to the average scores of the remaining classes (10th- 12th). The original tables *(shown on left)* below, include the scores of the 9th grade class and were replaced with *nan* in the updated tables *(shown on right)*. 

  - **Original & Updated Math Scores by Grade**
  
  ![Original Math Scores](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_math_grades_df.png) ![Updated Math Scores](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_math_grades_df.png)
  - **Original & Updated Reading Scores by Grade**
  
  ![Original Reading Scores](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_read_grades_df.png) ![Updated Reading Scores](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_read_grades_df.png)

- When scores were categorized into spending bins based on the *Per Student Budget* column in the **Original School Summary** table, Thomas High School belonged to the *$630-644* bin. Similarly, replacing the scores did not have a significant impact on the overall score metrics associated with said bin. The differences ccould only be observed when the data was displayed down to the hundredth decimal place. The average math and the reading score, as well as the percent passing math scores, were virtually the same value. The percent passing for reading and the overall percent passing values decreased by 0.1%. 

  - **Original Scores Based on Spending Ranges Summary**
  ![Original Spending Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_spend_df.png) 
  
  - **Updated Scores Based on Spending Ranges Summary**
  ![Updated Spending Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_spend_df.png)

- When scores were categorized into school size bins based on the *Total Student* column in the **Original School Summary** table, Thomas High School belonged to the *Medium (1,000 - 2,000)* bin. Similarly, replacing the scores did not have a significant impact on the overall test score metrics associated with said bin. Similarly, the differences could only be observed when the data was displayed down to the hundredth decimal place, since all score metrics were virtually the same value. The most notable value was the percent passing reading, which decreased by 0.1%. 

  - **Original Scores Based on School Size Summary**
  ![Original Size Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_size_df.png) 
  
  - **Updated Scores Based on School Size Summary**
  ![Updated Size Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_size_df.png)

- When scores were categorized into school size bins based on the *School Type* column in the **Original School Summary** table, Thomas High School belonged to the *Charter* bin. Similarly, replacing the scores did not have a significant impact on the overall test score metrics associated with said bin. The differences were similar to the previously presented tables. 

  - **Original Scores Based on School Type Summary**
  ![Original Type Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/OG_type_df.png) 
  
  - **Updated Scores Based on School Type Summary**
  ![Updated Type Summary](https://github.com/Fabalin/School_District_Analysis/blob/main/Output_Images/UD_type_df.png)

## Summary 
Replacing the reading and math scores of the 9th grade class in Thomas High School had negligable impacts upon the final outputs across all analyses, this can be attributed to the extremely similar average values of the 9th grade scores compared to the remaining grades' average scores, within the same school. Thomas High School still maintained its position as the second highest performing charter school based on its overall passing percentage. The updated school district analysis incorporated the `loc[ ]` function along with *Boolean Masks* constructed using conditional statements to first change the 9th grade test scores to *nan*, then to discount the population when calculating the percentages of passing students. The average math and reading score values remain unchanged because the `mean( )` function automatically disregards the replaced *nan* values in its computation. 
