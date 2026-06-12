# 🚖 Ola NCR Ride Cancellation Analysis

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Project Overview

This project presents a comprehensive **data analytics case study** on Ola ride cancellations across the **National Capital Region (NCR), India** for the year **2024**. The goal is to identify key patterns, root causes, and business impact of ride cancellations — and provide actionable recommendations to reduce cancellation rates.

---

## 🎯 Problem Statement

Ola NCR recorded a **32% cancellation rate** in 2024, resulting in an estimated revenue loss of **₹19.06 Million**. This analysis digs into:

- **Who** is cancelling rides — drivers or customers?
- **Why** are rides being cancelled?
- **When** do cancellations peak — by hour, day, or month?
- **Where** are cancellations most concentrated?
- **What** is the financial impact on the business?

---

## 📊 Dataset Description

| Property | Details |
|---|---|
| **Source** | NCR Ride Bookings Dataset |
| **Time Period** | January 2024 — December 2024 |
| **Total Records** | 1,50,000 rides |
| **Total Columns** | 21 |
| **Vehicle Types** | 7 (Auto, Go Mini, Go Sedan, Bike, Premier Sedan, eBike, Ola XL) |
| **Pickup Locations** | 176 unique locations across NCR |

### Key Columns:
- `Date`, `Time`, `Booking ID`, `Booking Status`
- `Vehicle Type`, `Pickup Location`, `Drop Location`
- `Avg VTAT` (Vehicle Time at Arrival), `Avg CTAT` (Customer Time at Arrival)
- `Cancelled Rides by Customer`, `Reason for cancelling by Customer`
- `Cancelled Rides by Driver`, `Driver Cancellation Reason`
- `Incomplete Rides`, `Incomplete Rides Reason`
- `Booking Value`, `Ride Distance`, `Driver Ratings`, `Customer Rating`
- `Payment Method`

---

## 🔢 Key Metrics

| Metric | Value |
|---|---|
| Total Rides | 1,50,000 |
| Completed Rides | 93,000 (62%) |
| Cancelled by Driver | 27,000 (18%) |
| No Driver Found | 10,500 (7%) |
| Cancelled by Customer | 10,500 (7%) |
| Incomplete Rides | 9,000 (6%) |
| Overall Cancellation Rate | 32% |
| Avg Booking Value (Completed) | ₹508 |
| Estimated Revenue Lost | ₹19.06 Million |

---

## 💡 Key Insights

### 1. Driver Cancellations Dominate
- Drivers cancel **2.57x more** than customers (27,000 vs 10,500)
- Top driver reason: **Customer related issues** (6,837 cases)
- Followed by: Customer was coughing/sick, Personal & Car issues, Overcrowding

### 2. Customer Cancellation Patterns
- Top customer reason: **Wrong Address** (2,362 cases)
- Followed by: Change of plans, Driver not moving, Driver asked to cancel
- **"Driver asked to cancel"** appearing in customer reasons suggests forced cancellations

### 3. Vehicle Type Analysis
- **Auto** has the highest cancellation volume (37,419 total rides)
- **Ola XL** has the lowest volume but needs further rate analysis
- **eBike** shows significant No Driver Found issues

### 4. Time Patterns
- Peak cancellation hours align with **morning (8–10 AM)** and **evening (6–9 PM)** rush hours
- **Weekdays** show significantly higher cancellations than weekends

### 5. Payment Insights
- **UPI** is the dominant payment method (45,909 rides — 44%)
- **Cash** still accounts for 25,367 rides (24%)

---

## 📋 Dashboard Pages

### Page 1 — Overview and cancellation deep dive and location
> KPI cards, Booking Status distribution, Rides by Vehicle Type

> Customer cancellation reasons, Driver cancellation reasons, Treemap by vehicle type, Incomplete ride reasons

### Page 3 — Time Analysis and revenue
> Cancellations by Month, Hour of Day, and Day of Week
> Top 10 Pickup locations by cancellations, Payment method distribution, Avg Booking Value by vehicle type

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Power BI** | Dashboard creation & visualization |
| **Power Query** | Data cleaning & transformation |
| **DAX** | Custom measures & calculations |
| **Microsoft Excel** | Initial data exploration |

---

## 🧹 Data Cleaning Steps

1. Fixed `Date` and `Time` column data types
2. Extracted `Hour`, `Month Name`, `Day of Week` columns
3. Cleaned `Booking ID` and `Customer ID` (removed extra quotes)
4. Replaced nulls with `0` in cancellation flag columns
5. Created unified `Cancellation Reason` column using conditional logic

---

## 📐 DAX Measures Created

```dax
-- Total Rides
Total Rides = COUNTROWS('ncr_ride_bookings')

-- Cancellation Rate
Cancellation Rate = 
DIVIDE(
    COUNTROWS(FILTER('ncr_ride_bookings', 
        'ncr_ride_bookings'[Booking Status] IN 
        {"Cancelled by Driver", "Cancelled by Customer", "No Driver Found"})),
    COUNTROWS('ncr_ride_bookings')
)

-- Revenue Lost
Revenue Lost = 
AVERAGEX(
    FILTER('ncr_ride_bookings', 
        'ncr_ride_bookings'[Booking Status] = "Completed"),
    'ncr_ride_bookings'[Booking Value]
) * 
COUNTROWS(FILTER('ncr_ride_bookings', 
    'ncr_ride_bookings'[Booking Status] IN 
    {"Cancelled by Driver", "Cancelled by Customer"}))
```

---

## ✅ Business Recommendations

1. **Driver Behaviour Training** — Address top driver cancellation reasons through training and strict policy enforcement
2. **Address Verification** — Improve in-app address confirmation to reduce "Wrong Address" cancellations
3. **Peak Hour Incentives** — Offer surge bonuses during 8–10 AM and 6–9 PM to retain drivers
4. **Auto Category Focus** — Investigate why Auto has highest cancellations despite highest volume
5. **Forced Cancellation Detection** — Flag cases where customers report "Driver asked to cancel" for investigation
6. **Driver Supply Management** — Increase driver availability in top 10 high-cancellation pickup zones

---

## 📁 Repository Structure

```
ola-ride-cancellation-analysis/
│
├── 📊 Ola_NCR_Dashboard.pbix      # Power BI Dashboard file
├── 📄 ncr_ride_bookings.csv        # Raw dataset
├── 📁 screenshots/                 # Dashboard page screenshots
│   ├── Ride_cancellation_analysis.png
│   ├── time_analysis.png
└── 📝 README.md                    # Project documentation
```

---

## 🚀 How to Use

1. Clone this repository
2. Open `Ola_NCR_Dashboard.pbix` in **Power BI Desktop**
3. If data doesn't load, update the data source path to your local `ncr_ride_bookings.csv`
4. Explore both dashboard pages using the slicers to filter by Date and Vehicle Type

---

## 👩‍💻 Author

**[Rimjhim Chawla]**  
Aspiring Data Analyst | Power BI | Excel | SQL  
📧 [rimjhimchawla22@gmail.com]  
🔗 [www.linkedin.com/in/rimjhim-chawla-1994112b8]  
🐙 [https://github.com/Rimjhim2208]

---

## 📌 Tags
`Data Analytics` `Power BI` `Ola` `Ride Cancellation` `NCR` `Dashboard` `Case Study` `DAX` `Data Visualization`
