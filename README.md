# E-Commerce SQL Data Analysis

**DecodeLabs Industrial Training Kit — Project 3 (SQL Data Analysis)**
*By Kingsley Ezenwanne | Batch 2026*

## Overview

This project is the extraction phase of the DecodeLabs Data Analytics Internship. Using SQL in Microsoft SQL Server Management Studio (SSMS), structured queries were written to answer 10 real-world stakeholder business questions drawn from the same 1,200-row e-commerce dataset cleaned in Project 1 and analysed in Project 2. The goal was to demonstrate the ability to bridge the gap between a raw database and actionable business intelligence through precise relational logic.

## Objectives

- Write SELECT queries to retrieve and inspect data
- Use WHERE to filter rows by business-relevant conditions
- Use GROUP BY with aggregate functions to summarise data by category
- Use ORDER BY to rank and present results meaningfully
- Use HAVING to filter aggregated groups
- Demonstrate CTE (WITH clause) as an alternative to HAVING for production-grade readability

## Tools Used

- **Microsoft SQL Server Management Studio (SSMS)**
- **MySQL Workbench** 

## Dataset

| Property | Detail |
|---|---|
| Source | Cleaned output from Project 1, imported into SSMS |
| Table | `DecodeLabs` |
| Records | 1,200 orders |
| Columns | 14 |

## SQL Clauses & Functions Demonstrated

`SELECT` · `FROM` · `WHERE` · `GROUP BY` · `ORDER BY` · `HAVING` · `COUNT()` · `SUM()` · `AVG()` · `ROUND()` · `TOP` · `CTE (WITH)`

## Stakeholder Questions Answered

| # | Business Question | Key Clauses Used |
|---|---|---|
| Q1 | What do the first 10 orders look like? | SELECT, TOP |
| Q2 | Which orders had TotalPrice above $3,000? | WHERE, ORDER BY |
| Q3 | How many orders used the SAVE10 coupon? | WHERE, COUNT, GROUP BY |
| Q4 | Total revenue and order count per product, ranked? | SUM, COUNT, GROUP BY, ORDER BY |
| Q5 | Average order value per payment method, ranked? | AVG, GROUP BY, ORDER BY |
| Q6 | Order count and revenue per order status? | COUNT, SUM, GROUP BY, ORDER BY |
| Q7 | Which referral source drives the highest AOV? | AVG, GROUP BY, ORDER BY |
| Q8 | Revenue per product for Delivered orders only? | WHERE, SUM, GROUP BY, ORDER BY |
| Q9 | Average order value per coupon type (excluding no-coupon orders)? | WHERE, AVG, GROUP BY |
| Q10 | Which products exceeded $150,000 in total revenue? | HAVING, SUM, GROUP BY + CTE |

## Notable Technical Decisions

**HAVING vs. SELECT alias**
In Q10, `HAVING SUM(TotalPrice) > 150000` is used instead of `HAVING TotalRevenue > 150000`. This is because HAVING is processed at execution Step 4, before SELECT aliases are created at Step 5 — referencing an alias in HAVING causes an error in SSMS. The aggregate function is repeated directly in the HAVING clause for full SQL Server compatibility.

**Dual-method approach for Q10**
Both a HAVING method and a CTE (WITH clause) method are provided for Q10 to demonstrate two valid approaches to the same problem. The CTE pre-computes the aggregated result, allowing the alias to be freely referenced in the outer WHERE clause — making it the preferred pattern for production SQL readability.

**~No Coupon~ label**
Orders without a coupon code were labelled `~No Coupon~` during the Project 1 cleaning phase. The tilde characters are intentional — they visually distinguish the placeholder from real coupon codes in query results. Q9 filters these out using `WHERE CouponCode != '~No Coupon~'`.

## Repository Contents

| File | Description |
|---|---|
| `Project_3.sql` | Full SQL script with professional header, 10 annotated stakeholder queries, and dual-method Q10 with execution order commentary |

---
*Part of the DecodeLabs Data Analytics Industrial Training Kit — Batch 2026*
