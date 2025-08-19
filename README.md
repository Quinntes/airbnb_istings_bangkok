
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

---

### Exploratory Data Analysis (EDA)

Here are the key findings from the data analysis conducted to understand the factors influencing Airbnb listing performance in Bangkok:

1. **Dominant Room Type and Price by Room Type**

   * The "Entire home/apt" room type has the highest number of listings and significantly higher prices compared to other room types. These listings tend to have more reviews but lower availability.

2. **Neighborhood Distribution and Location’s Impact on Competition**

   * Vadhana and Khlong Toei have the highest number of listings, indicating areas with higher competition between hosts. Location plays a key role in pricing strategy and occupancy.

3. **Professional vs. Non-Professional Hosts**

   * The majority of hosts (71%) are professionals managing multiple listings, while 29% are non-professionals with a single listing. Professional hosts tend to have more varied pricing and performance, although most listings are within the lower price range.

4. **Price Correlation with Reviews and Availability**

   * There is no strong correlation between price and review count, although higher-priced listings do not always have more reviews. High-priced listings tend to have lower availability but this pattern is not consistent.

5. **Minimum Night Duration and Guest Preferences**

   * Most listings set a minimum stay of just one night, indicating that guests prefer shorter stays.

6. **Seasonal Trends in Price and Reviews**

   * Prices and review counts show seasonal fluctuations, with peaks in December (holiday season). Summer months see lower prices and fewer reviews.

7. **Correlation Between Price, Reviews, and Occupancy**

   * No significant correlation was found between price and occupancy. The correlation between price and review count is weak, suggesting that other factors (like location and listing quality) are more influential.

8. **Popular Keywords in Listings and Sentiment**

   * Keywords related to location and accessibility (e.g., "BTS" and "near") dominate in listing descriptions. Descriptions are generally neutral, with little positive or negative sentiment. Listings with more reviews emphasize convenience and comfort.

9. **Impact of Last Review Time on Price and Popularity**

   * No strong relationship was found between the time since the last review and price. However, listings with longer gaps between reviews tend to have fewer reviews overall, indicating that recent reviews increase popularity.

10. **Impact of Proximity to Tourist Attractions on Price and Performance**

    * No strong correlation was found between proximity to key tourist attractions and price. Listings closer to popular tourist spots don’t always have higher prices, but some more distant areas (like Terminal 21) tend to be more affordable.

---

### Recommendations for Airbnb Hosts

1. **Optimize Location and Accessibility**
   Highlight your property's accessibility, especially if close to public transportation (e.g., BTS, MRT), and emphasize proximity to tourist attractions like the Grand Palace and Khao San Road. Use keywords like “near BTS” in your listing description to increase visibility.

2. **Enhance Room Types and Pricing Strategy**
   Focus on the "Entire home/apt" room type, which tends to dominate the market. Ensure high-quality amenities and competitive pricing. Professional hosts should offer a range of prices to cater to different market segments, while non-professional hosts should focus on competitive pricing with essential amenities.

3. **Leverage Seasonal Pricing and Availability**
   Adjust prices based on seasonal demand—raise prices during peak seasons (Winter and Spring) and offer discounts in off-peak seasons (Summer and Fall). Set flexible minimum stay policies, particularly during slower periods, and ensure availability is maintained, especially for lower-priced listings.

4. **Increase Reviews and Popularity**
   Encourage guests to leave reviews by offering incentives or discounts. Listings with more reviews are more likely to attract guests and achieve higher occupancy. Use positive reviews to enhance your listing’s attractiveness and visibility.

5. **Improve Management and Listing Performance in Competitive Areas**
   In high-competition areas like Vadhana and Khlong Toei, enhance your listing’s quality with better photos, descriptions, and promotional offers to stand out. Focus on improving both the listing’s appearance and strategic pricing to remain competitive.

6. **Focus on Room Type and Pricing Adjustments**
   For "Entire home/apt" listings, focus on enhancing amenities and exclusivity to justify higher prices. For "Private room" listings, keep prices competitive while ensuring comfort and appeal.

7. **Understand the Relationship Between Price and Reviews**
   While there is a weak correlation between price and the number of reviews, listings with more positive reviews and reasonable prices tend to attract more guests. Focus on improving guest experiences and increasing review counts.

---

### Key Conclusions

1. Location and accessibility are crucial factors that should be emphasized in each listing.
2. Prices should be adjusted according to seasonal trends to maximize revenue.
3. Listing quality and review count significantly impact price and occupancy.
4. Flexible pricing strategies and diversified room types help reach a wider market.
5. Efficient listing management is essential for professional hosts to stay competitive.

By following these recommendations, Airbnb hosts in Bangkok can improve their listing performance, optimize revenue, and maintain high occupancy rates.

---

### Key Suggestions


1. **Optimize Listings Based on Location, Accessibility, and Market Trends**
   Focus on strategic location features such as proximity to BTS, MRT, and popular tourist spots (e.g., Grand Palace, Khao San Road) in your listing descriptions. Additionally, adjust your pricing based on seasonal trends—raise prices during peak seasons (Winter and Spring) and offer discounts in off-peak times (Summer and Fall). Regularly monitor market trends to remain competitive.

2. **Enhance Appeal through Reviews and Sentiment**
   Listings with more reviews tend to attract more guests. Encourage guests to leave reviews by offering incentives and emphasize positive reviews in your descriptions. Focus on improving guest engagement to increase review count and listing popularity.

3. **Focus on Room Type, Availability, and Competitive Pricing**
   Ensure "Entire home/apt" listings are well-maintained with high-quality amenities, and for "Private room" listings, maintain competitive prices while ensuring comfort. Keep availability high, especially for budget-friendly listings, to improve occupancy. In competitive neighborhoods (e.g., Vadhana, Khlong Toei), adjust pricing carefully and use promotions to stand out.

4. **Use Data Insights for Better Decision Making**
   Understand the relationship between price, reviews, and availability to optimize your pricing strategies. Continuously improve your listing quality, service, and guest engagement to maximize occupancy and visibility.

---

## Tableau Visualization

Interactive Tableau dashboard will be provided upon project completion. The dashboard will present key metrics and visualizations such as:
- Map of Airbnb listings by price and popularity.
- Price vs. availability scatter plots.
- Heatmaps of listings by neighborhood and room type.

---

## Deliverables

1. **Jupyter Notebook**: `airbnb_listings_bangkok.ipynb`
2. **Tableau Dashboard**: [Tableau](https://public.tableau.com/views/airbnb_listings_bangkok_tableu/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
3. **Presentation Slides**: Summary and findings in slide format
4. **README.md**: Project documentation (this file)

---
