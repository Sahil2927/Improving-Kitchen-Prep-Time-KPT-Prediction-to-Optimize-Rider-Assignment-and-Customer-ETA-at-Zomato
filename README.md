# SmartKPT
### Improving Kitchen Prep Time (KPT) Prediction to Optimize Rider Assignment and Customer ETA

---

## Project Overview

Food delivery platforms heavily rely on accurate **Kitchen Prep Time (KPT)** prediction to:

- Dispatch riders efficiently  
- Provide reliable customer ETAs  
- Reduce SLA violations  
- Minimize refund costs  

Traditional systems use **static restaurant averages**, which fail during congestion, peak hours, or demand spikes.

This project builds a **congestion-aware, production-grade ML pipeline** to dynamically predict prep time and simulate its impact on:

- Late deliveries  
- Rider idle time  
- Severe delays  
- Financial savings  

---

## Problem Statement

Static ETA estimation leads to:

- Rider idle waiting at restaurants  
- Late deliveries during peak congestion  
- Refund payouts for severe delays  
- Poor customer experience  

We solve this by:

> Predicting prep time dynamically using real-time operational signals and simulating full business impact.

---

## 🧠 Solution Architecture

### 1️⃣ Synthetic Operational Data Generation

We simulate:

- 200 restaurants  
- 30 days of operations  
- 5-minute arrival windows  
- Realistic lunch/dinner peaks  
- Weather and festival spikes  
- Nonlinear congestion behavior  
- Heavy-tail rare delays  

This creates **550K+ realistic order records** with operational variability.

---

### 2️⃣ Feature Engineering

Key engineered signals:

- Kitchen utilization  
- Queue length  
- Congestion regime (bucketized stress levels)  
- Congestion × complexity interaction  
- Log queue transformation  
- Time cyclic features  

These features help model nonlinear congestion dynamics.

---

### 3️⃣ Congestion-Aware ML Model

We use:

- **LightGBM Regressor**
- Huber loss (robust to extreme delays)
- TimeSeries cross-validation
- Congestion-weighted training
- Early stopping

**Why LightGBM?**

- Handles nonlinear effects  
- Efficient on large datasets  
- Production scalable  
- Strong performance on tabular data  

---

## 📊 Model Performance

| Metric | Value |
|--------|-------|
| MAE | ~2.0 minutes |
| RMSE | ~3.7 minutes |
| R² | ~0.86 |
| Congestion MAE | ~2.7 minutes |

The model significantly improves performance during high-utilization scenarios.

---

# 📈 Business Impact Simulation

We simulate dispatch decisions using:

- **Baseline:** Static restaurant average  
- **ML Model:** Dynamic congestion-aware ETA  

---

## 🕒 Late Delivery Rate

| System | Late Rate |
|--------|-----------|
| Baseline | 10.11% |
| ML Model | 1.72% |

✅ **82% reduction in late deliveries**

---

## 🚨 Severe Delay Rate (>10 min)

| System | Severe Rate |
|--------|------------|
| Baseline | 1.8% |
| ML Model | 0.75% |

✅ **58% reduction in severe delays**

---

## 🚴 Rider Impact Simulation

We simulate rider dispatch timing and compute:

- Rider idle waiting  
- Food waiting at restaurant  
- Occurrence rates  

### Results

| Metric | Baseline | ML |
|--------|----------|----|
| Avg Rider Wait | 2.6 min | 0.43 min |
| Rider Wait Rate | 45% | 12% |

✅ **83% reduction in rider idle time**

---

# 💰 Financial Impact Estimation

### Assumptions

- ₹2 per rider idle minute  
- ₹40 refund per severe delay  
- Scaled to **1,000,000 orders**

### Projected Savings per 1M Orders

- Rider Idle Savings: ₹4.32M  
- Refund Savings: ₹0.42M  
- **Total Estimated Savings: ₹4.73M**

> Conservative estimate (excludes retention & brand impact).

---

# 🏗 Project Structure
