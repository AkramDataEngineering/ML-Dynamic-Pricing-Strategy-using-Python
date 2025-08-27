# ML-Dynamic-Pricing-Strategy-using-Python
# ⚖️ Dynamic Pricing Strategy with Python

**Project:** Build a data-driven dynamic pricing strategy to adjust prices in real time using demand, supply, and contextual features.  
**Goal:** Optimize revenue and balance supply–demand by setting flexible, data-backed prices for services (example: ride-sharing).

---

## 📌 Overview & Motivation (more detailed)
Dynamic pricing uses data science and algorithms to change prices dynamically based on factors like demand, supply, time, customer segments, and competitor pricing. Retailers, airlines, ride-hailing, and hospitality platforms use dynamic pricing to maximize revenue and utilization while maintaining customer satisfaction.

This project demonstrates a **practical pipeline** for creating a dynamic pricing model:
- exploratory data analysis (EDA)
- rule-based multiplier strategy (demand × supply)
- ML-based price prediction (Random Forest)
- evaluation and visualization
It’s tailored to a ride-sharing example but the approach generalizes to ecommerce, hotels, and ticketing.

---

## 🔍 Business Use Case: Ride-Sharing Example
Imagine a ride-hailing company operating in a metro area. Fixed per-km pricing fails to capture surges in demand, driver scarcity, or special events. A dynamic strategy:
- Increases prices during high demand / low driver supply (surge)
- Reduces prices during low demand / high supply (discounts)
- Differentiates by vehicle type (premium vs economy) and booking time
The result: better driver availability, improved revenue, and more efficient matching.

---

## 🗂 Dataset (example)
Typical columns:
- `Number_of_Riders`, `Number_of_Drivers` — demand & supply signals  
- `Location_Category` (Urban/Suburban/Rural)  
- `Customer_Loyalty_Status` (Silver/Regular/VIP)  
- `Number_of_Past_Rides`, `Average_Ratings`  
- `Time_of_Booking`, `Vehicle_Type` (Premium/Economy)  
- `Expected_Ride_Duration` (mins)  
- `Historical_Cost_of_Ride` (base price)

> Example dataset: `dynamic_pricing.csv` (1000 rows sample for experimentation).

---

## 🧭 Exploratory Data Analysis (EDA) — Key Insights
- **Descriptive Stats:** Understand central tendency & spread (means, percentiles).  
- **Duration vs Cost:** Positive trend — longer rides cost more historically.  
- **Vehicle Type Impact:** Premium rides have higher median & variance in costs.  
- **Correlation Matrix:** Identify features strongly associated with price (e.g., riders, drivers, duration).  
EDA helps choose features and design rules or model inputs.

---

## 🛠 Dynamic Pricing Strategy (Rule-based approach)
A simple, interpretable approach uses **multipliers**:

1. Compute demand multiplier:
   ```py
   demand_multiplier = np.where(
       riders > pctile_high, riders / pctile_high, riders / pctile_low
   )

