# 🏦 Bank Personal Loan Performance Dashboard

## 📘 Project Overview
This project analyzes **bank personal loan data** to evaluate loan approvals, defaults, and customer credit behavior.
The dashboard is built using **SQL** for data cleaning & modeling, and **Tableau Public** for visualization.
It provides key performance metrics to understand approval efficiency, borrower demographics, and branch performance.

---

## 🧮 Tools Used
- **SQL Server / MySQL** – Data cleaning, modeling, KPI generation
- **Excel / CSV** – Data export for Tableau
- **Tableau Public** – Dashboard creation and publishing

---

## 🧹 Data Cleaning & Modeling (SQL Steps)
```sql
-- Remove nulls and duplicates
DELETE FROM bank_loan WHERE Application_ID IS NULL;
WITH cte AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY Application_ID ORDER BY Application_Date) rn
  FROM bank_loan
)
DELETE FROM cte WHERE rn > 1;

-- Standardize fields
UPDATE bank_loan
SET Loan_Status = UPPER(TRIM(Loan_Status));

-- Add Approval Flag
ALTER TABLE bank_loan ADD Approval_Flag BIT;
UPDATE bank_loan
SET Approval_Flag = CASE WHEN Loan_Status = 'APPROVED' THEN 1 ELSE 0 END;
```

---

## 📊 KPIs Tracked
| KPI | Description |
|-----|--------------|
| **Total Applications** | Total number of loan applications |
| **Approval Rate (%)** | % of loans approved |
| **Default Rate (%)** | % of loans defaulted |
| **Avg Loan Amount (Approved)** | Average size of approved loans |
| **Avg Credit Score (Approved)** | Average credit score of approved borrowers |

---

## 📈 Visuals in Tableau
| Visualization | Purpose |
|----------------|----------|
| **Loan Status Distribution (Bar Chart)** | Shows approved, rejected, and defaulted loans |
| **Branch-wise Approval (Pie / Bar)** | Compares approval efficiency by branch |
| **Loan Status by Gender** | Shows approval trends across genders |
| **Quarterly Application Trends (Line Chart)** | Displays seasonal patterns in loan applications |
| **Loan Amount by Age Group (Treemap)** | Highlights which age groups borrow the most |

---

## 🎛️ Filters (Applied to Entire Dashboard)
- Loan Status
- Application Date (Quarter / Month)
- Branch
- Gender
- Credit Score Range

---

## 💡 Key Insights
- Total **10,000 applications**, with an **approval rate of ~60%**.
- **Default rate ~4.7%**, within acceptable limits.
- **Average approved loan = $531K**, mostly from mid-income borrowers.
- **30–45 age group** takes the largest share of total loan amounts.
- **Branches C & D** show higher approval efficiency (~61%).
- Female borrowers tend to take **slightly higher loan amounts** on average.

---

## 🚀 How to Use
1. Run SQL cleaning queries on your raw dataset.
2. Export the cleaned table as `bank_loan.xlsx` or `.csv`.
3. In **Tableau Public**, connect → Microsoft Excel → `bank_loan.xlsx`.
4. Create KPIs and visual sheets.
5. Combine visuals into a dashboard and apply filters globally.
6. Save → Publish to Tableau Public as
   👉 *“Bank Personal Loan Performance Dashboard”*

---

## 📂 File Structure
```
📁 Bank_Personal_Loan_Dashboard/
│
├── bank_loan.xlsx               # Cleaned dataset
├── SQL_queries.docx             # Data cleaning & modeling queries
├── Bank_Personal_Loan_Dashboard.twbx  # Tableau workbook (optional)
├── README.md                    # This file
└── dashboard_screenshot.jpg     # Dashboard image preview
```

---

## 🧠 Summary
The **Bank Personal Loan Performance Dashboard** provides actionable insights into lending trends and credit health.
It demonstrates proficiency in **SQL, data cleaning, KPI design, and Tableau dashboarding** — an ideal portfolio project for a Data Analyst or BI professional.
