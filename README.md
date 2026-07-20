# Bank Loan Analysis Dashboard 📊🏦

## Project Overview
This project delivers a comprehensive, data-driven Bank Loan Performance & Credit Risk Dashboard. By leveraging robust data analytics techniques, the repository bridges the gap between raw transactional logs and operational financial insights. The objective is to empower financial institutions with the clarity needed to track loan health, evaluate regional default rates, monitor repayment performance, and make strategic data-backed lending decisions.

The project is structured into three main focal areas:
1. **Summary Page:** Tracking vital financial KPIs, month-on-month (MoM) growth metrics, and high-level portfolio segregation (Good vs. Bad Loans).
2. **Overview Page:** Uncovering multi-dimensional demographic and regional patterns behind borrower profiles.
3. **Details Page:** Offering a granular, transactional breakdown of all active loan portfolios.

---

## 🛠️ Technical Stack & Architecture
* **Database Management:** SQL Server / T-SQL (For core KPI calculation, data validation, and aggregation logic)
* **Business Intelligence / Data Visualization:** Power BI / Microsoft Excel (For interactive UI/UX design, visual charts, and dynamic filtering)
* **Domain Focus:** Credit Risk Management, Financial Analytics, Portfolio Health Evaluation

---

## 📈 Core Metrics & Dashboard Insights

### 1. High-Level Portfolio Performance
* **Total Applications:** Managed **38.6K** loan records over the observed period, featuring a steady **6.9% MoM growth** heading into December.
* **Capital Disbursed:** A total of **$436M** was successfully funded across all categories.
* **Repayment Collection:** The bank successfully collected **$473M**, showcasing highly effective general portfolio health and liquidity management.
* **Portfolios at Glance:** Held a steady **12.05% Average Interest Rate** alongside a safe **13.3% Average Debt-to-Income (DTI)** ratio.

### 2. Credit Quality Classification (Good vs. Bad Loans)
To properly analyze credit risk patterns, loans are strictly divided by their performance statuses:
* **Good Loans (Fully Paid & Current):** Comprises **86.2%** of the entire application pool (~33.2K applications). This healthy portfolio alone captured **$370.2M in funding** and generated **$435.8M in collected returns**.
* **Bad Loans (Charged Off):** Accounted for **13.8%** of total applications (~5.3K applications). This segment generated a loss vector representing **$65.5M in funded capital** against a diminished **$37.3M collection**.

### 3. Multi-Dimensional Deep Dives
* **Temporal Trend Analysis:** Consistent upward application acceleration month-over-month, starting from a base of **2.3K in January** and scaling up to an active **4.3K in December**.
* **Borrower Purpose Segregation:** **Debt Consolidation** emerged as the single largest driving indicator for borrowing volume, vastly eclipsing categories like credit cards and home improvements.
* **Structural Distribution:** The data highlights that the absolute majority of consumers opt for stable **36-month terms (73.2%)** over long-term 60-month windows.

---

## 💾 Core SQL Query Implementation Examples
Below are specialized query snippets used to evaluate, map, and cleanly pull metrics directly from our core transactional data:

### Total KPI Portfolio Breakdown
```sql
SELECT 
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Amount_Received,
    AVG(int_rate) * 100 AS Avg_Interest_Rate,
    AVG(dti) * 100 AS Avg_DTI
FROM bank_loan_data;
'''

### Risk Profiling Metrics (Good vs. Bad Loan Segregation)

'''sql
SELECT
    (COUNT(CASE WHEN loan_status IN ('Fully Paid', 'Current') THEN id END) * 100.0) / COUNT(id) AS Good_Loan_Percentage,
    (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) / COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data;
'''

Dynamic Categorical Aggregation (Lending Status View)

'''sql
SELECT
    loan_status,
    COUNT(id) AS LoanCount,
    SUM(total_payment) AS Total_Amount_Received,
    SUM(loan_amount) AS Total_Funded_Amount,
    AVG(int_rate * 100) AS Interest_Rate,
    AVG(dti * 100) AS DTI
FROM bank_loan_data
GROUP BY loan_status;
'''

💡 Key Business Takeaways
Risk Mitigation: Identifying the exact tipping points of the 13.8% default rate enables underwriters to modify credit score minimums for high-risk categories.

Product Optimization: Recognizing that Debt Consolidation represents the primary customer pipeline allows targeted financial marketing and specialized lending packages.

Liquidity Guardrails: Monitoring dynamic MTD and MoM changes enables financial desks to prepare operational cash reserves efficiently to buffer high December spikes.




Screenshots

   ![Dashboard Preview](https://github.com/gopikantachary1-hub/Bank-Loan-Performance-and-Risk-Analysis-Dashboard/blob/main/Summary.png)

![Dashboard Preview](https://github.com/gopikantachary1-hub/Bank-Loan-Performance-and-Risk-Analysis-Dashboard/blob/main/Overview.png)

![Dashboard Preview](https://github.com/gopikantachary1-hub/Bank-Loan-Performance-and-Risk-Analysis-Dashboard/blob/main/Details.png)


