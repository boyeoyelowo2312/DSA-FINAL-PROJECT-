# DSA-FINAL-PROJECT
## Palmoria Group emp-data Analysis
Methods used
### 1. Power BI Desktop was open ,I  Click "Get Data" and select CSV Navigate to file location and  selected  the  Palmoria Group emp-data.csv file. In the preview window, click "Transform Data" to open  Power Query Editor.
Data Cleaning was Performed in Power Query Editor:  
 Remove Rows with Null Salaries: Select the "Salary" column. Click the filter icon on the
 column header. Uncheck "null"  and click "OK". Remove
 Rows with Null Departments: Select the "Department" column. Click the filter icon on the
 column header. Uncheck "NULL" and click "OK". Assign Generic Gender Status: Select the
 "Gender" column. Click "Replace Values" from the "Transform" tab. In "Value To Find",
 leave it blank (or type "null" if it appears as such). In "Replace With", type "Undisclosed" (or
 "Other" as a generic gender status). Click "OK". Change Data Types.
  "Salary" is set  to "Decimal Number" or "Whole Number".
  "Rating" is set to "Text". 
 "Gender", "Department", and "Location" are "Text".
  "Close & Apply" load the cleaned data into  Power BI Desktop.

 2. Gender Distribution Analysis
  Visualization: Donut Chart or Pie Chart. Fields: Drag "Gender" to "Legend" and "Name" (or
 any unique identifier) to "Values" (and set aggregation to "Count"). 
 Chart show the overall proportion of Male, Female, and Undisclosed genders in the company.
 
Gender Distribution by Regions:
 Visualization: Clustered Column Chart or Stacked Column Chart. 
Use  "Location"  for  "Axis", "Gender" to "Legend", and "Name" to "Values" (Count). 
 Display the  gender breakdown for each region (Lagos, Abuja, Kaduna).

 Gender Distribution by Departments:
 Visualization: Stacked Bar Chart or 100% Stacked Bar Chart. 
 "Department" for  "Axis", "Gender" to "Legend", and "Name" to "Values" (Count). 
This show the  gender composition within each department.

Ratings Based on Gender
 Visualization: Clustered Column Chart or Stacked Column Chart.
  "Rating" for "Axis", "Gender" to "Legend", and "Name" to "Values" (Count).
  Chart illustrate how different genders are distributed across performance
 ratings (Very Good, Good, Average, Poor, Very Poor, Not Rated). 

  Gender Pay Gap Analysis
 Calculate Average Salary by Gender:
 Visualization: Clustered Column Chart. Fields: Drag "Gender" to "Axis" and "Salary" to
 "Values" (set aggregation to "Average"). Insight: This will immediately show if there's a
 noticeable difference in average salaries between genders.

 Identify Gender Pay Gap by Department and Region:
 Create a Matrix Visual: Rows: "Department" Columns: "Location" Values: "Salary" (set
 aggregation to "Average") and "Gender" (drag "Gender" to "Columns" as well to split the
 average salary by gender within each department and region). Conditional Formatting:
 Apply conditional formatting to the average salary values to highlight significant differences.
 This detailed matrix pinpoint specific departments and regions where a gender
 pay gap exists, allowing management to focus their efforts.

  Minimum Salary Requirement Analysis
  Create a New Measure (DAX):
 DAX
 Employees Below Minimum = 
CALCULATE(
 COUNTROWS(' Palmoria Group emp-data '),
             ' Palmoria Group emp-data ‘[Salary] < 90000
        )
 Visualization: Card visual for "Employees Below Minimum". Insight: This card will show the
 total number of employees earning less than $90,000. You can also create another
 measure for the total number of employees to show the proportion.

 Pay Distribution by Salary Band:
 Create a New Calculated Column (DAX) for Salary Bands:
 DAX
        Salary Band = 
        VAR SalaryValue = ' Palmoria Group emp-data '[Salary]
        RETURN
            SWITCH(
                TRUE(),
                SalaryValue >= 10000 && SalaryValue < 20000, "$10,000 - $19,999",
                SalaryValue >= 20000 && SalaryValue < 30000, "$20,000 - $29,999",
                SalaryValue >= 30000 && SalaryValue < 40000, "$30,000 - $39,999",
                SalaryValue >= 40000 && SalaryValue < 50000, "$40,000 - $49,999",
                SalaryValue >= 50000 && SalaryValue < 60000, "$50,000 - $59,999",
                SalaryValue >= 60000 && SalaryValue < 70000, "$60,000 - $69,999",
                SalaryValue >= 70000 && SalaryValue < 80000, "$70,000 - $79,999",
                SalaryValue >= 80000 && SalaryValue < 90000, "$80,000 - $89,999",
                SalaryValue >= 90000 && SalaryValue < 100000, "$90,000 - $99,999",
                SalaryValue >= 100000 && SalaryValue < 110000, "$100,000 - $109,999",
                SalaryValue >= 110000 && SalaryValue < 120000, "$110,000 - $119,999",
                "$120,000+"
            )
 Visualization: Clustered Column Chart or Bar Chart. Fields: Drag "Salary Band" to "Axis"
 and "Name" to "Values" (Count). Insight: This chart will show the number of employees in
 each salary band.

 Pay Distribution by Salary Band and Region:
 Visualization: Stacked Column Chart. Fields: Drag "Salary Band" to "Axis", "Location" to
 "Legend", and "Name" to "Values" (Count). Insight: This will show the salary distribution
 across regions, highlighting which regions have more employees below the $90,000
 threshold.

 6. Bonus Allocation (Requires additional data and rules)
 Data Preparation for Bonus:
 You would need to load the "another data set that contains rules for making bonus
 payments" into Power BI. Let's assume this data set is named BonusRules.csv and contains
 columns like Rating and BonusPercentage or BonusAmount. Merge Queries: In Power Query Generated 

 Editor, merge your emp-data table with the BonusRules table based on the "Rating" column.
 This  bring the bonus rules into your main employee data.
 Calculate Bonus for Individual Employees (New Calculated Column - DAX):
 Assuming BonusPercentage is a column from the merged BonusRules table:
 DAX
 Bonus Amount = 'Table'[Salary]  ' Palmoria Group emp-data '[BonusPercentage]
 If the bonus rule is a fixed amount per rating:
 DAX
 Bonus Amount = ' Palmoria Group emp-data '[BonusAmount]

 Calculate Total Amount to be Paid to Individual Employees (New Calculated Column 

DAX):
 DAX
 Total Pay (Salary + Bonus) = ' Palmoria Group emp-data '[Salary] + ' Palmoria Group emp-data '[Bonus Amount]
 Total Amount to be Paid Out Per Region (New Measure - DAX):
 DAX
 Total Pay by Region = 
SUM('Table'[Total Pay (Salary + Bonus)])
 Visualization: Table visual or Clustered Column Chart. Fields: Drag "Location" to
 "Rows/Axis" and "Total Pay by Region" to "Values".
 Total Amount to be Paid Out Company-Wide (New Measure - DAX):
 DAX
 Total Company Pay = 
SUM('Table'[Total Pay (Salary + Bonus)])
 Visualization: Card visual.
 General Power BI Tips for this Case Study:
 Interactive Dashboards: Create multiple pages in your Power BI report, each focusing on
 a specific aspect (e.g., "Gender Distribution", "Pay Gap Analysis", "Compliance &
 Bonus").
 Slicers: Add slicers for "Location" and "Department" to allow users to dynamically filter
 the data and gain more granular insights.
Clear Titles and Labels: Ensure all charts and tables have clear, descriptive titles and
 axis labels.
I Use text boxes to add explanations and key takeaways from the  analysis on
 the report pages.
 





