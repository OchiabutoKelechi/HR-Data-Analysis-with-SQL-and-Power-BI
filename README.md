# HR Data Analysis (SQL & Power BI Project)

## Project Overview

The goal of this project is to perform an in-depth analysis of a company’s HR data to gain insights into workforce composition and trends, including department distributions, demographics (gender, age, and marital status), tenure, shifts, pay rates, and annual workforce changes. These insights aim to support stakeholders in improving staff retention and aligning HR strategies with organizational goals.

## Data Source
The data for this analysis was extracted from the AdventureWorks2022 database, which I downloaded from the Microsoft website and hosted locally on my PC. This database includes data from four company departments. For this analysis, I primarily focused on HR data, obtained through SQL joins.

### Click on the link to interact with the [Analysis Dashboard](https://app.powerbi.com/groups/me/reports/cbb68014-4482-41ba-9158-7e271b345fab/ReportSectionef8754970a381b4e41a6?experience=power-bi) 

## Data Extraction
I used SQL queries to extract relevant columns from multiple tables within the Human Resources schema. Here is the SQL query that brought together data points from the Employee, Department, Shift, and Pay History tables:

```sql
SELECT 
    h.BusinessEntityID, 
    h.DepartmentID, 
    h.ShiftID, 
    d.Name As Department, 
    e.BirthDate, 
    e.MaritalStatus, 
    e.Gender, 
    e.HireDate, 
    p.Rate, 
    s.Name As Shift
FROM 
    HumanResources.EmployeeDepartmentHistory h
JOIN 
    HumanResources.Department d ON d.DepartmentID = h.DepartmentID
JOIN 
    HumanResources.Employee e ON e.BusinessEntityID = h.BusinessEntityID
JOIN 
    HumanResources.EmployeePayHistory p ON p.BusinessEntityID = h.BusinessEntityID
JOIN 
    HumanResources.Shift s ON s.ShiftID = h.ShiftID
```
The final extracted table used for the analysis contained the following columns:

- BusinessEntityID
- DepartmentID
- ShiftID
- Department
- BirthDate
- MaritalStatus
- Gender
- HireDate
- Rate
- ShiftID
- Age(calculated)
- Tenure(calculated)

## Tools and Software Used

1) SQL Server Management Studio (SSMS): Connected to and queried the database to extract the required data.
2) Power BI: Built interactive dashboards to visualize and present key insights.
3) Power Query and DAX: Used for data cleaning and calculated columns.

## Data Cleaning and Transformation
Although the database data required minimal cleaning, I performed several transformations for consistency and readability:

- Header Standardization: Ensured headers were properly formatted.
- Column Formatting: Standardized column formats for easier analysis.
- Age and Tenure Calculations: Used DAX to calculate staff age and tenure:

```DAX
Age = DATEDIFF([BirthDate], TODAY(), YEAR)
Staff Tenure = DATEDIFF([HireDate], TODAY(), YEAR)
```

## Exploratory Data Analysis (EDA)
The following business questions guided the analysis and informed the design of visualizations:

1) What is the total number of staff?
2) What departments and shifts are present?
3) What are the average age, tenure, and pay rate values?
4) How do marital status and gender distribute staff?
5) How do staff metrics (tenure, pay rate) vary across departments?
6) What is the yearly trend for staff count?

## Data Analysis

The final analysis was divided into two dashboards, with slicers enabling users to drill down into specific areas. Key insights include:

1) Analysis Period: June 2006 to May 2013
2) Total Staff: 334 employees across 16 departments
3) Average Metrics:
- Age: 45.84 years
- Tenure: 15.01 years
- Hourly Pay Rate: $18.19
4) Staff by Department:
- Production: 198 employees
- Sales: 18 employees
- Purchasing: 17 employees
- Other notable departments include Marketing (14), Finance (13), and Information Services (10). The remaining departments have fewer than nine (9) staff each.
5) Staff by Shift:
- Morning Shift: 220 employees
- Evening Shift: 62 employees
- Night Shift: 52 employees
6) Gender Distribution:
- Male: 70.96% (237 employees)
- Female: 29.04% (97 employees)
7) Marital Status: This even distribution presents a balanced marital demographic across the workforce.
- Married: 167 employees
- Single: 167 employees
8) Yearly Staff Trend: Staff numbers show a generally stable trend with minor fluctuations. The year 2009 saw the highest headcount, reaching 170 hires, marking a peak in hiring activity during the analysis period.
    
9) Average Tenure by Department:
Departments with the longest average tenure are:
- Tool Design: 16 years
- Engineering: 15.89 years
- Human Resources: 15.5 years
#### Most departments fall within an average tenure of around 15 years, except Sales, where average tenure is slightly lower at 12.44 years.
10) Average Hourly Pay Rate by Department: The highest-paying departments include:
- Executive: $68 per hour
- Research and Development: $44 per hour
- Information Services and Engineering: $34 per hour
- Sales and Finance: $30 per hour
#### Remaining departments have hourly rates below $20.

## Conclusion
This HR analysis provides a clear overview of employee demographics, department staffing, pay structure, and hiring trends. These insights are designed to assist stakeholders in making informed HR and workforce management decisions aimed at enhancing retention and aligning HR goals with business objectives.
