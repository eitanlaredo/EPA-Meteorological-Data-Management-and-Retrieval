# Easy EPA

A command-line tool for retrieving, managing, and analyzing meteorological data from the U.S. Environmental Protection Agency.

## Overview

Easy EPA scrapes the [EPA Air Quality System](https://aqs.epa.gov/aqsweb/airdata/download_files.html) to download environmental datasets, then provides summaries, plots, and state-by-state comparisons through an interactive menu. Supports data going back to 1980.

## Features

- **Daily Summaries** — Temperature, Wind, and AQI for any date and state
- **Yearly Summaries** — Aggregate Temperature or AQI statistics by state and year
- **Plotting** — Yearly trend plots for Temperature, AQI, and EPA criteria pollutant gases (Ozone, SO2, NO2, CO)
- **State Comparisons** — Side-by-side plots comparing states for a given year
- **File Management** — Download and cache EPA datasets locally as CSVs

## Variables Supported

| Variable | Period |
|----------|--------|
| Temperature | Daily |
| Air Quality Index (AQI) | Daily |
| Wind | Daily |
| Ozone | Daily |
| SO2 | Daily |
| NO2 | Daily |
| CO | Daily |

## Project Structure

```
├── Easy_EPA.py            # Main CLI — menu-driven user interface
├── backend_functions.py   # Data analysis, summaries, and plotting (Pandas, Matplotlib)
├── epa_webscraper.py      # Scrapes EPA website for downloadable dataset URLs
├── url_storage.py         # Manages URL index, downloads, and extracts zip → CSV
├── input_validation.py    # Validates user inputs (dates, years, states)
├── test_functions.ipynb   # Jupyter notebook with function tests and demonstrations
└── csv_folder/            # Auto-generated local cache of downloaded CSVs
```

## How It Works

1. `epa_webscraper.py` parses the EPA downloads page using BeautifulSoup, extracting all available `.zip` file URLs into a local index
2. `url_storage.py` maps those URLs to metadata (variable, year, period) and handles downloading/extracting into `csv_folder/`
3. `backend_functions.py` reads the CSVs with Pandas and produces summaries and Matplotlib plots
4. `Easy_EPA.py` ties it all together with a menu interface that guides the user through variable, year, and state selection

## Usage

```bash
python Easy_EPA.py
```

The menu will prompt you to select an action:

- **D** — Daily summary (Temperature, Wind, AQI) for a specific date and state
- **Y** — Yearly summary for Temperature or AQI by state
- **P** — Plot Temperature, AQI, or criteria gases for a state and year
- **C** — Compare states via plot
- **S** — Download a specific dataset to `csv_folder/`
- **Q** — Quit

## Tools & Libraries

- **Pandas** — data manipulation and aggregation
- **Matplotlib** — visualization
- **BeautifulSoup** — web scraping
- **Requests** — HTTP requests with retry logic

## Example Output

```
The AQI in Texas in 2022 was recorded for 45 Texas counties, and a total of
365 days were recorded. The average AQI was 40.6 and the maximum recorded
AQI was 194.0. (AQI's over 100 are considered unhealthy for sensitive groups.)
```
