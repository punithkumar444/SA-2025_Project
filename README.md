# 🅿️ Smart Dynamic Parking Price Optimization System

## 📖 Introduction

This project proposes a **Smart Dynamic Parking Pricing System**, focusing on the analytical models and simulations required to dynamically calculate optimal prices, simulate user behavior, and explore rerouting strategies when lots are full. The goal is to lay the groundwork for creating a fair, efficient, and intelligent parking environment.
---

## 🎯 Objectives

* Design **three adaptive pricing models**: baseline linear, demand-weighted, and geo-competitive.
* Simulate **real-time price adjustments** as demand changes over time.
* Implement **rerouting logic** to redirect vehicles from full lots to nearby alternatives.
* Provide a **Streamlit dashboard** to visualize price changes and simulate the system interactively.
* Enable smarter city-level parking distribution using data-centric logic.

---

## 🛠️ Tech Stack Used

* **Python**
* **Plotly** (Interactive visualizations)
* **Pandas** (Data manipulation)
* **NumPy** (Numerical computations)

---


## 📁 Dataset Overview

The dataset simulates parking sensor data and includes the following features:

* **Lot ID**: Unique identifier for each parking location.
* **Capacity**: Maximum number of vehicles that can be parked.
* **Occupancy**: Real-time count of currently parked vehicles.
* **Queue Length**: Vehicles waiting for a spot.
* **Vehicle Type**: Categorical feature (car, bike, van, etc.)
* **Traffic Conditions Nearby**: Encoded value representing congestion near the lot.
* **Special Day Flag**: Boolean for holidays/weekends.
* **Timestamp**: Combined date and time for streaming simulation.
* **Latitude & Longitude**: Coordinates used for geospatial distance calculations (Model 3).

This dataset serves as input for real-time dynamic pricing models and rerouting logic.

---

## 🧹 Data Preprocessing & Feature Engineering

Several steps were applied to prepare the data for dynamic modeling:

* **Datetime Indexing**: Combined `Date` and `Time` into a unified `Timestamp` for simulation streaming.
* **Occupancy Rate Calculation**: Normalized as `occupancy / capacity` for pricing logic.
* **Queue Normalization**: Scaled values for compatibility across lots.
* **Traffic & Special Day Encoding**: Converted categorical inputs to numerical weights.
* **Vehicle Demand Weighting**: Assigned demand stress factors to vehicle types.
* **Geospatial Distance Matrix**: Calculated between all lots using the Haversine formula for rerouting logic.

---

## 🧠 Pricing Models

The project implements three progressively intelligent models, each adding complexity and realism.

---

### 🔹 Model 1: Linear Pricing Based on Occupancy

**Principle**: Price is linearly adjusted based on how full the lot is.

* Price increases proportionally to occupancy rate.
* Simple and interpretable.
* Useful as a baseline.

**Formula**:
`price = base_price + α × (occupancy / capacity)`

**Limitations**:

* Ignores traffic, queue length, and other environmental factors.
* Cannot adapt to special days or vehicle types.

---

### 🔹 Model 2: Multi-Factor Demand-Based Pricing

**Principle**: Prices reflect a composite demand score calculated from multiple real-world factors.

**Demand Score Includes**:

* Occupancy Rate
* Normalized Queue Length
* Traffic Congestion Level
* Special Day Flag (higher base demand)
* Vehicle Type (larger vehicles = higher price impact)

**Formula**:
`price = base_price + α × demand_score`
(*Where demand\_score is a weighted sum of the above factors*)

**Strengths**:

* More adaptive and robust.
* Reflects real-world scenarios better than Model 1.

---

### 🔹 Model 3: Geo-Competitive Pricing with Rerouting

**Principle**: Lots adjust pricing based on surrounding lot conditions and reroute users if full.

**Key Features**:

* **Competitive Pricing**: If a nearby lot (within 1 km) has better availability and lower price, current lot may decrease its price.
* **Rerouting Logic**: When a lot is over 90% full, reroute to the nearest underutilized lot.
* **Proximity Analysis**: Geospatial calculations find nearest alternatives in real time.

**Outcome**:

* Optimizes usage across the network, not just individual lots.
* Prevents overcrowding and improves city-wide traffic flow.

---

## 📌 Key Results & Insights

* **Model 2** yields smoother, more reasonable pricing by factoring multiple variables.
* **Model 3** is the most realistic, showing how rerouting eases pressure on congested lots.
* **Dynamic pricing helps flatten the demand curve**, encouraging use of underutilized lots.
* **Queue-based pricing** prevents excessive waiting time and spreads traffic more evenly.

---


### Architectural Diagaram Explanation:

1. **Real-Time Data Sources:** Data streams from parking sensors, traffic conditions, and queue lengths feed into the system continuously.
2. **Data Preprocessing & Feature Engineering:** Raw data is cleaned, normalized, timestamped, and enriched (e.g., distance matrices) for the pricing models.
3. **Pricing Models:** Three models (linear, demand-based, geo-competitive) compute dynamic prices based on the preprocessed data.
4. **Rerouting Logic:** Geo-competitive pricing adjusts prices and reroutes vehicles to less congested lots.
5. **Streamlit Dashboard:** Offers a user interface for visualizing price changes, simulating demand, and interacting with the system.
6. **User Interaction:** Stakeholders adjust parameters and observe system behavior live.

---


## 🔮 Future Work

* Integrate **live traffic APIs** (e.g., Google Maps) for real-time congestion updates.
* Build a **driver-facing mobile app** that displays optimal nearby parking with live prices.
* Deploy the app publicly using **Streamlit Cloud or AWS Lambda**.

---

## 🌟 Acknowledgements

This project was developed as part of Summer Analytics Course 2025 Academic Work at **Indian Institute of Technology (IIT) Guwahati**.

Special thanks to:
* **Plotly & Bokeh** – for powerful interactive plotting.
