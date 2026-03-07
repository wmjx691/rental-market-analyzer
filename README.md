# rental-market-analyzer
An automated tool to scrape rental data from 591 rental websites in Taiwan and analyze market trends using the Google Sheets API.

- `scraper_basic_logic.ipynb`: A lightweight script for quick market data collection.
- `scraper_advanced_asset_tracking.ipynb`: A full-featured system with database simulation to track listing lifecycles and calculate days-on-market.
- `scraper_withGeo-Fencing_asset_tracking.ipynb`: This advanced version introduces Geospatial Analysis to the rental market scraper, allowing for precise identification of properties within a specific "living circle" rather than just administrative districts. **It also features a robust, anti-scraping, two-stage architecture for high-volume data extraction.**

### 🌟 Key Features
* **Two-Stage Robust Architecture**:
    * Decouples the pipeline into "Dynamic DOM Scraping" (Phase 1) and "Data Cleansing & Geo-computation" (Phase 2). This prevents data loss if API rate limits or network issues interrupt the process.
* **Anti-Scraping & Infinite Scrolling**:
    * Bypasses the 591 website's 170-item display limit and fake pagination using simulated keyboard scrolling (`Keys.END`) and a unique ID memory pool.
* **Multi-Type Polling Automation**:
    * Automatically cycles through different property types (e.g., entire apartments, independent studios) in a single run and merges the results.
* **Geo-Fencing & Distance Calculation**:
    * Integrates `geopy` to convert addresses into coordinates (Lat/Lon).
    * Calculates the linear distance (km) between each property and a target anchor point (e.g., University or workplace).
    * **Dynamic Filtering**: Automatically excludes properties that exceed the defined `MAX_DISTANCE_KM` threshold.
* **Verbose Terminal Monitor**:
    * Implements an in-place refreshing progress monitor using IPython's `clear_output` to track real-time API call status and distance filtering without cluttering the console.
* **Centralized Configuration (Config-Driven)**:
    * All scraping parameters (City, Districts, Anchor Point, Google Sheet Names) are consolidated in a global `CONFIG` section for easy customization.
* **Smart Address Parsing**:
    * Implements a fallback mechanism to handle incomplete addresses (e.g., removing floor numbers to find coordinates based on road names).

### 🛠️ How to Use
1.  Open the notebook in Google Colab.
2.  Modify the **Global Config** section in `Cell 3` to set your target city, anchor point, limits, and API configurations.
3.  Run `Cell 4-1` to execute Phase 1 (Web Scraping) and collect raw data into memory.
4.  Run `Cell 4-2` to execute Phase 2 (Data Processing), which calculates distances, applies geo-fencing filters, and saves the final dataset to Google Sheets.
5.  (Optional) Run `Cell 5` if you need to execute a one-time migration script to backfill coordinate data for existing legacy records.

