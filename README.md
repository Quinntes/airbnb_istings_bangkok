
# Capstone Project 2: Analysis of Popularity of Airbnb Listings in Bangkok

## Background & Problem Statement

### Background
Airbnb in Bangkok has more than 14,000 active listings, with an average annual revenue of approximately $7,443 and an occupancy rate of around 44%. While there is variation in listing performance, key factors such as price, room type, location, and reviews play a significant role in determining the popularity and potential revenue. However, many listings are suboptimal in attracting guests, especially those that rarely update information or receive reviews.

**Source:** [Airroi](https://www.airroi.com/report/world/thailand/bangkok/bangkok)

### Problem Statement
The goal of this analysis is to identify the factors influencing the performance of Airbnb listings in Bangkok, both in terms of popularity and potential revenue. These factors will be explored based on available data, including room types, price, location, and guest reviews. A better understanding of these factors will allow Airbnb to provide more accurate recommendations to hosts to optimize their listings.

This analysis aims to delve into the factors affecting listing performance and provide actionable recommendations to optimize revenue and occupancy potential. The first step involves data cleaning and feature engineering to ensure data quality and prepare additional features for enhanced analysis.

---

## Data Preparation

Data cleaning and feature engineering are essential first steps. The dataset will be evaluated to ensure its quality by checking for missing values, duplicates, or inconsistent data. Additionally, new features will be developed to enrich the analysis and provide deeper insights into the factors that affect listing performance.

### Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
import requests
import folium
import warnings
warnings.filterwarnings('ignore')
```

| Library             | Purpose                                                                                                                                                 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pandas`            | Used for data manipulation such as cleaning, transformation, and analysis of tabular data.                                                           |
| `numpy`             | Used for numerical operations, mainly for calculating statistics and manipulating arrays/matrices.                                                       |
| `matplotlib.pyplot` | Used for data visualization, particularly basic charts like histograms, boxplots, etc.                                                                 |
| `seaborn`           | Used for advanced data visualization with more attractive and informative designs (e.g., heatmaps, pairplots, etc.). |
| `scipy.stats`       | Used for statistical analysis like normality tests, hypothesis testing, and outlier detection.                                                              |
| `requests`          | Used for HTTP requests, useful when downloading data from APIs or external sources.                                                        |
| `folium`            | Used for interactive map visualization, useful when data involves geographic coordinates (latitude/longitude).                                      |
| `warnings`          | To manage and suppress warning messages during code execution.  |

### Load Dataset

The first step in this analysis is to load the dataset that will be used. Data is imported from two sources:
- The main dataset in CSV format containing information about Airbnb listings in Bangkok.
- A GeoJSON file describing districts in Bangkok, used for geographical visualization.

```python
url = 'https://raw.githubusercontent.com/Quinntes/airbnb_listings_bangkok/refs/heads/main/airbnb_listings_bangkok.csv'
df_raw = pd.read_csv(url)
url = 'https://raw.githubusercontent.com/Quinntes/airbnb_listings_bangkok/main/bangkok-districts.geojson'

response = requests.get(url)
geojson_data = response.json()  # Get GeoJSON data
```

### Data Cleaning

- **Backup Raw Dataset**: Create a backup of the raw dataset before any cleaning is done to ensure the original data remains intact.
- **Overview & Diagnosis**: Check the shape of the dataset, data types, and missing values per column.
- **Duplicate Handling**: Verify that there are no duplicate rows.
- **Data Type Correction**: Ensure columns such as `price` are numeric and convert `last_review` to datetime.
- **Missing Values**: Handle missing values for columns like `name` and `host_name`.
- **Outlier Detection**: Identify and handle outliers in columns such as `price` and `minimum_nights`.
- **Feature Engineering**: Create new features like `days_since_last_review`, `host_type`, and `estimated_revenue`.

### Exploratory Data Analysis (EDA)

The data will be analyzed to answer the following questions:

1. **Distribution of Listings by Room Type and Neighborhood**  
   - Visualizations: Bar chart, Pie chart
   - Insight: Identifying the most common room types and their geographical spread.

2. **Price vs. Occupancy**  
   - Visualizations: Scatter plot between `price` and `availability_365`
   - Insight: Identifying the optimal price points for listings.

3. **Characteristics of Popular Listings (More Reviews)**  
   - Visualizations: Boxplot for comparing `price`, `room_type`, and `minimum_nights` for listings with high reviews.

4. **Factors Affecting Popularity**  
   - Visualizations: Heatmap of correlations between numeric variables.
   - Insight: Identifying variables strongly correlated with listing popularity.

5. **Hosts with Multiple Listings**  
   - Visualizations: Bar chart/Boxplot comparing reviews based on `host_type`.

---

## Insight & Recommendations

### Insights:
- Based on the findings from EDA, the following insights emerged regarding Airbnb listings in Bangkok:
  - Room type distribution shows a high concentration of `Entire home/apt` listings.
  - Listings with higher prices tend to have lower availability and fewer reviews.
  - Listings with active reviews are more popular, while those without reviews tend to have lower prices and fewer bookings.

### Recommendations:
- **Invest in Entire Homes/Apartments**: These listings tend to have the highest price points and are more frequently booked.
- **Focus on High-demand Neighborhoods**: Areas like Vadhana and Khlong Toei dominate the listing count and present competitive opportunities for hosts.
- **Price Optimization**: Implement dynamic pricing strategies based on seasonal trends and competition.
- **Increase Review Counts**: Encourage guests to leave reviews, which correlates with higher visibility and bookings.

---

## Tableau Visualization

Interactive Tableau dashboard will be provided upon project completion. The dashboard will present key metrics and visualizations such as:
- Map of Airbnb listings by price and popularity.
- Price vs. availability scatter plots.
- Heatmaps of listings by neighborhood and room type.

---

## Deliverables

1. **Jupyter Notebook**: `airbnb_analysis.ipynb`
2. **Tableau Dashboard**: [Tableau](https://public.tableau.com/views/airbnb_listings_bangkok_tableu/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
3. **Presentation Slides**: Summary and findings in slide format
4. **README.md**: Project documentation (this file)

---
