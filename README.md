# Pewlett-Hackard Analysis with SQL
A project to assist with strategic planning for the anticipated "silver tsunami" (mass retirements) at Pewlett-Hackard

## Overview of the Analysis:

Pewlett-Hackard's human resources department has enlisted the help of my colleague Bobby and myself with analyzing their current staffing to start preparation and strategic planning to accomodate the "silver tsunami" (mass retirements occurring closely together), they are anticipating. The company has a large workforce with over 300,000 employees being organized primarily through several MS Excel spreadsheets. The data has become overwhelming to keep track of and they are requesting our help to utilize PostgreSQL 13 and PGAdmin4 allowing more insight to the large amounts of data that has been accumulated specifically the number of retirees by job title and also a list of employees that are eligible for a newly developed mentorship program.

## Results:

#### 1. Creating a list of retirees

Having imported all of the tables into PostgreSQL and established the proper linkages between the tables 'keying' off of the replicate data from each table, we first created a table named retirement_titles.csv. With this new file we have joined information from an Employees table and Titles table to create a list of employees born between 1952 and 1955. The issue with this first analysis is it created a dataset where some employees occured more than once due to them switching titles over the years working with Pewlett-Hackard. See illustration:

![Retirement Titles Output Example](https://github.com/sqrtofpi/Pewlett-Hackard_Analysis/blob/d30fa3d45415ac940f831db0def1fb370bfb7696/Data/retirement_titles%20output%20example.png)

#### 2. Eliminating duplicates in the list of retirees

Due to the duplicates in analysis 1, we then created a new query to retrieve the first occurrence of the employee number from the retirement_titles.csv file. This successfully removed duplicate entries for each employee. See illustration:

![Unique Titles Output Example](https://github.com/sqrtofpi/Pewlett-Hackard_Analysis/blob/d30fa3d45415ac940f831db0def1fb370bfb7696/Data/unique_titles%20output%20example.png)

#### 3. Grouping the retirees by title and sorting in descending order

 Finally, we used another query to retrieve the number of employees by their most recent job title who are about to retire. This was accomplished by retrieving the number of titles from the unique titles table, then creating a retiring titles table to hold the required information. We then grouped the table by title and sorted the count column in descending order. See illustration:

![Retiring Titles Output Example](https://github.com/sqrtofpi/Pewlett-Hackard_Analysis/blob/d30fa3d45415ac940f831db0def1fb370bfb7696/Data/retiring_titles%20output%20example.png)

#### 4. Creating a mentorship eligibility file

In light of this information, we have created another table named mentorship_eligibility.csv which holds a listing of the employees who are eligible to participate in a mentorship program ordered by the employee number. See illustration:

![Mentor Eligibility Output Example](https://github.com/sqrtofpi/Pewlett-Hackard_Analysis/blob/d30fa3d45415ac940f831db0def1fb370bfb7696/Data/mentor_eligibility%20output%20example.png)

## Summary:

Based on an analysis of the results, Pewlett-Hackard's human resources department is correct in calling this a "silver tsunami". There is the potential for 30.1% of their employees to retire in the next few years leaving a total of 90,398 roles that will need to be filled if staffing levels are to remain constant. Of those, 19.2% (57,668) are senior level employees with 67.4% of engineers being senior level and 69.8% of staff being senior level. There is not enough lower level employees to fill the senior level positions. Recognizing that nearly 20% of their senior staff could soon retire draining a significant amount of historical job specific knowledge the company is looking to see if they can retain many of them in a mentorship type role to bring new hires up-to-speed which is a prudent step in addressing the "silver tsunami" that is approaching.

We recommend in addition to the mentorship program included in this project that the following 2 additional queries be considered when approaching this topic strategically:

1. Completing an analysis of the retiree's expected by year as grouping them in a 3 year block could make the issue seem more problematic than it really is. So our first recommendation is to create a query of those employees that were born in 1952 so they can be assigned a junior employee to mentor. This can be accomplished with the following modifications to the retirement_titles.csv query:

   - changing the following line from: **WHERE (birth_date BETWEEN '1952-01-01' AND '1955-12-31')**

     ​														to: **WHERE (birth_date BETWEEN '1952-01-01' AND '1952-12-31')**

2. In addition, we would also recommend establishing a mentorship program that will last indefinitely, meaning past this wave of "silver tsunami" retirees. This can be accomplished creating a query that will group mentor eligible employees into position titles to better manage the attrition by department; so with every loss of a senior level employee, there is a junior employee that has been already engaged in a mentorship program to lessen the impact of the retiree.
