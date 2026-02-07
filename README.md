# rental-market-analyzer
An automated tool to scrape rental data from 591 rental websites in Taiwan and analyze market trends using the Google Sheets API.

- `scraper_basic_logic.ipynb`: A lightweight script for quick market data collection.
- `scraper_advanced_asset_tracking.ipynb`: A full-featured system with database simulation to track listing lifecycles and calculate days-on-market.
- `scraper_withGeo-Fencing_asset_tracking.ipynb`: This advanced version introduces **Geospatial Analysis** to the rental market scraper, allowing for precise identification of properties within a specific "living circle" rather than just administrative districts.

### 🌟 Key Features
* **Geo-Fencing & Distance Calculation**:
    * Integrates `geopy` to convert addresses into coordinates (Lat/Lon).
    * Calculates the linear distance (km) between each property and a target anchor point (e.g., University or workplace).
    * Enables filtering of properties that are geographically close but located across different district borders.
* **Centralized Configuration (Config-Driven)**:
    * All scraping parameters (City, Districts, Anchor Point, Google Sheet Names) are consolidated in a global `CONFIG` section for easy customization.
* **Smart Address Parsing**:
    * Implements a fallback mechanism to handle incomplete addresses (e.g., removing floor numbers to find coordinates based on road names).
* **Data Migration Tool**:
    * Includes a one-time migration script (`Cell 5`) to backfill coordinate and distance data for existing records in the database.

### 🛠️ How to Use
1.  Open the notebook in Google Colab.
2.  Modify the **Global Config** section in `Cell 3` to set your target city and anchor point.
3.  Run `Cell 5` once if you need to migrate old data.
4.  Run `Cell 4` to start the daily scraper.
