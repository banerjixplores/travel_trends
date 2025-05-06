# 🌍 Travel Trends 

> "Great journeys begin with insight – knowing who travels, where, how, and why is the map to every business decision."

---

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)


## 📌 Project Objective

This project delivers a multi-layered analytical view of global travel behavior. By integrating traveler, fuel, and weather data, we uncover **demographic, geographic, and economic factors** that shape trip duration, transport/accommodation preferences, and travel cost dynamics.

Our final deliverable is an **interactive Power BI dashboard** supported by **statistical validation in Python**.

### Intended Users
- **Travel Intelligence Analysts** – to better understand traveler profiles and preferences.
- **Transport Providers** – to optimize service offerings based on user demand and cost patterns.

---

## 📁 Dataset Summary

| Dataset             | Source   | Description                                                                 |
|---------------------|----------|-----------------------------------------------------------------------------|
| Traveler Trip Data  | Kaggle   | Destination, duration, nationality, transport, accommodation type & cost   |
| Global Weather      | Kaggle   | Monthly temperature per country                                             |
| Fuel Prices         | U.S. EIA | Monthly average fuel prices in the U.S. (2019–2025)                         |

---

## 🔍 Core Questions

1. Which destinations are most popular across age, gender, and nationality?
2. How does trip duration vary with age or gender?
3. Are accommodation and transport preferences linked to demographics?
4. How have transportation costs evolved, and how are they affected by fuel price and climate?
5. Which regions or cities show the strongest travel demand?
6. Can we categorize travel behaviors into actionable segments for agencies?

---

## ✅ Hypotheses

| ID | Hypothesis |
|----|------------|
| H1 | Gender significantly influences destination preference |
| H2 | Age group affects trip duration |
| H4 | Age group has a significant correlation with accommodation cost |
| H5 | Age group is associated with destination preference |
| H6 | Age group influences accommodation type |
| H7 | Transportation cost is significantly affected by fuel price |
| H8 | Temperature correlates with fuel pricing |
| H9 | War (2022) and COVID (2019–22) impacted fuel pricing |

> **Note:** Hypothesis on nationality vs destination was excluded due to low sample size.

---

## 🛠️ Tools & Technologies Used

- **Python**: pandas, seaborn, pingouin, matplotlib
- **Power BI**: Dashboard creation and interactivity
- **Jupyter Notebooks**: For analysis and documentation
- **GitHub**: Version control and collaboration

---

## 📊 Dashboard Structure (Power BI)

### Page 1: Travel Overview
- **KPI Cards**: Total trips, average duration, top destinations
- **Bar Chart**: Most visited countries
- **Thematic Map**: Destination map sized by traveler count
- **Donut Chart**: Transport type usage by gender
- **Slicers**: Age, Gender, Nationality

### Page 2: Trip Duration & Demographics
- **Boxplots**: Trip duration by age group
- **Histograms**: Duration distribution by gender
- **Line Charts**: Duration vs age trends

### Page 3: Accommodation & Transportation
- **Stacked Bars**: Accommodation type vs age group
- **Bubble Chart**: Age vs Accommodation Cost vs Gender
- **Pie Charts**: Transport type breakdown

### Page 4: Fuel Cost & Climate Analysis
- **Line Chart**: Monthly fuel price trend
- **Bar Chart**: Cost comparison 2019–2025
- **Scatter Plot**: Fuel price vs avg temperature by country
- **Heatmaps**: Correlation matrix

---

## 🧪 Statistical Hypotheses Testing

- **Chi-Square**: Gender vs destination; age group vs accommodation type
- **Correlation Matrix**: Accommodation cost vs transport cost, age, and fuel price

Plots generated using Python and imported into Power BI as images or tooltips.

---

## 🧾 Project Phases

### Day 1: Ideation, ETL, and Planning
- Dataset loading, cleaning, removing nulls
- Feature engineering: trip duration, age group, city-country lookup
- Integration with weather and fuel datasets
- Kanban setup + README draft + wireframe planning

### Day 2: EDA + Hypothesis Testing + Dashboard Building
- Data validation and model relationships
- Visualization in Power BI (grouped, stacked, map, matrix, slicers)
- Python stats testing and import of visual results

### Day 3: Final Touches + Presentation
- Dashboard formatting and interactivity
- Markdown polishing and GitHub push
- Final review + team demo walk-through

---

## 📂 Project Structure

project-root/
│
├── data/raw/ # Raw data files (CSV, XLS, etc.)
│ ├── Travel details dataset.csv
│ ├── GlobalWeatherRepository.csv
│ └── fuel_price.xls
│
├── data/procesed/ # Cleaned and processed datasets
│ ├── cleaned_travel.csv
│ ├── merged_weather.csv
│ └── enriched_travel.csv
│
├── notebooks/ # Jupyter notebooks for analysis
│ ├── Hackathon_Travel_Dataset.ipynb
│ ├── Weather_Data.ipynb
│ └── Fuel_Price.ipynb
│
├── dashboard/ # Power BI dashboard files
│ └── Travel_Dashboard.pbix
│
├── images/ # Static images for README/docs
│ └── hypothesis_visuals.png
│
├── README.md # Project overview and documentation
└── .gitignore # Git ignore file

---

## 🔮 Future Improvements (Backlog)

- Predictive analytics for cost estimation
- Time series model on fuel price fluctuation
- Real-time climate API integration
- Interactive bundling recommendation engine

---

## 🤝 Team Roles

| Role           | Key Tasks                                      |
----------------|------------------------------------------------|
| Data Architect | Feature engineering, Power BI integration      |
| Data Analyst   | Visuals, storytelling, statistical plots        |
| Project Manager| Kanban, retrospectives, GitHub coordination    |

---

## 📚 References

- [Traveler Trip Dataset – Kaggle](https://www.kaggle.com/datasets/rkiattisak/traveler-trip-data)
- [Global Weather Repository – Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository)
- [U.S. Fuel Prices – EIA](https://www.eia.gov/petroleum/gasdiesel/)

## Acknowledgements (optional)
* Thank the people who provided support through this project.