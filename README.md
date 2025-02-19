# Twitter Analytics Power BI Dashboard - README

## Overview
This Power BI dashboard is designed to analyze Twitter engagement data, including impressions, likes, retweets, media views, and user interactions. The dashboard consists of two pages:

1. **Page 1:** General Twitter engagement metrics and trends.
2. **Page 2:** Task-specific charts fulfilling three predefined tasks based on engagement criteria and time-based visibility constraints.

## Data Sources
- The dashboard is built using two similar but distinct sheets (`Sheet1` and `SocialMedia (1)`).
- The dataset includes key columns such as:
  - `engagement rate`
  - `likes`
  - `media views`
  - `replies`
  - `tweet character count`
  - `tweet word count`
  - `impressions`
  - `tweet date`

## Task-Based Charts (Page 2)
The second page contains three charts, each controlled by time-based visibility constraints in **Indian Standard Time (IST)**:

### **1. Top Tweets by Engagement Rate**
- **Filters Applied:**
  - Displays top 10% engagement rate tweets.
  - Includes only tweets with **more than 50 likes**.
  - Must have been **posted on weekdays**.
  - The tweet character count **must be below 30**.
- **Time Visibility Constraint:**
  - Visible **only between 3 PM - 5 PM IST**.
  - Hidden outside this time range.
- **DAX Query for Visibility:**
```DAX
Chart1_Visible =
IF(
    HOUR(UTCNOW()) + 5.5 >= 15 && HOUR(UTCNOW()) + 5.5 <= 17,
    1, 0
)
```

### **2. Media Engagements vs. Media Views (Scatter Chart)**
- **Filters Applied:**
  - Analyzes tweets with **more than 10 replies**.
  - Highlights tweets with an **engagement rate above 5%**.
  - The tweet date **must be an odd number**.
  - The tweet **word count must be above 50**.
- **Time Visibility Constraint:**
  - Visible **only between 6 PM - 11 PM IST**.
  - Hidden outside this time range.
- **DAX Query for Visibility:**
```DAX
Chart2_Visible =
IF(
    HOUR(UTCNOW()) + 5.5 >= 18 && HOUR(UTCNOW()) + 5.5 <= 23,
    1, 0
)
```

### **3. Media Engagements & Views by Weekdays (Dual-Axis Chart)**
- **Filters Applied:**
  - Displays media engagements and views for the **last quarter**.
  - Highlights days with **significant spikes** in media interactions.
  - The tweet **impressions must be an even number**.
  - The tweet **date must be an odd number**.
  - The **tweet character count must be above 30**.
  - **Tweets containing words with the letter 'H' are removed**.
- **Time Visibility Constraint:**
  - Visible **only between 3 PM - 5 PM IST and 7 AM - 11 AM IST**.
  - Hidden outside these time ranges.
- **DAX Query for Visibility:**
```DAX
Chart3_Visible =
IF(
    (HOUR(UTCNOW()) + 5.5 >= 15 && HOUR(UTCNOW()) + 5.5 <= 17) ||
    (HOUR(UTCNOW()) + 5.5 >= 7 && HOUR(UTCNOW()) + 5.5 <= 11),
    1, 0
)
```

## Implementation
1. **Add these DAX formulas as calculated columns** in Power BI.
2. **Apply Visual-Level Filters** to each chart:
   - `Chart1_Visible = 1` for **Task 1 chart**.
   - `Chart2_Visible = 1` for **Task 2 chart**.
   - `Chart3_Visible = 1` for **Task 3 chart**.
3. The charts will **automatically hide** outside their designated time slots.

## Notes
- The `UTCNOW()` function is adjusted by **+5.5 hours** to align with **IST**.
- Power BI **must refresh regularly** to ensure real-time time-based filtering.
- This setup ensures a **dynamic, time-sensitive experience** based on Twitter analytics data.
