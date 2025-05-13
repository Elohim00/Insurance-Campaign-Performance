# 📊 Insurance Campaign Performance Analysis

> **Strategic Dashboard & Conversion Intelligence Using Power BI + DAX**

---

## 🧭 Executive Summary

In 2019, a national insurance provider launched a large-scale telemarketing campaign to acquire new customers. Despite making **45,211 outbound calls**, the campaign yielded only **5,289 conversions**, reflecting a modest **11.7% conversion rate** and an average of **23.63 calls per conversion**.

Through advanced segmentation, behavior analytics, and timing optimization in Power BI, this project reveals how to **elevate conversion rates by 10–15%** by shifting from mass outreach to **precision targeting**.

### 🚀 Key Outcomes

- 🎯 **Identified top-converting personas** (e.g., married executives aged 25–34 using mobile) with **2x higher conversion** than campaign average.
- 🕒 **Defined optimal contact timing**: Monday–Tuesday, 6–15 minute calls, 2–3 attempts.
- ⚠️ **Flagged inefficiencies**: landline contacts, students, and Friday calls drove high cost per conversion.

---

## 📚 Table of Contents

1. [🎯 Project Title & Problem Statement](#-project-title--problem-statement)  
2. [📊 Data Description](#-data-description)  
3. [⚙️ Methodology](#-methodology)  
4. [🧠 DAX Feature Engineering](#-dax-feature-engineering)  
5. [📈 Key Visuals](#-key-visuals)  
6. [🔍 Strategic Insights](#-strategic-insights)  
7. [📝 Business Recommendations](#-business-recommendations)  
8. [🧰 Tools & GitHub Repository](#-tools--github-repository)  
9. [🏁 Business Impact & Reflection](#-business-impact--reflection)  

---

## 🎯 Project Title & Problem Statement

### **Title:**  
**Customer Conversion Intelligence for Insurance Campaign Optimization**

### **Problem Statement:**  
Despite making 45,211 outbound calls, the insurer achieved only an 11.7% conversion rate, with 23.63 calls required per successful sale.

### **Challenges Identified:**

- ❓ **Unclear segmentation**: What traits actually drive conversions?
- 💸 **High cost per sale**: Inefficient call strategy and poor targeting.

### **Business Objective:**  
Uncover data-driven answers to:

- Who are the most responsive customers?
- What channels and timing yield the highest ROI?
- How can we optimize conversion without increasing call volume?

---

## 📊 Data Description

### **Dataset Overview**

- 📁 **Source:** Internal CRM – 2019 Campaign Data  
- 🔢 **Volume:** 45,211 call records  
- 🎯 **Target Variable:** `conversion_status` (Yes/No)

### **Key Attributes:**

- 👤 Demographics: Age, Marital Status, Occupation, Education  
- 📞 Engagement: Call Duration, Frequency, Call Date  
- 📱 Channel: Mobile, Landline, Unidentified  
- 🕰️ History: Prior campaign results

### **Data Preparation:**

- Cleaned nulls, standardized formatting  
- Binned variables: age, duration, frequency  
- Created derived columns: Weekday, Month, Personas  
- Filtered invalid conversion records to preserve model accuracy

---

## ⚙️ Methodology

### 🧪 Exploratory Data Analysis (EDA)

- Segment-wise analysis across demographics, behavior, and channel
- Correlation assessment of variables with conversion likelihood
- Created persona-based views and funnel performance breakdowns

### 📈 Modeling & Visualization Tools

- **Power BI** for dynamic, drillable dashboards  
- **DAX** for engineered KPIs and segmentation logic  
- **Excel/CSV** for initial wrangling

---

## 🧠 DAX Feature Engineering
## 📐 DAX Measures

```DAX
-- Age Buckets
AgeGroup =
    SWITCH (
        TRUE (),
        [age] <= 24, "18–24",
        [age] <= 34, "25–34",
        [age] <= 44, "35–44",
        [age] <= 54, "45–54",
        [age] <= 64, "55–64",
        "65+"
    )

-- Call Duration Segments
CallDurationGroup =
    SWITCH (
        TRUE (),
        [call_duration] <= 2, "0–2 min",
        [call_duration] <= 5, "3–5 min",
        [call_duration] <= 15, "6–15 min",
        [call_duration] <= 30, "16–30 min",
        "31+ min"
    )

-- Frequency Group
CallFrequencyGroup =
    SWITCH (
        TRUE (),
        [call_frequency] = 1, "1 call",
        [call_frequency] <= 3, "2–3 calls",
        [call_frequency] <= 6, "4–6 calls",
        [call_frequency] <= 10, "7–10 calls",
        "11+ calls"
    )

-- Weekday & Month
CallWeekday = FORMAT([call_date], "dddd")
CallMonth = FORMAT([call_date], "MMMM")

-- Conversion Binary Flag
Converted = IF([conversion_status] = "Yes", 1, 0)

-- Persona Creation
Persona =
    'Marketing Dataset'[Marital_Status] & " - " &
    'Marketing Dataset'[Occupation] & " - " &
    'Marketing Dataset'[AgeGroup] & " - " &
    'Marketing Dataset'[channel]
```



# 📈 Key Visuals

## 📊 Dashboard Highlights

📌 **Executive Overview (KPIs + Summary)**
📌 **Conversion Drivers by Persona**
📌 **Channel Performance: Mobile vs Landline**
📌 **Best Call Timing Heatmap**

---

# 🔍 Strategic Insights

### 🔥 High-Performing Segments
| Persona Attribute | Value     |
| ----------------- | --------- |
| Marital Status    | Married   |
| Occupation        | Executive |
| Age Group         | 25–34     |
| Preferred Channel | Mobile    |
| Conversion Rate   | Over 23%  |

**Engagement Traits:**

* Stable income, high responsiveness
* Engage on Mon/Tue, 6–15 min calls
* Convert within 2–3 attempts

Insights:
This group significantly outperforms all others — converting at over 23%, which is more than twice the campaign average. Their profile indicates stable income and high responsiveness. They engage best on Monday and Tuesday, during 6–15 minute calls, and typically convert within 2–3 attempts. These traits suggest decisiveness and efficiency. This persona is ideal for focused, high-priority outreach with minimal effort and high return.

---

### 🟡 Mid-Performing Segments

| Persona Attribute | Value                  |
| ----------------- | ---------------------- |
| Marital Status    | Mixed (Single/Married) |
| Occupation        | Educated Professionals |
| Age Group         | 35–44                  |
| Preferred Channel | Mixed                  |
| Conversion Rate   | Moderate (\~10–15%)    |

* Educated professionals aged 35–44
* Require 4–6 attempts, longer call durations
* Convert best early in month (March, May, August)
* Suitable for nurture campaigns

Insights:
These individuals show moderate conversion rates, particularly when contacted early in the month (March, May, August stand out). They tend to require 4–6 call attempts and prefer longer conversations, indicating that while interested, they need more time and touchpoints to make decisions. They are ideal candidates for nurturing campaigns, where education and consistent engagement can lead to conversions over time.
---

### 🔻 Low-Performing Segments


| Persona Attribute | Value                           |
| ----------------- | ------------------------------- |
| Marital Status    | Mixed                           |
| Occupation        | Students / Unemployed           |
| Age Group         | 18–24                           |
| Preferred Channel | Landline                        |
| Conversion Rate   | <5% (Students), <10% (Landline) |


* Students, unemployed: <5% conversion
* Landline users: <10% of conversions, 7+ call attempts
* Friday outreach = lowest response rates
* High resource drain with poor ROI


Insights:
This segment has the lowest return on investment. Students and unemployed individuals rarely convert, with rates under 5%. Landline users account for less than 10% of conversions, despite requiring 7 or more call attempts. Outreach on Fridays also performs poorly across the board, suggesting timing fatigue. These leads result in high resource usage with minimal return, and efforts here should be minimized or rerouted to automated low-cost channels.

---

# ⚙️ Operational Inefficiencies

* 📱 **Mobile calls convert 8× better** than landline
* ❗ Yet, call volume was evenly split — major inefficiency
* 📊 10% of data had **unclassified channels**, creating blind spots in targeting

---

# 📝 Business Recommendations

### 🎯 Persona Targeting

✅ Focus: Married + Executive + Mobile + Age 25–34
❌ Deprioritize: Students, landline-only leads

---

### 📆 Timing Strategy

📅 Call on **Monday/Tuesday**
⏱️ Target call duration: **6–15 minutes**

---

### 📞 Channel Optimization

* Prioritize mobile
* Limit landline attempts
* Invest in predictive mobile dialers

---

### ⏱️ Touchpoint Control

* Cap follow-ups to **2–3 calls per lead**
* Send **SMS/email nudges pre-call** to warm leads

---

### 🧼 Data Quality

* Clean & classify **\~10% unknown channels**
* Refresh **persona models quarterly** based on trends

---

# 🧰 Tools & GitHub Repository

### 🔧 Tools Used

* **Power BI** – storytelling & dashboarding
* **DAX** – KPI, segment & persona logic
* **Excel/CSV** – raw data cleaning

---

### 📁 Repository Structure

```
Insurance-Campaign-Conversion/
├── README.md
├── visuals/
│   ├── overview.png
│   ├── drivers.png
│   ├── channel.png
│   └── timing.png
├── dax-measures/
│   └── persona_kpis.dax
├── data/
│   └── sample-marketing-data.csv
```

👉 **GitHub Repo:** \[Insert Your Link Here]

---

# 🏁 Business Impact & Reflection

### 💡 Business Value

📈 +10–15% projected uplift in conversion rate
💰 Reduced cost-per-sale via **precise targeting**
🎯 Scalable framework for **data-driven campaign optimization**

---

### 🧠 Personal Reflection

> “This project deepened my fluency in both **analytics and strategy**. It taught me how to go beyond metrics and build a **data story that drives business decisions**. By aligning behavioral insight with segmentation and timing, I transformed outreach into intelligent engagement.”

---

💬 **“Let the data tell the story—then let the story drive better decisions.”**

---

### ✅ How to Use

Just paste the above **as plain text** into your `README.md` on GitHub. It will **render emojis, bold text, spacing, and bullet points cleanly** without being inside any code block or fenced formatting.

Let me know if you want a downloadable `.md` file or styled HTML version for a portfolio site!
