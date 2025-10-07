#  Data Cleaning, Analysis & Interactive Dashboard Project

##  Overview
In this assignment, I was tasked with transforming a **raw dataset** (known to contain data-quality issues) into a **clear, insightful, and interactive dashboard**.  
The process involved four key stages:

1. **Clean** — Identify and fix data errors in the 632-row dataset (e.g., missing values, duplicates, incorrect formatting, inconsistent categories).  
2. **Enrich** — Create new calculated columns to enhance the dataset (e.g., profit margins, customer segments, time-based groupings).  
3. **Analyze** — Explore the cleaned data to uncover key insights on sales performance, profitability, regional trends, and product analysis.  
4. **Present** — Build a dynamic dashboard with filters, KPIs, and visualizations for interactive exploration of results.

---

## Part A: Data Cleaning & Preparation

### Steps Taken
- Created a **staging table** in a new sheet named `Cleaned`.  
- Confirmed there were **no duplicate records**.  
- Corrected all **column data types**.  
- Replaced **missing text values** with `"Not provided"`.  
- Flagged **suspicious unit prices** in red and corrected any **negative prices**.  
- Ensured that `RequiredDate` was **not earlier than** `OrderDate`.

### Rule Applied
**Business Rule:**  
> The `RequiredDate` must always be equal to or later than the `OrderDate`.  
> If the `RequiredDate` is earlier, it should be corrected to match the `OrderDate`.

**Formula Used:**  
```excel
=IF(B2 < A2, A2, B2)
```

After applying the correction, I replaced the old `RequiredDate` column with the updated one.

---

## Part B: Analysis Tasks

### 1. Add Month Column
Created a `Month` column (formatted as `"MMM-YYYY"`) using:  
```excel
=TEXT(B2, "MMM-YYYY")
```

### 2. Identify First Sale Month
Computed the **first sale month** for each product or customer using:  
```excel
=MINIFS(B2:B633, J2:J633, J2, E2:E633, E2)
```

---

### 7. Channel Mix & Cannibalization Analysis

**Objective:**
- Compare revenue share (%) of each **Channel** (e.g., Online vs. Retail) by **Region**.  
- Identify regions where Online sales might be **cannibalizing** Retail sales.

**Pivot Table Setup:**
- **Rows:** Region  
- **Columns:** Channel  
- **Values:** Sum of Gross Revenue  

Then, to calculate **Revenue Share (%):**  
- Go to **Value Field Settings  Show Values As  % of Row Total**  

**Cannibalization Logic:**
```text
Online Cannibalization = Increase in Online Revenue - Decrease in Retail Revenue
```

- If Online is high while Retail is low Online is cannibalizing Retail.  
- If both increaseor or stable Channels are complementary.

---

### 8. Service Level Proxy

**Goal:** Measure service performance using `LeadTimeDays`.  
Find % of orders fulfilled within **7 days**, broken down by **Country** and **Product Category**.

**Steps:**
1. Create a new column `Within7Days`:  
   ```excel
   =IF(H2 <= 7, 1, 0)
   ```
   - `1` = delivered within 7 days  
   - `0` = missed target  

2. Create a **Pivot Table**:  
   - **Rows:** Country  
   - **Columns:** Product Category  
   - **Values:** Average of `Within7Days`

---

### 9. Price Compliance Analysis

**Goal:** Identify whether salespeople or regions are granting excessive discounts.

**Steps:**
1. Add a new column `DiscountAbove20`:  
   ```excel
   =IF(T2 > 20%, 1, 0)
   ```
   - `1` = discount above 20% (*non-compliant*)  
   - `0` = compliant  

2. Create a **Pivot Table**:  
   - **Rows:** Region  
   - **Columns:** Salesperson  
   - **Values:** Average of `DiscountAbove20`  

Use this to identify **outliers** with unusually high discount rates.

---

##  Part C: Scenario Modeling (What-If Analysis)

A **What-If Control Panel** was introduced to simulate various business scenarios such as:
- Adjusting discount rates  
- Modifying sales targets  
- Observing potential impact on revenue and profit  

*(This section was particularly challenging to me and I am open for further improvement.)*

---

##  Insights derived from the Sales Dashboard

### Regional Highlights
- **Americas:**  
  - *Brazil* leads with **1.037M** in total revenue — outperforming the USA (**768k**) and Canada (**882k**).  
- **Europe:**  
  - *United Kingdom* dominates with **1.111M**, ahead of Germany (**929k**) and France (**757k**).  
- **Asia:**  
  - *India* tops at **1.092M**, followed by China (**894k**) and Japan (**854k**).  
- **Africa:**  
  - *Kenya* (**935k**) and *Nigeria* (**881k**) lead in regional revenue generation.

###  Seasonal Trend
- Peak sales occur in **May, June, and July**, each generating **over 1.25M**.  
  Suggests strong **mid-year demand**, ideal for targeted marketing campaigns.

###  Product Insights
- **Networking** equipment is the top category (**1.773M**)  
- **Laptops** follow closely (**1.711M**)  
  → Indicates strong demand in **technology and remote work** sectors.

###  Sales Performance
- **Top Performer:** *B. Chen*  
  - Highest Gross Revenue (**893k**) and Gross Profit (**315k**)  
  - Achieved this with fewer orders — showing high efficiency and focus on high-value deals.

---

## Tools & Techniques Used
- **Microsoft Excel**
  - Pivot Tables & Charts  
  - Conditional Formatting  
  - IF, TEXT, MINIFS formulas  
- **Dashboard Visualization**
  - KPIs  
  - Filters & Slicers  
  - Interactive Charts

---

##  Final Deliverable
I added An **interactive sales performance dashboard** that enables:
- Dynamic regional and product analysis  
- Monitoring of discount compliance and service performance  
- Identification of channel-based trends  

---

**Author:** Felix Amenya Kenyansa 
**Dataset Size:** 632 rows  
**Deliverables:** Cleaned dataset, analysis report, and interactive Excel dashboard  
<img width="1470" height="459" alt="Screenshot 2025-10-08 000428" src="https://github.com/user-attachments/assets/807cb1a9-b6a0-4493-87bb-a980de724991" />
