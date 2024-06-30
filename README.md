# Elections_Results_2024


This project analyzes the results of the 2024 elections using a dataset of election results. The analysis includes identifying the party with the highest and lowest margins of victory, visualizing the number of seats won by each party, and examining the top margins achieved by different parties.

## Table of Contents
- [Introduction](#introduction)
- [Dataset](#dataset)
- [Usage](#usage)
- [Analysis Overview](#analysis-overview)
- [Visualizations](#visualizations)
- [License](#license)

## Introduction

The goal of this project is to provide a comprehensive analysis of the 2024 election results. This includes:
- Identifying which party had the highest and lowest margin of victory.
- Plotting the number of seats won by each party.
- Highlighting the top margins achieved by different parties.
- Visualizing the election results on a map.

## Dataset

The dataset used for this analysis is `election_result_2024.csv`, which contains information on the election results, including the leading party and the margin of victory for each constituency.


## Usage
1. Clone this repository:

```sh
https://github.com/Vishal9871/Elections_Results_2024/blob/main/README.md
```

2. Navigate to the project directory:


3. Ensure you have the dataset election_results_2024.csv in the Dataset directory.

4. Run the Jupyter notebook:

```sh
jupyter notebook Election_results_2024_stats.ipynb
```
## Analysis Overview
### Import Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import plotly.express as px
import plotly.offline as py
from geopy.geocoders import Nominatim
import warnings
```

### Load Data

```python
data = pd.read_csv('Dataset/election_results_2024.csv')
data.head(10)
```

### Party with Highest and Lowest Margin of Victory

```python
party_votes = data.groupby('Leading Party')['Margin'].sum().sort_values(ascending=False)
data['Margin'] = pd.to_numeric(data['Margin'], errors='coerce')

highest_margin = data.loc[data['Margin'].idxmax()]
lowest_margin = data.loc[data['Margin'].idxmin()]
```
![image](https://github.com/Vishal9871/Elections_Results_2024/blob/main/graph/Highest%20and%20lowest%20Victory%20Candidate.png)

### Plot Number of Seats Won by Each Party

```python
leading_party_highest_votes = party_votes.idxmax()
leading_party_lowest_votes = party_votes.idxmin()
seats_won = data['Leading Party'].value_counts()

plt.figure(figsize=(20, 8))
sns.barplot(x=seats_won.index, y=seats_won.values, palette='viridis')
plt.title('Number of Seats Won by Each Party')
plt.xlabel('Party')
plt.ylabel('Seats Won')
plt.xticks(rotation=90)
plt.show()
```
![image](https://github.com/Vishal9871/Elections_Results_2024/blob/main/graph/Plot%20number%20of%20seats%20won%20by%20each%20party.png)

### Top Margin Achieved by Party
The analysis further explores the top margins achieved by different parties.
![image](https://github.com/Vishal9871/Elections_Results_2024/blob/main/graph/Top%20margin%20Achieved%20by%20party.png)

## Visualizations
### Election Results Map
To visualize the election results on a map, you can use the following code snippet:
```python
# Assuming your data has columns 'Constituency', 'Latitude', 'Longitude', 'Leading Party'
fig = px.scatter_geo(data,
                     lat='Latitude',
                     lon='Longitude',
                     color='Leading Party',
                     hover_name='Constituency',
                     size='Margin',
                     projection='natural earth')

fig.update_layout(title='Election Results 2024')
fig.show()
```
![State wise party distribution](https://github.com/Vishal9871/Elections_Results_2024/blob/main/graph/State%20wise%20party%20distribution.png)

### Number of Seats Won by Each Party
Here is a sample visualization of the number of seats won by each party:
![image](https://github.com/Vishal9871/Elections_Results_2024/blob/main/graph/Top%2010%20trailing%20party%20by%20SEAT.png)

## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/Vishal9871/Elections_Results_2024/blob/main/LICENSE) file for details.
