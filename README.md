This Power BI dashboard provides a comprehensive analysis of employee retention and attrition across departments, roles, and demographics. It is designed to help HR teams and senior leadership identify risk areas, monitor workforce trends, and make data-driven decisions to improve employee engagement and reduce churn.

Source: IBM HR Analytics Employee Attrition & Performance Dataset

Fields: Employee ID, Age, Gender, Education, Department, Job Role, Monthly Income, Job Satisfaction, Attrition, Years at Company, OverTime, Performance Rating, etc.

Insights & Use Cases:

HR Managers can use this dashboard to pinpoint departments with high attrition.

Enables proactive retention strategies by identifying at-risk employee segments.

Helps justify HR budget allocation for employee engagement or training initiatives.

Key DAX Measures Used:
1. Attrition Rate: Attrition Rate (%) = 
DIVIDE(
    CALCULATE(COUNTROWS(EmployeeData), EmployeeData[Attrition] = "Yes"),
    COUNTROWS(EmployeeData),
    0
) * 100

2. Avg Monthly Income (Active) = 
CALCULATE(
    AVERAGE(EmployeeData[MonthlyIncome]),
    EmployeeData[Attrition] = "No"
)

3. Avg Tenure = AVERAGE(EmployeeData[YearsAtCompany])

4. Retention Score = 
SWITCH(
    TRUE(),
    EmployeeData[OverTime] = "Yes" && EmployeeData[JobSatisfaction] < 2, 1,
    EmployeeData[JobSatisfaction] >= 4 && EmployeeData[MonthlyIncome] >= 5000, 5,
    EmployeeData[JobSatisfaction] >= 3, 4,
    3
)

