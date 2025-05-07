# 🌍 Travel Trends 

> "Great journeys begin with insight – knowing who travels, where, how, and why is the map to every business decision."

---

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)


## 📌 Project Objective

This project delivers a **multi-layered analytical view** of global travel behavior. By integrating traveler, fuel, and weather data, we uncover **demographic, geographic, and economic factors** that shape trip duration, transport/accommodation preferences, and travel cost dynamics.

The final product includes:

- A Power BI dashboard showing dynamic insights for two main stakeholders.

- A statistical validation notebook in Python with advanced plots and hypothesis testing.

### 👥 Intended Users
- **Travel Intelligence Analysts** – Identify patterns in travel behavior and segments for optimized planning and offers.
- **Transport Providers** – Align pricing and service delivery with travel and fuel trends.

---

## 📁 Dataset Summary

| Dataset             | Source   | Description                                                   |
| ------------------- | -------- | ------------------------------------------------------------- |
| Travel Trip Dataset | Kaggle   | Traveler demographics, destinations, costs, modes of travel   |
| Global Weather Repo | Kaggle   | Monthly average temperatures per country                      |
| Fuel Price (Excel)  | U.S. EIA | Monthly fuel price index for U.S. (2019–2025)                 |
| Temperature Summary | Derived  | Cleaned CSV of monthly average temperatures mapped by country |

---

## ❓ Core Questions

1. **Destination Preferences**
Which destinations are most preferred overall and by demographic groups (age, gender, nationality)?  
How do travel preferences differ by nationality — which nationalities prefer which destination?  
Which destinations contribute the most to traveler counts?  

 2. **Spending Behavior**
Which age group of which nationality spends the most on travel?  
Which age groups and genders spend more on travel and accommodation?  
How does accommodation cost vary across different demographic segments?  

3. **Accommodation Preferences**
How do accommodation types differ by age group and gender?  
Are certain age groups more likely to choose luxury or economy options?  


4. **Trip Duration Patterns**
What is the typical trip duration, and how does it vary by age group or gender?  
Do older or younger travelers tend to take longer vacations?


5. **Travel Trends over Time**
Which years recorded the most travel activity (number of trips)?  
Are there noticeable demographic trends across years?

6. **Transporation Preferences**
Which transportation modes are most commonly used?  
How does transport vary by Age group, gender and nationality?  
Do certain cities or regions show a stronger preference for specific transport types ( train vs air travel, for example?)  
Association between trip duration and transport type?

---

## 🔧 ETL Process

✅ Initial Cleaning & Preprocessing (Pandas)
Removed personal identifiers (name, ID)

Generated derived features:

TripDuration = EndDate - StartDate

Age_Group (Young Adult, Youth, etc.)

Handled missing values: dropped rows with null accommodation/transport costs

Merged temperature and fuel price data using:

Destination country ↔ Average temperature

Year-Month ↔ Fuel price

---

## 🏷️ Feature Engineering

🔹 Mapping Functions (Custom Pandas Functions)
Destination → Country: Cleaned inconsistent city-country formats

Country → Climate Zone: Based on avg. temperature

Nationality Normalization: Mapped similar variants into a single label

Cost Buckets:

Accommodation and transportation costs categorized into 7 levels (Very cheap → Very expensive)

### 🔹 Rare Label Encoding (Custom)

We implemented custom encoding to group rare categorical values into "Rare":

```def rare_label_encoder(df, column, threshold=0.05):
    freq = df[column].value_counts(normalize=True)
    rare_labels = freq[freq < threshold].index
    df[column] = df[column].apply(lambda x: "Rare" if x in rare_labels else x)
    return df
```

### 🔹 Ordinal Encoding (Custom Pandas Approach)

Manually encoded categories with custom-defined ranks (e.g., cost buckets, climate):

```ordinal_mappings = {
  'Accommodation cost category': {'Very cheap': 0, ..., 'Very expensive': 7},
  ...
}
```
---

## 🧠 Feature Encoding Strategy
We opted for custom pandas-based encoders instead of external libraries due to:

✅ Compatibility: category_encoders showed issues with Python 3.12 due to deprecations
✅ Simplicity: Native pandas encoding is easier to debug and maintain
✅ Hackathon Constraint: Avoiding extra dependencies for smoother collaboration

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
- **Git & GitHub**: Version control and collaboration

---

## 📊 Visual Insights in Pandas

✅ *KDE / Density Plots*

Help explore overlaps between age groups and:

- Trip duration
- Accommodation type
- Cost categories

✅ *Box & Violin Plots*

Helpful for hypothesis testing:

- Age Group vs Duration
- Age Group vs Cost
- Accommodation Type vs Age Group

✅ *Heatmaps & Correlations*

- Used to analyze multi-variable relationships
- Correlation between Age & Transport/Accomm. cost

🔬 *Normality & Chi-Square*
- Normality check via pingouin.normality()
- Chi2 independence tests for categorical associations

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

*Note on Power BI Integration*
We used pandas as a preprocessing bridge to clean, encode, and engineer features before importing the dataset into Power BI. This allowed greater control over transformations and supported seamless hypothesis testing alongside interactive dashboarding.

---

## 🧾 Project Workflow

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
├── data/
│ ├── raw/ # Original data files
│ │ ├── Travel details dataset.csv
│ │ ├── GlobalWeatherRepository.csv
│ │ └── EMM_EPM0_PTE_NUS_DPGm.xls
│ ├── processed/ # Cleaned & enriched datasets
│ ├── cleaned_travel.csv
│ ├── Temperature Data.csv
│ ├── fuel_price.csv
│ └── enriched_travel.csv
│
├── notebooks/ # Jupyter Notebooks
│ ├── Hackathon_Travel_Dataset.ipynb
│ ├── pcleaned_Weather_Data.ipynb
│ └── pcleaned_Fuel_Price.ipynb
│
├── dashboard/
│ └── Travel_Dashboard.pbix # Final Power BI dashboard
│
├── .gitignore
└── README.md

---

## Dataset Limitations 

- Sparse Dataset
- No actual cost data (accommodation and transport are categorical only)
- No true time series – dates exist, but no booking or seasonal trends
- Includes PII (names, IDs) — must be removed for ethical use
- No metadata or source details — limits confidence in representativeness
- Some fields (e.g., nationality, transport) may be imbalanced or biased
- No trip ID, making tracking and grouping more difficult.

## 🚧 Backlog & Improvements

- Predictive analytics for cost estimation
- Time series model on fuel price fluctuation
- Real-time climate API integration
- Interactive bundling recommendation engine

---

## 🤝 Team **Hitchhikers** Roles

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