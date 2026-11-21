# 🚌 RTA Bus Fleet & Crowd Optimization Pipeline

An end-to-end machine learning, spatial forecasting, and dispatch optimization system built to predict passenger crowd surges (**"Red Nodes"**) across Dubai's Roads and Transport Authority (RTA) bus network and automate double-decker fleet allocation.

Developed during the **RTA Mobility & AI Hackathon**, this repository contains the complete **Dataiku DSS project export**—including visual recipes, saved ML models, Jupyter notebook analyses, experiment tracking logs, and interactive operational dashboards—paired with the companion **Mesh Map RTA Bus Ops** dispatcher web application.

---

## 📌 Problem Statement

Urban bus networks experience sharp, localized demand spikes driven by commuter rush hours, Dubai Metro feeder bottlenecks, and event-driven footfall. Static schedules struggle to adapt in real time, resulting in:
* **Severe Overcrowding ("Red Nodes"):** High-density stops exceeding vehicle capacity thresholds during peak windows.
* **Suboptimal Fleet Utilization:** Standard single-deck buses becoming overwhelmed on high-demand corridors while double-decker buses run under capacity on lower-load routes.

**Objective:** Forecast passenger boarding volumes at the stop and route level, flag critical congestion hotspots ahead of peak waves, and surface automated recommendations to deploy double-decker buses before bottlenecks form.

---

## 🏗️ System Architecture & Workflow

```text
┌─────────────────────────┐      ┌──────────────────────────────┐      ┌─────────────────────────┐
│   Historical RTA Data   │      │    Dataiku DSS Pipeline      │      │   Operational Outputs   │
│                         │      │                              │      │                         │
│ • Nol Card Tap-In/Out   │─────▶│ • Spatial-Temporal Joins     │─────▶│ • Dataiku Dashboards    │
│ • Bus Stop & Route GIS  │      │ • Red-Node Surge Forecasting │      │ • Saved ML Models       │
│ • Trip & Fleet Logs     │      │ • Double-Decker Optimization │      │ • Mesh Map Web App      │
└─────────────────────────┘      └──────────────────────────────┘      └─────────────────────────┘
```

---

## 📂 Repository Structure

This repository is the unzipped export of the Dataiku DSS project (`RTA_BUS_OPTIMISATION`):

```text
RTA-BUS-OPTIMISATION/
├── analysis-data/          # Visual analysis scripts, intermediate feature datasets & model evaluations
├── discussions/            # Project collaboration notes and annotations
├── experiment-tracking/    # MLflow / Dataiku experiment runs, hyperparameters & metric comparisons
├── notebook_results/       # Executed Jupyter notebooks for EDA, Red-Node forecasting & optimization
├── project_config/         # Dataiku Flow definitions, recipes, datasets, scenarios & dashboard configs
├── saved_models/           # Serialized trained ML models for crowd & Red-Node prediction
├── timelines/              # Project version history and build timeline logs
└── export-manifest.json    # Dataiku DSS project export metadata and dependency manifest
```

---

## ✨ Key Components

### 1. Dataiku DSS Flow & Feature Engineering (`project_config/` & `analysis-data/`)
* **Multi-Source Data Ingestion:** Combines historical RTA Nol card tap-in/tap-out transactions, bus stop coordinates, route geometries, trip logs, and fleet capacity records.
* **Spatiotemporal Feature Engineering:** Computes rolling passenger volume windows, lag demand features, scheduled vs. actual headway intervals, time-of-day/day-of-week cyclical encodings, and metro-transfer density scores.
* **Automated Dispatch Logic:** Evaluates predicted load factors against standard bus capacities to trigger double-decker bus reassignment rules.

### 2. Red-Node Forecasting Notebooks (`notebook_results/`)
Custom Python & Jupyter notebooks developed inside Dataiku for statistical analysis and surge modeling:
* **Red-Node Classification & Forecasting:** Identifies high-risk stops where projected passenger demand exceeds capacity thresholds, categorizing stops into severity tiers (Green / Amber / **Red Nodes**).
* **Corridor Spillover Analysis:** Traces upstream and downstream passenger accumulation along major arterial corridors and Dubai Metro feeder stations.
* **Fleet Reallocation Modeling:** Simulates single-decker to double-decker bus swaps to minimize overcrowding across peak commuter windows.

### 3. Saved Models & Experiment Tracking (`saved_models/` & `experiment-tracking/`)
* Compares tree-based ensemble models (XGBoost, LightGBM, Random Forest) and regression baselines across RMSE, MAE, and Red-Node precision/recall.
* Exports production-ready scoring pipelines inside `saved_models/` for batch and real-time inference.

### 4. Interactive Operational Dashboards (`project_config/dashboards/`)
Built directly within Dataiku DSS for transit planners and operations teams:
* **Geospatial Red-Node Heatmap:** Interactive map of Dubai bus stops highlighting predicted crowd surges by time window.
* **Route Capacity vs. Forecasted Demand:** Time-series breakdowns showing peak-hour capacity deficits and post-optimization load balancing.
* **Double-Decker Utilization Overview:** KPIs tracking fleet efficiency, reduced passenger wait times, and mitigated Red Nodes.

### 5. Companion Dispatcher Web App (`mesh-map-rta-bus-ops`)
An interactive frontend decision-support application built alongside this pipeline to visualize network topology and operational alerts:
* **Live Mesh Map Topology:** Interactive node-and-corridor visualization highlighting Red Nodes and feeder bottlenecks in real time.
* **Actionable Dispatch Queue:** Surfaces prioritized recommendations indicating which routes and departure slots require double-decker bus deployment.
* **Scenario Simulation:** Lets operators test fleet swaps and observe the projected reduction in stop-level congestion.

---

## 🚀 How to Import into Dataiku DSS

Because this repository contains the unzipped Dataiku export structure, you can re-import it directly into any **Dataiku DSS** instance:

1. **Zip the repository contents** (ensure `export-manifest.json` and the folders are at the root of the `.zip` archive, not nested inside an extra parent folder):
   ```bash
   git clone [https://github.com/zainab-arslan-dar/RTA-BUS-OPTIMISATION.git](https://github.com/zainab-arslan-dar/RTA-BUS-OPTIMISATION.git)
   cd RTA-BUS-OPTIMISATION
   zip -r RTA_BUS_OPTIMISATION.zip . -x "*.git*"
   ```
   *(On Windows PowerShell)*:
   ```powershell
   Compress-Archive -Path * -DestinationPath ..\RTA_BUS_OPTIMISATION.zip
   ```
2. Open **Dataiku DSS** and click **+ New Project > Import Project**.
3. Upload `RTA_BUS_OPTIMISATION.zip`.
4. Remap your input dataset connections (Filesystem / SQL) in **Project Settings > Connections** and run the **Flow** to reproduce all datasets, models, and dashboards.

---

## 🛠️ Tech Stack

* **Data Engineering, AutoML & Dashboards:** Dataiku DSS
* **Data Science & Forecasting:** Python, Pandas, NumPy, Scikit-Learn, XGBoost / LightGBM, Jupyter Notebooks
* **Web Application:** Mesh Map RTA Bus Ops (React / TypeScript / Python)

---

## 👤 Author

**Zainab Arslan Dar**  
*Cybersecurity & Digital Forensics*  
[GitHub](https://github.com/zainab-arslan-dar)
