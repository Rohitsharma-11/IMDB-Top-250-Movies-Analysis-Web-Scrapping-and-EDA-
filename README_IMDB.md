# 🎬 IMDb Top 250 — Web Scraping, Data Cleaning & EDA

## 🧠 Project by: Rohit Sharma

---

## 📌 Project Description

This project scrapes the **IMDb Top 250 Movies** and performs **data cleaning** and **exploratory data analysis (EDA)** to uncover patterns across ratings, genres, runtimes, release years, and directors.  
The scraping workflow handles **pagination** and **dynamic content** using **Beautiful Soup** and **Selenium**. Visualizations produced during EDA are available in this repository.

**Source:** [IMDb Top 250](https://www.imdb.com/chart/top/)

---

## 🎯 Problem Statement

Movie recommendation and catalog systems benefit from clean, reliable metadata. The aim of this project is to:
- **Programmatically collect** the Top 250 movie metadata from IMDb.
- **Clean and standardize** the dataset for analysis.
- **Explore** genre trends, ratings distribution, decade-wise patterns, and key contributors.
- **Surface insights** that help understand what defines a top-rated film.

---

## 📖 Table of Contents

1. [Project Overview](#project-overview)  
2. [Tech Stack](#tech-stack)  
3. [How to Run](#how-to-run)  
4. [Data Understanding](#data-understanding)  
5. [Data Cleaning](#data-cleaning)  
6. [Exploratory Data Analysis (EDA)](#eda)  
7. [Insights Derived](#insights-derived)  
8. [Challenges Faced](#challenges-faced)  
9. [Future Scope](#future-scope)  
10. [Final Outcome](#final-outcome)  
11. [Project Credits](#project-credits)

---

## 🧩 Project Overview

We collected and analyzed metadata for the **Top 250 movies on IMDb**, focusing on:
- Year-wise and decade-wise release trends
- IMDb rating distribution and outliers
- Popular genres and multi-genre combinations
- Runtime distribution and its link to ratings
- Directors and countries that frequently appear in the Top 250

---

## 🛠️ Tech Stack

- **Python**: `requests`, `BeautifulSoup`, `Selenium`, `pandas`, `numpy`
- **Automation/Drivers**: Selenium WebDriver (e.g., ChromeDriver)
- **Visualization**: `matplotlib`, `seaborn`  
- **Environment**: Jupyter/Notebook or Python scripts

---

## ▶️ How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/Rohitsharma-11/IMDB-Top-250-Movies-Analysis-Web-Scrapping-and-EDA.git
   cd IMDB-Top-250-Movies-Analysis-Web-Scrapping-and-EDA
   ```

2. **Create & activate a virtual environment (recommended)**
   ```bash
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # macOS/Linux
   source .venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the scraper (Selenium-based for dynamic content)**
   ```bash
   python src/scrape_imdb_top250_selenium.py
   ```

5. **Run the BeautifulSoup (static) fallback (if needed)**
   ```bash
   python src/scrape_imdb_top250_bs4.py
   ```

6. **Open the EDA notebook**
   ```bash
   jupyter notebook notebooks/EDA_IMDb_Top250.ipynb
   ```

> **Note:** Make sure the appropriate **WebDriver** (e.g., ChromeDriver) is installed and on your PATH. For dynamic panels (like genres) and infinite/paginated sections, Selenium is used to render and interact with the page.

---

## 🧾 Data Understanding

Typical fields collected (subject to page structure):
- `title`, `year`, `rating`, `rank`
- `genre` (single or multiple)
- `duration` (runtime in minutes)
- `director`, `cast_top`
- `votes`, `metascore` (if available)
- `certificate` / `content_rating` (if available)
- `url` (movie page)

Raw data is saved to: `data/raw/imdb_top250_raw.csv`  
Cleaned data is saved to: `data/processed/imdb_top250_clean.csv`

---

## 🧼 Data Cleaning

- **Column standardization**: consistent names, types, and ordering
- **Type casting**: `year` → int, `rating` → float, `duration` → int, `votes` → int
- **Parsing**: split multi-genre strings into lists; extract numeric fields
- **Duplicates & nulls**: drop duplicates, fill or drop nulls where appropriate
- **Derived columns**:
  - `decade` (e.g., 1990s, 2000s)
  - `primary_genre` (first listed genre)
  - `title_clean` (stripped/pattern-cleaned title)

---

## 📊 EDA

Visualizations are available in the repository (see the **Images** or **Plots** folder, or the EDA notebook). Common analyses include:

### ⭐ Rating Distribution
- Histogram/KDE of IMDb ratings across the Top 250.

### 🎭 Genre Landscape
- Top genres and frequent multi-genre combinations.
- Share of movies by primary genre.

### ⏱️ Runtime Patterns
- Distribution of runtimes; long vs short movies in the Top 250.

### 🗓️ Decade Trends
- Count of movies per decade; golden eras of cinema.

### 🎬 Directors & Contributors
- Most frequent directors in the list.
- Average rating by director (min movie count threshold).

### 🌍 Country/Language (if scraped)
- Distribution by production country/language (where available).

> **Note:** Plots are exported from the EDA notebook to the repository. Check the `Images/` or `Plots/` directory.

---

## 📍 Insights Derived

1. **Ratings Cluster at the Top End**  
   Top 250 ratings tend to cluster above ~8.0, with a few outliers near 9.0+.

2. **Genre Concentration**  
   Drama and Crime often dominate, with frequent combinations like **Drama–Crime**, **Drama–Thriller**, and **Drama–Romance**.

3. **Era Effects**  
   Certain decades (e.g., 1990s–2000s) show dense representation, hinting at strong cinematic output.

4. **Runtime Sweet Spot**  
   Many top films cluster between **120–150 minutes**; extremes exist but are less common.

5. **Director Footprints**  
   A handful of directors appear repeatedly; their averages typically remain high even with a higher film count.

*(Your specific insights may vary based on the scrape and cleaning rules applied.)*

---

## ⚠️ Challenges Faced

- **Pagination & partial listing**: Initial attempts only returned the first 25 titles; addressed by identifying page/offset parameters or iterating over dynamic loads.
- **Dynamic content for genres & details**: Some attributes revealed only after interactions (e.g., expanding a panel). **Selenium** was used to render and interact with these elements.
- **Anti-bot/403 issues**: Added appropriate headers, delays, and error-handling; switched to Selenium where necessary.
- **HTML structure changes**: Wrote resilient selectors (CSS/XPath) and fallback logic.

---

## 🚀 Future Scope

- Build a **dashboard** (e.g., Streamlit) to explore Top 250 interactively.  
- Add **time-series refresh** to track list changes over time.  
- Enrich with **external metadata** (awards, box office, countries).  
- Train **recommendation or clustering models** using embeddings of plot/genre metadata.

---

## ✅ Final Outcome

A reliable pipeline that:
- Scrapes Top 250 metadata (handling dynamic content and pagination)  
- Produces a clean, analysis-ready dataset  
- Generates visualizations that explain trends across genres, ratings, decades, and runtimes

---

## 👏 Project Credits

- **Author:** Rohit Sharma  
- **Tech:** Beautiful Soup, Selenium, pandas, matplotlib, seaborn, requests

> Visualizations and notebooks are available in this repository. If you find this useful, consider ⭐ starring the repo!
