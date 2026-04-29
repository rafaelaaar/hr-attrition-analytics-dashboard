HR Attrition Analytics Dashboard
This project analyses employee attrition using HR data to identify key drivers of workforce turnover.

Overview
| Metric | Value |
|---|---|
| Total Employees | 1,470 |
| Attrition Count | 237 |
| Attrition Rate | 16% |
| Average Monthly Income | $6,500 |
The dataset represents a snapshot of the workforce and does not include a time dimension, meaning attrition cannot be analysed over time.

Key Insights
1. Department Analysis
Attrition is relatively balanced across departments: Sales accounts for 20% and Human Resources for 19%, while Research and Development shows the lowest rate at 13.8%.
2. Job Role & Experience
Sales Representatives show the highest attrition rate (42.1%), with a large proportion of employees under 30 years old (55%), suggesting higher turnover in entry-level positions. Managers and Directors (typically 40+ years old) show the lowest attrition rates.
Within the Research and Development department, Laboratory Technicians account for the highest share of attrition (23.9%), with 63.6% having one year or less tenure. Additionally, 50% of this role works overtime and 50% are under 30 years old.
3. Age Distribution
Employees under 30 exhibit the highest attrition rates (38.4%), reinforcing the pattern of higher turnover among early-career professionals.
4. Job Satisfaction
Lower levels of job satisfaction (39.2% in the very dissatisfied/dissatisfied group) are associated with higher attrition, suggesting that employee engagement plays an important role in retention.
5. Work-Life Balance
Despite moderate overall work-life balance levels (with 48.2% reporting being very dissatisfied/dissatisfied), attrition remains significant, suggesting that work-life balance may help explain employee turnover but is not the sole driver.
6. Tenure
Attrition is highest during the early tenure period (0–5 years), with a significant decline after 10 years, suggesting that employees who remain longer tend to be more stable and engaged.
7. Income
Lower salary groups show higher attrition rates (28.6%), suggesting that compensation influences employee retention.

📊 Conclusion
The data reveals an important pattern across entry-level roles (Job Level 1). While average salaries are relatively similar for entry-level positions, attrition rates vary significantly by role.

Laboratory Technicians — average salary of $2,850 with 28% attrition
Sales Representatives — lower average salary of $2,530 with the highest attrition rate at 42%

This suggests that compensation alone does not fully explain turnover. For Sales Representatives, improving entry-level salary may help reduce attrition, while for Laboratory Technicians, non-monetary factors such as working conditions and job environment are likely more important drivers of retention.

🛠️ Data Preparation & Measures
Dataset: IBM HR Analytics Employee Attrition & Performance
Source: Kaggle
Tool: Power BI

Calculated Columns (DAX)
Created directly in the Employee table to segment data:
daxAge Group = 
SWITCH(
    TRUE(),
    Employee[Age] < 30, "Under 30",
    Employee[Age] < 40, "30-39",
    Employee[Age] < 50, "40-49",
    "50+"
)
daxIncome Group = 
SWITCH(
    TRUE(),
    Employee[MonthlyIncome] < 3000, "Low",
    Employee[MonthlyIncome] < 7000, "Medium",
    "High"
)
daxTenure Group = 
SWITCH(
    TRUE(),
    Employee[YearsAtCompany] <= 1, "0-1 year",
    Employee[YearsAtCompany] <= 3, "1-3 years",
    Employee[YearsAtCompany] <= 5, "3-5 years",
    "5+ years"
)

Measures (DAX)
daxTotal Employees = 
COUNTROWS(Employee)
daxAttrition Count = 
CALCULATE(
    COUNTROWS(Employee),
    FILTER(Employee, Employee[Attrition] = "Yes")
)
daxAttrition Rate = 
DIVIDE(
    [Attrition Count],
    [Total Employees]
)

Data Modelling

Created dimension tables for Job Satisfaction and Work-Life Balance, mapping numeric scores to descriptive labels:

1 = Very Dissatisfied
2 = Dissatisfied
3 = Satisfied
4 = Very Satisfied


Established relationships between dimension tables and the Employee fact table in Model View
This approach follows proper star schema data modelling principles


📊 KPI Overview
This section presents the main HR metrics, including total employees, attrition rate, attrition count, and average income.
Show Image

🔍 Attrition Analysis Dashboard
This dashboard explores the key drivers of employee attrition, including overtime, job satisfaction, work-life balance, income groups, and tenure.
Show Image
## 📊 KPI Overview

This section presents the main HR metrics, including total employees, attrition rate, attrition count, and average income.

![KPI Overview](KPI.png)

---

## 🔍 Attrition Analysis Dashboard

This dashboard explores the key drivers of employee attrition, including overtime, job satisfaction, work-life balance, income groups, and tenure.

![Attrition Analysis](Attrition_analysis.png)
