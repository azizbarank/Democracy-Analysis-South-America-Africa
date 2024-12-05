# Democracy-Analysis-South-America-Africa
The data analysis of the situation of democracy in South America and Africa
## Overview
This project aims to analyse and generate insight into the general situation of democracy in the South American and African countries. To achieve this, it uses the Python libraries of pandas, numpy, matplotlib and the Tableau for further visualizations. After having done with the coding part, the backstory of the current democracy scores of each country were explained according to their own political and historical events. Here are the specifics questions defined for the project:

### Project Questions:
#### To be answered during the preliminary analysis with pandas:
* What are the average democracy scores of South American and African countries during COVID-19 pandemic?
* What is the trend of change in democracy index during this period?
#### To be answered with Tableau:
* How can we compare all of countries in general (i.e., create a general map to show the democracy score of each country)
* Which countries are remarkable in the sense of having full democracies and authoritarian regimes?

## Dataset & Methods

---
### Dataset
The dataset was taken from is based on the index of the Economist Intelligence Unit, [EIU](https://ourworldindata.org/grapher/democracy-index-eiu). The general structure of the dataset is as follows:
* **Entity**: The name of the countries
* **Code**: The standard ISO code name of the countries
* **Year**: Respective years
* **Democracy score**: The score showing the condition of democracy in each country, ranging from 0-10.
---
---
### Methods & Steps
Below are the general steps taken for the data analysis. A few example codes are given to have an idea of what has been done. To look at the full codes, you can refer to the [notebook](https://github.com/azizbarank/Video-Game-Sales-Analysis/blob/main/games_analysis.ipynb).
1. Importing the necessary packages:

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```

2. First quick glance at the dataset:
```python
df.head()
df.info()
df.value_counts()
```

3. Since the focus is on South American and African countries only, making a list for each of them and also dropping the "Code" column since Tableau can generate an automatic map using only the name of the countries:
```python
south_american_countries = [
    "Argentina", "Bolivia", "Brazil", "Chile", "Colombia", "Ecuador",
    "Guyana", "Paraguay", "Peru", "Suriname", "Uruguay", "Venezuela"
]
df_filtered = df[df['Entity'].isin(south_american_countries)]
.
.
.
df_filtered.drop(columns=['Code'], inplace=True)
df_filtered.head()
```
4. Filtering the years to see if there is a trend of decline during COVID-19 pandemic:
```python
year_filtered_df = df_filtered[(df_filtered['Year'] >= 2019) & (df_filtered['Year'] <= 2023)]
year_filtered_df.head(20)
```
5. Looking at the democracy change throughout the years:
```python
year_filtered_df['Democracy change'] = year_filtered_df.groupby('Entity')['Democracy score'].diff()
.
.
.
average_change = year_filtered_df.groupby('Entity')['Democracy change'].mean().round(2)
```
6. Making the exact same thing for the African countries except that for the sake of simplicity of preliminary exploration, I decided to focus only on countries having suffered from a coup or military junta in the last five years, leaving the full comparison of South American and African countries for Tableau.
```python
african_countries = ['Mali', 'Burkina Faso', 'Niger', 'Chad', 'Guiena', 'Gabon', 'Sudan', 'Democratic Republic of Congo', 'Central African Republic']
.
.
.
```
4. Gaining insights:
    ##### 1. The condition of democracy in South American countries in terms of score (*table*)
    ##### 2. The condition of democracy in selected African countries in terms of score (*table*)
    ##### 3. The trend of these during the COVID-19 pandemic (*line plot*)
      ```python
      .
      .
      .
      bottom_updated_pivot = bottom_updated_df.pivot(index='Year', columns='Entity', values = 'Democracy score')
      for country in bottom_updated_pivot.columns:
      plt.plot(bottom_updated_pivot.index, bottom_updated_pivot[country], marker='o', label=country)

      # Add title and labels
      plt.title("Democracy Scores of Countries Over Time", fontsize=14)
      plt.xlabel("Year", fontsize=12)
      plt.ylabel("Democracy Score", fontsize=12)
      plt.xticks(bottom_updated_pivot.index, rotation=45)
      plt.legend(title="Country")
      plt.grid(True, linestyle='--', alpha=0.6)

      # Show the plot
      plt.tight_layout()
      plt.show()
      ```
5. Further visualizations with Tableau
---
## Results (Project Questions)
1. How can we compare all of countries in general (i.e., create a general map to show the democracy score of each country)
![maps](https://github.com/azizbarank/Democracy-Analysis-South-America-Africa/blob/main/images/maps.jpg)

2. Which countries are remarkable in the sense of having full democracies and authoritarian regimes?

For the detailed expression, please refer to this [blog post]() or [Tableau dashboard](https://public.tableau.com/app/profile/aziz.baran.kurtulus/viz/democracy_17333942440360/DemocracyMap).
