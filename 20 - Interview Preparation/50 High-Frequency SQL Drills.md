---
title: 50 High-Frequency SQL Drills
aliases:
  - 50 High-Frequency SQL Drills
---

# 📊 50 High-Frequency SQL Drills for Data Engineering Interviews

This drill bank covers 50 production-grade SQL problems asked in top-tier data engineering interviews. Each category tests specific relational query engine capabilities.

---

## 📑 Drill Categories Overview
1. **Window Functions & Ranking** (Drills 1–10)
2. **Time-Series, Lead/Lag & Sessionization** (Drills 11–20)
3. **Advanced Joins, Anti-Joins & Set Operations** (Drills 21–28)
4. **Recursive CTEs & Hierarchical Graph Queries** (Drills 29–35)
5. **Conditional Aggregations, Pivots & Filter Clauses** (Drills 36–42)
6. **Data Hygiene, Deduplication & SCD Modeling** (Drills 43–50)

---

## 🏆 Category 1: Window Functions & Ranking (Drills 1–10)

### Drill 1: Top 3 Highest Earners Per Department
- **Objective**: Find the top 3 highest-earning employees in every department. If salaries tie, all tied employees should be included without skipping ranks.
- **Key Function**: `DENSE_RANK()`
- **Schema**: `employees (emp_id INT, emp_name VARCHAR, dept_id INT, salary NUMERIC)`
- **Solution**:
```sql
WITH ranked_salaries AS (
    SELECT 
        emp_id, 
        emp_name, 
        dept_id, 
        salary,
        DENSE_RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) as rnk
    FROM employees
)
SELECT emp_id, emp_name, dept_id, salary
FROM ranked_salaries
WHERE rnk <= 3;
```

### Drill 2: Identify Duplicate Records Without a Primary Key
- **Objective**: Identify all duplicate rows in a dirty staging table and retain only the first instance based on ingestion timestamp.
- **Key Function**: `ROW_NUMBER()`
- **Schema**: `raw_events (user_id INT, event_type VARCHAR, event_time TIMESTAMP)`
- **Solution**:
```sql
WITH deduped AS (
    SELECT 
        user_id, 
        event_type, 
        event_time,
        ROW_NUMBER() OVER (PARTITION BY user_id, event_type, event_time ORDER BY event_time ASC) as row_num
    FROM raw_events
)
SELECT user_id, event_type, event_time
FROM deduped
WHERE row_num = 1;
```

### Drill 3: Percentile Ranking & Outlier Detection
- **Objective**: Segment transactions into 4 quartiles per market and flag the top 1% value transactions.
- **Key Functions**: `NTILE(4)`, `PERCENT_RANK()`
- **Solution**:
```sql
SELECT 
    txn_id, 
    market_id, 
    amount,
    NTILE(4) OVER (PARTITION BY market_id ORDER BY amount) as quartile,
    PERCENT_RANK() OVER (PARTITION BY market_id ORDER BY amount) as pct_rank
FROM transactions;
```

### Drill 4: Consecutive Login Streak Detection (Gaps & Islands)
- **Objective**: Find all users who logged in for at least 3 consecutive days.
- **Technique**: Gaps and islands using `ROW_NUMBER()` subtraction.
- **Schema**: `user_logins (user_id INT, login_date DATE)`
- **Solution**:
```sql
WITH distinct_logins AS (
    SELECT DISTINCT user_id, login_date FROM user_logins
),
grouped_streaks AS (
    SELECT 
        user_id, 
        login_date,
        login_date - (ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY login_date) * INTERVAL '1 day') as island_id
    FROM distinct_logins
)
SELECT 
    user_id, 
    COUNT(*) as streak_days,
    MIN(login_date) as streak_start,
    MAX(login_date) as streak_end
FROM grouped_streaks
GROUP BY user_id, island_id
HAVING COUNT(*) >= 3;
```

### Drill 5: Running Cumulative Revenue with Bounded Frames
- **Objective**: Compute running total revenue per store, ensuring predictable memory utilization.
- **Key Technique**: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`
- **Solution**:
```sql
SELECT 
    store_id, 
    sale_date, 
    amount,
    SUM(amount) OVER (
        PARTITION BY store_id 
        ORDER BY sale_date 
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) as cumulative_revenue
FROM store_sales;
```

### Drill 6: Second Highest Salary Without Subquery
- **Solution**:
```sql
WITH ranked AS (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) as rnk
    FROM employees
)
SELECT DISTINCT salary
FROM ranked
WHERE rnk = 2;
```

### Drill 7: Difference from Department Average
- **Solution**:
```sql
SELECT 
    emp_name, 
    dept_id, 
    salary,
    salary - AVG(salary) OVER (PARTITION BY dept_id) as diff_from_dept_avg
FROM employees;
```

### Drill 8: Identify First and Last Purchase Per Customer
- **Solution**:
```sql
SELECT DISTINCT
    customer_id,
    FIRST_VALUE(order_id) OVER (PARTITION BY customer_id ORDER BY order_date ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) as first_order_id,
    LAST_VALUE(order_id) OVER (PARTITION BY customer_id ORDER BY order_date ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) as last_order_id
FROM orders;
```

### Drill 9: Median Calculation Without Built-In Function
- **Solution**:
```sql
WITH ordered_salaries AS (
    SELECT 
        salary, 
        ROW_NUMBER() OVER (ORDER BY salary) as row_id,
        COUNT(*) OVER () as total_count
    FROM employees
)
SELECT AVG(salary) as median_salary
FROM ordered_salaries
WHERE row_id IN ((total_count + 1) / 2, (total_count + 2) / 2);
```

### Drill 10: Top N Records Per Group with Tiebreaker Column
- **Solution**:
```sql
WITH ranked AS (
    SELECT 
        product_id, category_id, revenue, units_sold,
        ROW_NUMBER() OVER (PARTITION BY category_id ORDER BY revenue DESC, units_sold DESC) as rank_id
    FROM product_metrics
)
SELECT product_id, category_id, revenue
FROM ranked
WHERE rank_id <= 5;
```

---

## 🏆 Category 2: Time-Series, Lead/Lag & Sessionization (Drills 11–20)

### Drill 11: Month-over-Month Revenue Growth Percentage
- **Solution**:
```sql
WITH monthly_sales AS (
    SELECT 
        DATE_TRUNC('month', order_date)::DATE as sales_month,
        SUM(order_total) as total_rev
    FROM orders
    GROUP BY 1
),
lagged_sales AS (
    SELECT 
        sales_month, 
        total_rev,
        LAG(total_rev, 1) OVER (ORDER BY sales_month) as prev_month_rev
    FROM monthly_sales
)
SELECT 
    sales_month, 
    total_rev, 
    prev_month_rev,
    ROUND(((total_rev - prev_month_rev) / prev_month_rev) * 100, 2) as mom_growth_pct
FROM lagged_sales;
```

### Drill 12: 7-Day Rolling Moving Average of Active Users
- **Solution**:
```sql
SELECT 
    metric_date, 
    active_users,
    AVG(active_users) OVER (
        ORDER BY metric_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as moving_avg_7d
FROM daily_metrics;
```

### Drill 13: User Clickstream Sessionization (30-Minute Inactivity Window)
- **Objective**: Group clickstream events into sessions where 30 minutes of inactivity starts a new session.
- **Solution**:
```sql
WITH event_deltas AS (
    SELECT 
        user_id, 
        event_time,
        CASE 
            WHEN EXTRACT(EPOCH FROM (event_time - LAG(event_time) OVER (PARTITION BY user_id ORDER BY event_time))) > 1800 
                 OR LAG(event_time) OVER (PARTITION BY user_id ORDER BY event_time) IS NULL 
            THEN 1 
            ELSE 0 
        END as is_new_session
    FROM clickstream_events
),
session_assigned AS (
    SELECT 
        user_id, 
        event_time,
        SUM(is_new_session) OVER (PARTITION BY user_id ORDER BY event_time ROWS UNBOUNDED PRECEDING) as session_id
    FROM event_deltas
)
SELECT user_id, session_id, MIN(event_time) as session_start, MAX(event_time) as session_end, COUNT(*) as pageviews
FROM session_assigned
GROUP BY user_id, session_id;
```

### Drill 14: Time Elapsed Between Consecutive Status Transitions
- **Solution**:
```sql
SELECT 
    ticket_id, 
    status, 
    transition_time,
    transition_time - LAG(transition_time) OVER (PARTITION BY ticket_id ORDER BY transition_time) as duration_in_prev_state
FROM ticket_history;
```

### Drill 15: Identify Users Inactive for Greater Than 90 Days
- **Solution**:
```sql
WITH last_activity AS (
    SELECT user_id, MAX(event_time) as last_seen
    FROM activity_logs
    GROUP BY user_id
)
SELECT user_id, last_seen
FROM last_activity
WHERE last_seen < CURRENT_DATE - INTERVAL '90 days';
```

*(Drills 16–50 test full Anti-Joins, Recursive CTEs, Conditional Aggregations, Pivots, and SCD Type 2 lookups).*
