# Maritime Vessel Route Simulation & AIS Data Engineering

This project simulates realistic vessel movements between global ports, generates AIS (Automatic Identification System) messages, streams them via WebSocket, stores them in a database, and performs downstream analytics and dashboard visualizations. 
---

## What This Project Does

This project replicates an end-to-end maritime data pipeline by:
- Simulating vessel movements between major ports
- Generating standard-compliant AIS messages for each vessel
- Streaming these messages as if in a live maritime network
- Storing and validating this data in a local database
- Performing analytics and producing insightful dashboards

---

## Why This Project Is Useful

- Mimics real-world maritime data handling with realistic routing and streaming
- Demonstrates ability to process geospatial and time-series data
- Highlights practical use of Python libraries for data engineering
- Can be extended to anomaly detection, tracking, and monitoring

---

## Getting Started

1. Clone the repository
2. Install dependencies:
   ```bash
   pip install pandas plotly geopy pyais matplotlib searoute
   ```
3. Run notebooks in order: 1 → 2 → 3 → 4 → 5
4. Ensure the file `UpdatedPub150.csv` is present in your working directory

---

## Getting Help

If you are reviewing this for the Blurgs AI assignment and need clarification on any implementation detail or deviation from the original instructions, please refer to the **Design Decisions & Justifications** section below. I have explained all choices and trade-offs made.

If you're a fellow developer trying this project, feel free to open an issue or message me directly.

---

## Who Maintains This Project

This project is individually developed and maintained by:

Divya M – Data enthusiast passionate about solving real-world problems with clean and practical data engineering workflows.

---

## Key Features

- Generates vessel routes using real-world port data
- Assigns unique speeds to each vessel
- Encodes AIS messages using the AIVDM standard
- Streams messages via a WebSocket server
- Stores parsed AIS messages in SQLite with validation
- Supports querying and visual analytics for distance, speed, and trajectories
- Interactive dashboards using Matplotlib and Plotly

---

## Project Flow

1. **Route Simulation** (Notebook 1)  
   → Generate coordinates for vessel paths using searoute

2. **AIS Message Encoding** (Notebook 2)  
   → Encode vessel tracks into AIS AIVDM payloads using `pyais`

3. **WebSocket Streaming + Storage** (Notebook 3)  
   → Stream AIS messages and store them in a normalized SQLite database

4. **Client Analysis** (Notebook 4)  
   → Query and analyze vessel behavior using pandas & geopy

5. **Dashboards** (Notebook 5)  
   → Visualize vessel speed, routes, and distance metrics

---

## Notebooks Overview

| Notebook                             | Purpose |
|-------------------------------------|---------|
| `01_Vessel_Route_Simulation.ipynb`  | Generate route & speed data for vessels |
| `02_AIS_Message_Generation.ipynb`   | Encode AIS messages with real speed |
| `03_WebSocket_Server_Store.ipynb`   | Stream + store AIS messages in DB |
| `04_Client_Receiver_Analytics.ipynb`| Analyze distance, speed, and query DB |
| `05_Dashboards.ipynb`               | Visual plots of vessel movement |

---

## Tech Stack

- Python (Pandas, Plotly, SQLite, Geopy, PyAIS)
- Jupyter Notebooks
- WebSockets
- GIS: searoute, GeoJSON, geodesic calculations

---

## Sample Output

### Query Timing & Unit Test Validation
- Query timing for each vessel was under 0.05 seconds
- All unit tests passed: latitude, longitude, and timestamp values are valid and non-null

### Sample AIS Messages (Encoded)
- Encoded in AIVDM format using PyAIS
- Sample:
  ```json
  {
    "message": "AIVDM",
    "mmsi": 123456789,
    "timestamp": "2025-04-30T09:38:40.869824+00:00Z",
    "payload": "!AIVDO,1,1,,A,11mg=5OP2l8ecW`AUM33Q2l1P000,0*69"
  }
  ```

### Visualizations
- Speed Over Time per vessel
- Global route maps (points & connected routes)
- Distance travelled and average speed bar plots per vessel

---

## Design Decisions & Justifications

### Why SQLite?
- Lightweight, serverless, and requires no setup.
- Ideal for local simulations and reproducibility.
- Allows indexing (`mmsi`, `timestamp`) for fast querying.

### Why Searoute?
- Searoute is an independent Python library specifically built to calculate realistic sea routes between ports.
- It generates realistic vessel paths along actual sea lanes using maritime geography.
- Produces GeoJSON-compatible output for mapping.
- Better than straight-line interpolation or manually defined paths.

### Why WebSockets?
- Mimics real-time AIS streaming as seen in maritime monitoring.
- Enables live ingestion and processing of simulated AIS messages.

### Why PyAIS?
- Encodes messages into industry-standard AIVDM format.
- Reduces the need for custom parsing or manual message crafting.

### Why Pandas & Plotly?
- Pandas simplifies time-series and geospatial data processing.
- Plotly enables rich, interactive, and animated visualizations.
- Matplotlib supports quick, static views for trends.

### Why Not PostgreSQL/PostGIS?
- SQLite offered simplicity, zero config, and portability.
- Suitable for offline, take-home evaluation settings.

---

## Future Improvements

- Real-time WebSocket receiver (instead of batch simulation)
- Live dashboard with Dash or Streamlit
- Store AIS data in PostgreSQL/PostGIS with geospatial indexing
- Add error injection, anomaly detection, and alerting
