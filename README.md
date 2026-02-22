# 🌆 Smart City Real-Time Air Quality Monitoring System  
### Built using Microsoft Fabric | Eventstream | KQL | Power BI

---

## 📌 Project Overview

This project simulates a large-scale **Smart City IoT Air Quality Monitoring System** using Microsoft Fabric.

The system ingests real-time sensor data, performs time-series analytics using KQL, and provides both:

- ⚡ Operational Monitoring (Real-Time Dashboard)
- 📊 Executive Analytics (Power BI Report)

The objective is to demonstrate real-time ingestion architecture, time-series analytics, risk classification logic, and dashboard storytelling using Microsoft Fabric.

---

## 📊 Project Metrics

- 📡 Simulated **50,000+ IoT sensors**
- 📈 Processed **300,000+ sensor records**
- ⏱ Achieved **sub-2 minute ingestion latency**
- 🔄 Automated incremental ingestion using Fabric Data Pipeline
- 📊 1-minute time-series aggregation for live analytics
- 🚨 Real-time severe pollution detection (PM2.5 > 200)

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
- Simulated high-volume IoT data generation
- Incremental ingestion using KQL `.set-or-append`
- Automated pipeline scheduling
- Data freshness monitoring (Data Delay KPI)
- Duplicate-safe ingestion strategy

### 📈 Time-Series Analytics (KQL)
- 1-minute bin aggregation
- 2-hour rolling monitoring window
- Zone-level pollution comparison
- Risk classification using threshold logic
- Top 15 severe pollution event ranking

### 🚨 Intelligent Monitoring
- Risk Status indicator (SAFE / MODERATE / HIGH RISK / CRITICAL)
- Severe pollution alert table
- Peak PM2.5 tracking
- Executive KPI summary row

---

## 📊 Dashboards

### 🟢 Real-Time Operational Dashboard
Designed for control-room style monitoring.

Includes:
- Current Avg PM2.5
- Peak PM2.5
- Data Delay indicator
- Risk Status classification
- City-wide PM2.5 trend (2-hour live window)
- Zone pollution comparison
- Top severe pollution alerts

### 🔵 Power BI Executive Report
Designed for analytical and strategic insights.

Includes:
- Executive KPI cards
- PM2.5 trend visualization
- Zone performance comparison
- Pollution severity distribution
- Interactive filtering by zone

---

## 🧠 KQL Logic Highlights

Trend Analysis:

SensorEvents  
| where timestamp_utc > ago(2h)  
| summarize avg_pm25 = avg(pm25) by bin(timestamp_utc, 1m)  
| order by timestamp_utc asc  

Zone Risk Classification:

SensorEvents  
| summarize avg_pm25 = avg(pm25) by zone_name  
| extend risk_level =  
  case(  
   avg_pm25 > 200, "Severe",  
   avg_pm25 > 150, "High",  
   avg_pm25 > 100, "Moderate",  
   "Normal"  
  )  

Severe Pollution Alerts:

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

## 🎯 Engineering Concepts Demonstrated

- Real-time ingestion architecture
- Incremental data processing
- Time-series analytics using KQL
- Threshold-based risk classification
- Operational vs analytical dashboard design
- Monitoring ingestion latency and freshness
- Scalable Fabric-native solution design



## 👤 Author

**Nikhil Reddy**  
Aspiring Data Engineer  
Microsoft Fabric | KQL | Power BI | Real-Time Analytics  

---

## 📌 Summary

This project demonstrates how Microsoft Fabric can be used to design and implement a scalable real-time smart city monitoring system capable of processing hundreds of thousands of records with near real-time analytics and automated operational monitoring.

It combines data engineering architecture with analytical intelligence and dashboard storytelling.
