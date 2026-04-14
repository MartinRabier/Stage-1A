# Geolocation & Prospect Scoring Project 📍

This repository contains the work completed during my first-year engineering internship. The project focuses on building a geospatial intelligence pipeline to map competitors and developing an interactive interface for prospect data collection and scoring.

## 📋 Project Overview

The project is divided into three main pillars:
1.  **Competitor Mapping (Staffing Industry):** Identifying and geolocating competitor agencies and "Onsite" locations across France.
2.  **Market Analysis:** Segmenting data by region, employment zones, and NAF codes to evaluate business density.
3.  **Data Entry Interface (Streamlit):** A specialized app for operational teams to input prospect data directly into the Snowflake data warehouse for scoring.

## 🛠️ Tech Stack

* **Database:** Snowflake (Cloud Data Platform).
* **Languages:** SQL (Snowflake Dialect), Python.
* **Web Framework:** Streamlit.
* **Python Libraries:** Pandas, Snowpark, Datetime.

## 📂 Repository Structure

### 1. Data Engineering & ETL (SQL)
The SQL scripts transform raw INSEE and internal MDM data into business-ready views:
* **Competitor Discovery:** Filters and geolocates temporary staffing agencies (NAF Code `78.20Z`) in specific French regions.
* **Onsite Detection Logic:** An algorithm designed to identify "Onsite" agencies by detecting addresses where two distinct SIRETs coexist: a staffing provider and a client.
* **Manpower vs. Market:** Consolidation of internal agency data (Manpower) and "MOS" (Management On Site) against the wider competitive landscape.

### 2. Streamlit Application (`app_streamlit.py`)
A Python-based interface designed to bridge the gap between operational input and data scoring:
* **Dynamic Forms:** Allows users to input SIRET, job categories (via reference tables), turnover rates, hourly rates, and parking availability.
* **Real-time Injection:** Uses Snowpark to insert validated data directly into the `TEST_STREAMLIT_PROSPECT` table within Snowflake, including timestamps.

### 3. Statistical Analysis
* **Market Segmentation:** Scripts utilizing `ROLLUP` functions to generate hierarchical statistics by Region (REG), Employment Zone (ZE), and Activity Sector (NAF/NES39).

## 🚀 How to Run

### Prerequisites
* A Snowflake account with access to the `FR_DISCOVERY` database.
* Python 3.8+ installed.

### Installation & Launch
1.  Install dependencies:
    ```bash
    pip install streamlit pandas snowflake-snowpark-python
    ```
2.  Run the application:
    ```bash
    streamlit run app_streamlit.py
    ```

---
**Note:** *This project was developed within a secure corporate data environment. References to specific databases (e.g., `FR_DISCOVERY.LANDING`) are part of the internal data architecture of the host company.*
