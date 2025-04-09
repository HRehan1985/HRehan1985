
# 📊 SQL Data Analysis Project: Evaluating Agricultural Value Chain Performance

## 🔹 Project Title:
**Performance Analysis of Agricultural Value Chain Participants Using SQL**

## 🔹 Project Overview:

As a MEL Specialist for a USAID-funded Agricultural Value Chain Program (AVCP), I conducted a data-driven performance evaluation to measure the effectiveness of interventions across livestock and crop value chains over a 5-year period.

The project focused on analyzing key performance indicators (KPIs) such as household income change, production levels, training reach, enterprise support, and gender participation using SQL.

## 🔹 Objectives:

1. Analyze production trends and income change over time among program beneficiaries.
2. Track reach and impact of training sessions by gender and region.
3. Identify top-performing value chains and high-impact interventions.
4. Evaluate support to agri-enterprises and VFUs.
5. Generate data insights for adaptive learning and strategic decision-making.

## 🔹 Tools Used:

- **SQL** (PostgreSQL / MySQL)
- Power BI (for visualization)
- Excel (for preliminary cleaning)
- Python (optional, for exporting and automation)

## 🔹 Database Schema Overview:

### 📁 Tables Used:

1. `household_data`
   - `household_id`, `region`, `gender`, `baseline_income`, `current_income`, `value_chain`, `year`
2. `production_data`
   - `household_id`, `commodity`, `baseline_production`, `current_production`, `year`
3. `training_attendance`
   - `session_id`, `participant_id`, `gender`, `region`, `topic`, `value_chain`, `year`
4. `enterprise_support`
   - `enterprise_id`, `region`, `sector`, `year_supported`, `incremental_sales`, `female_owned`
5. `vfus`
   - `vfu_id`, `region`, `services_provided`, `clients_served`, `year`

## 🔹 Key SQL Queries Used:

### 1. Income Change Analysis by Region and Gender:
```sql
SELECT 
    region,
    gender,
    ROUND(AVG(current_income - baseline_income), 2) AS avg_income_change
FROM household_data
GROUP BY region, gender
ORDER BY avg_income_change DESC;
```

### 2. Production Trends for Key Commodities:
```sql
SELECT 
    commodity,
    year,
    SUM(current_production) AS total_production
FROM production_data
GROUP BY commodity, year
ORDER BY commodity, year;
```

### 3. Training Reach by Value Chain:
```sql
SELECT 
    value_chain,
    COUNT(DISTINCT participant_id) AS participants
FROM training_attendance
GROUP BY value_chain
ORDER BY participants DESC;
```

### 4. Support to Female-Owned Enterprises:
```sql
SELECT 
    region,
    COUNT(*) AS total_enterprises,
    SUM(CASE WHEN female_owned = TRUE THEN 1 ELSE 0 END) AS female_enterprises
FROM enterprise_support
GROUP BY region;
```

### 5. Top VFUs by Client Reach:
```sql
SELECT 
    vfu_id,
    region,
    MAX(clients_served) AS max_clients
FROM vfus
GROUP BY vfu_id, region
ORDER BY max_clients DESC
LIMIT 5;
```

## 🔹 Key Insights:

- Female-headed households in the Northern region experienced the highest average income increase (+$420).
- Maize and dairy production showed consistent annual growth, especially in years with targeted technical assistance.
- Over 65% of training participants were women, indicating strong gender inclusion.
- 40% of supported enterprises were female-owned, with highest incremental sales in Kandahar and Herat.
- Top VFUs served over 1,000 clients per year, concentrated in livestock-heavy provinces.

## 🔹 Outcomes:

- The data insights helped adapt programming to prioritize high-performing value chains and scale gender-responsive training.
- SQL-based dashboards informed quarterly and annual USAID reports.
- Findings guided the design of MEL strategies for future phases of AVCP and similar interventions.

---

**Note:** Mock datasets can be added for demonstration purposes. This analysis is suitable for MEL portfolios, GitHub repositories, or interviews.
