# 🌍 Travel Trends 

"Great journeys begin with insight – knowing who travels, where, how, and why is the map to every business decision."


# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)


## 📌 Project Objective

This project delivers a **multi-layered analytical view** of global travel behavior. By integrating traveler, fuel, and weather data, we uncover **demographic, geographic, and economic factors** that shape trip duration, transport/accommodation preferences, and travel cost dynamics.

The final product includes:

- A Power BI dashboard showing dynamic insights for two main stakeholders.

- A statistical validation notebook in Python with advanced plots and hypothesis testing.

### 👥 Intended Users
- **Travel Intelligence Analysts** – Identify patterns in travel behavior and segments for optimized planning and offers.
- **Transport Providers** – Align pricing and service delivery with travel and fuel trends.


## 📁 Dataset Summary

| Dataset             | Source   | Description                                                   |
| ------------------- | -------- | ------------------------------------------------------------- |
| Travel Trip Dataset | Kaggle   | Traveler demographics, destinations, costs, modes of travel   |
| Global Weather Repo | Kaggle   | Monthly average temperatures per country                      |
| Fuel Price (Excel)  | U.S. EIA | Monthly fuel price index for U.S. (2019–2025)                 |
| Temperature Summary | Derived  | Cleaned CSV of monthly average temperatures mapped by country |


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

## 🧠 Feature Encoding Strategy
We opted for custom pandas-based encoders instead of external libraries due to:

✅ Compatibility: category_encoders showed issues with Python 3.12 due to deprecations

✅ Simplicity: Native pandas encoding is easier to debug and maintain

✅ Hackathon Constraint: Avoiding extra dependencies for smoother collaboration


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

## 🧪 Hypothesis Framing & Validation

We followed a structured approach:

1. **Defined hypotheses** from questions rooted in domain logic
2. **Segregated data** by demographics
3. **Applied statistical tests** (Chi-Square, Pearson, ANOVA) using `scipy`
4. **Visualized results** using appropriate charts (bar, violin, scatter, heatmap)
5. **Documented conclusions** inline with visual output

This methodology ensured traceability from question to decision.

## 🛠️ Tools & Technologies Used

- **Python**: pandas, seaborn, pingouin, matplotlib
- **Power BI**: Dashboard creation and interactivity
- **Jupyter Notebooks**: For analysis and documentation
- **Git & GitHub**: Version control and collaboration


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

## 📊 Dashboard Design Strategy

The dashboard was designed around stakeholder needs identified early in the project:

- Executives: quick KPIs and overall travel trends
- Analysts: filters and drill-downs by age, gender, nationality
- Planners: demand trends, cost distributions, seasonality indicators

Tools used:
- **Power BI** for final interactive dashboard
- **Seaborn & Matplotlib** for static exploratory plots
- **Plotly** for GitHub deployment of interactive visuals

### 🖼 Dashboard Preview

Below is a snapshot of the interactive travel dashboard built in Power BI:

![Dashboard Screenshot](jupyter_notebooks\images\cover.png)
![Dashboard Screenshot](jupyter_notebooks\images\map.png)


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

## 🚀 Deployment & Visual Integration

### 🌐 GitHub Pages – Fuel Price Trends vs Global Events

An interactive choropleth map of the **Top 5 Destination Countries** has been deployed using Plotly and GitHub Pages:

🔗 **Live Demo**: 
[Top 5 Destination Countries Map](https://banerjixplores.github.io/travel_interactive/)
[Geopolitical Events and Travel Costs](https://banerjixplores.github.io/geopoliticalevents_travel/)

Key Features:
- Time series line chart of average fuel prices
- Shaded periods for COVID-19 and Ukraine war
- Powered by Seaborn and Matplotlib, rendered via nbviewer

This deployment leverages Plotly’s interactivity and nbviewer compatibility to provide a web-friendly visualization.

### 📊 Notebook Structure for Visuals

We organized our visualization strategy into two key layers:

- `travel_visualizations_pandas.ipynb`: Built using **Seaborn** and **Matplotlib** for high-quality, static plots suitable for **Power BI** integration. These visuals are exported as PNGs or directly embedded into Power BI reports using Python visuals.

- `travel_interactive_plotly.ipynb` (linked above): Includes dynamic **Plotly** maps and charts for GitHub and notebook storytelling.

Each visualization directly supports one or more hypotheses outlined in the statistical testing framework.


## 🧪 Statistical Hypotheses Testing

- **Chi-Square**: Gender vs destination; age group vs accommodation type
- **Correlation Matrix**: Accommodation cost vs transport cost, age, and fuel price

Plots generated using Python and imported into Power BI as images or tooltips.

*Note on Power BI Integration*
We used pandas as a preprocessing bridge to clean, encode, and engineer features before importing the dataset into Power BI. This allowed greater control over transformations and supported seamless hypothesis testing alongside interactive dashboarding.


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


## 📂 Project Structure

```project-root/
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
```
## 🔬 Libraries & Analysis Techniques Used

| Category             | Tools/Methods                                 |
|----------------------|-----------------------------------------------|
| Data Cleaning        | pandas, custom encoding & label grouping      |
| Visualization        | seaborn, matplotlib, plotly                   |
| Statistical Testing  | scipy.stats (chi2, Pearson), ANOVA            |
| Hypothesis Framing   | Exploratory EDA + data segmentation           |
| Deployment           | GitHub Pages, Jupyter Notebooks, nbviewer     |


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


## 🤝 Team **Hitchhikers** Roles

| Role           | Key Tasks                                      |
----------------|------------------------------------------------|
| Data Architect | Feature engineering, Power BI integration      |
| Data Analyst   | Visuals, storytelling, statistical plots        |
| Project Manager| Kanban, retrospectives, GitHub coordination    |


## 📚 References

- [Traveler Trip Dataset – Kaggle](https://www.kaggle.com/datasets/rkiattisak/traveler-trip-data)
- [Global Weather Repository – Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository)
- [U.S. Fuel Prices – EIA](https://www.eia.gov/petroleum/gasdiesel/)

## Code Assisted by AI (ChatGPT & GitHub Copilot)

This project leveraged AI-based support for formatting, markdown, and geospatial logic.

A key example:

```python
import geopandas as gpd
import pandas as pd
import matplotlib.pyplot as plt

# Load world map
url = "https://raw.githubusercontent.com/datasets/geo-countries/master/data/countries.geojson"
world = gpd.read_file(url)

# Destination frequency
trip_counts = df["Dest_Country"].value_counts().reset_index()
trip_counts.columns = ["country", "trip_count"]

# Country name alignment
replace_map = {
    "USA": "United States of America",
    "UK": "United Kingdom",
    "UAE": "United Arab Emirates",
    "Russia": "Russian Federation",
    "South Korea": "Korea, Republic of",
    "Vietnam": "Viet Nam",
    "Ivory Coast": "Côte d'Ivoire",
}
trip_counts["country"] = trip_counts["country"].replace(replace_map)

# Merge and visualize
world["trip_count"] = world["name"].map(trip_counts.set_index("country")["trip_count"]).fillna(0)
world["is_top5"] = world["name"].isin(trip_counts.nlargest(5, "trip_count")["country"])

fig, ax = plt.subplots(figsize=(15, 8))
world.plot(ax=ax, color="#eeeeee", edgecolor="white")
world[world["trip_count"] > 0].plot(ax=ax, color="#e6e6b3", edgecolor="gray")
world[world["is_top5"]].plot(ax=ax, color="#ffa07a", edgecolor="gray")

for _, row in world[world["is_top5"]].iterrows():
    x, y = row.geometry.representative_point().coords[0]
    plt.text(x, y, row["name"], fontsize=10, ha="center")

ax.set_facecolor("#d6ebf2")
ax.set_title("World Map: Top 5 Destination Countries", fontsize=14)
ax.axis("off")
plt.tight_layout()
plt.show()
```

## Acknowledgements (optional)

Thanks to Vasi for facilitating all the resources and clear instructions for conducting this standalone project.

Thanks to John's interactive coding sessions on coding, and recapitulating the concepts through practical examples during the Data Coach sessions, and to Niel's SME sessions

Last, but not the least, Grateful to have such nice colleagues in this Cohort :)