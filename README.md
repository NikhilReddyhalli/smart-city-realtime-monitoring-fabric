# 🌆 Smart City Real-Time Air Quality Monitoring System  
### Built using Microsoft Fabric | Eventstream | KQL | Power BI

---

## 📌 Project Overview

This project simulates a large-scale **Smart City IoT Air Quality Monitoring System** using Microsoft Fabric.

The system ingests real-time sensor data, performs time-series analytics using KQL, and provides both:

- ⚡ Operational Monitoring (Real-Time Dashboard)
- 📊 Executive Analytics (Power BI Report)

It demonstrates real-time ingestion patterns, time-series analysis, anomaly detection logic, and dashboard design principles.

---

## 🏗 Architecture

IoT Data Simulator (Notebook)  
  ↓  
Lakehouse (Delta Raw Storage)  
  ↓  
External Table (KQL Shortcut)  
  ↓  
Fabric Data Pipeline (Incremental Ingestion)  
  ↓  
Eventhouse (KQL Database)  
  ↓  
Real-Time Dashboard + Power BI Report  

---

## ⚡ Key Features

### 🔄 Real-Time Data Pipeline
- Simulated IoT sensor data generation
- Incremental ingestion using KQL `.set-or-append`
- Automated pipeline orchestration
- Data freshness monitoring (Data Delay KPI)

### 📈 Time-Series Analytics (KQL)
- 1-minute bin aggregation
- Rolling time-window analysis
- Zone-level pollution comparison
- Risk classification using case logic
- Severe event detection (PM2.5 > 200)

### 🚨 Intelligent Monitoring
- Risk Status indicator (SAFE / MODERATE / HIGH RISK / CRITICAL)
- Top 15 severe pollution alerts
- Data pipeline health indicator
- Executive KPI summary row

---

## 📊 Dashboards

### 🟢 Real-Time Operational Dashboard
Designed for control-room style monitoring.

Includes:
- Current Avg PM2.5
- Peak PM2.5
- Data Delay (pipeline health)
- Risk Status indicator
- City-wide PM2.5 trend (2-hour window)
- Zone risk comparison
- Severe alert panel

### 🔵 Power BI Executive Report
Designed for strategic insights.

Includes:
- Executive KPI summary
- Pollution trend analysis
- Zone performance breakdown
- Severity distribution
- Interactive filtering by zone

---

## 🧠 KQL Logic Highlights

**Trend Analysis**
SensorEvents  
| where timestamp_utc > ago(2h)  
| summarize avg_pm25 = avg(pm25) by bin(timestamp_utc, 1m)  
| order by timestamp_utc asc  

**Zone Risk Classification**
SensorEvents  
| summarize avg_pm25 = avg(pm25) by zone_name  
| extend risk_level =  
  case(  
   avg_pm25 > 200, "Severe",  
   avg_pm25 > 150, "High",  
   avg_pm25 > 100, "Moderate",  
   "Normal"  
  )  

**Severe Pollution Alerts**
SensorEvents  
| where pm25 > 200  
| project timestamp_utc, zone_name, pm25  
| order by pm25 desc  
| take 15  

---

## 🛠 Technologies Used

- Microsoft Fabric
- Eventstream
- Eventhouse (KQL Database)
- Lakehouse (Delta format)
- Fabric Data Pipeline
- Power BI
- Python (IoT data simulation)

---

## 🎯 What This Project Demonstrates

- Real-time ingestion architecture
- Fabric-native orchestration
- KQL time-series analytics
- Risk-based classification logic
- Operational vs analytical dashboard design
- Monitoring pipeline health
- Clean portfolio documentation

---

## 🚀 Future Enhancements

- Machine learning-based anomaly detection
- Geo-spatial pollution mapping
- Predictive pollution forecasting
- CI/CD pipeline deployment automation

---

## 👤 Author

**Nikhil Reddy**  
Aspiring Data Engineer  
Microsoft Fabric | KQL | Power BI | Real-Time Analytics  

---

## 📌 Summary

This project demonstrates how Microsoft Fabric can be used to build a scalable, real-time smart city monitoring system with automated ingestion, analytical intelligence, and executive-level visualization.

It combines engineering discipline with analytics storytelling.
