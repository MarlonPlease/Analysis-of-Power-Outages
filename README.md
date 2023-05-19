# Analysis of Power Outages in the United States

by Marlon Garay (mjgaray@ucsd.edu) and Jiawei Li (jil237@ucsd.edu)

***Note***: Testing

---

## Introduction

This repository contains a group project focused on analyzing power outages in the United States. The project utilizes Python and the Pandas library for data analysis using an Excel file as the data source.
Objective

The main objective of this project is to identify trends and patterns in power outages through comprehensive data analysis.
Data Source

The data used in this analysis originates from the article "A Multi-Hazard Approach to Assess Severe Weather-Induced Major Power Outage Risks in the U.S." (Mukherjee et al., 2018). It explores major power outages that occurred in different states across the continental United States between January 2000 and July 2016. Major outages are defined by the Department of Energy as those impacting a minimum of 50,000 customers or causing an unplanned firm load loss of at least 300 MW.

The dataset contains details such as outage location, date, and time. Additionally, it includes regional climate data, land-use characteristics, electricity consumption patterns, and economic factors of the affected states. This comprehensive dataset enables the identification and analysis of historical trends and patterns in major outages, as well as the assessment of risk predictors associated with prolonged power disruptions in the continental United States.
Data Acquisition

To obtain the necessary data for this study, we utilized various publicly available datasets, including:

- OE-417 form Schedule 1 published by DOE's Office of Electricity Delivery and Energy Reliability
- U.S. Energy Information Administration (EIA) datasets, specifically form EIA-826 and EIA-861
- National Oceanic and Atmospheric Administration (NOAA) and National Climatic Data Center (NCDC)
- U.S. Department of Labor, Bureau of Labor Statistics
- U.S. Census Bureau

By combining these datasets, we were able to gather comprehensive information for our power outage analysis.

Please refer to the project files for the implementation details and analysis of the data.

---

## Cleaning and EDA

The data, referred to as "outage.xlsx," originated from an Excel file. To import the data into the notebook, the "pd.read_excel" function was utilized.

In the provided code snippet, we address the data cleaning process for the columns in the `powerDF` DataFrame, which was initially loaded from an Excel file named `'outage.xlsx'`. The DataFrame encountered challenges with its index and misaligned rows and columns, which were attributed to the structure of the original `'outage.xlsx'` file. To resolve these issues, the following steps were undertaken:

- We merged the `'OUTAGE.START.DATE'` and `'OUTAGE.START.TIME'` columns together by adding their values and stored the result in a new column called `'OUTAGE.START'`. This process was repeated for the `'OUTAGE.RESTORATION.DATE'` and `'OUTAGE.RESTORATION.TIME'` columns, which were merged into the `'OUTAGE.RESTORATION'` column. This merging of date and time columns allows us to have a combined timestamp for each outage event.
- `'OBS'` assigned as the new index: The 'OBS' column was designated as the new index for the DataFrame. 
- The newly created `'OUTAGE.START'` and `'OUTAGE.RESTORATION'` columns were converted to the appropriate datetime type using the `pd.to_datetime` function. This conversion ensures that the timestamps are recognized as datetime objects, enabling further analysis and manipulation based on time-related operations. 
- We dropped the original date and time columns (`'OUTAGE.START.DATE'`, `'OUTAGE.START.TIME'`, `'OUTAGE.RESTORATION.DATE'`, and `'OUTAGE.RESTORATION.TIME'`) from the DataFrame. Since we have already merged and converted the relevant information into the `'OUTAGE.START'` and `'OUTAGE.RESTORATION'` columns, the original date and time columns are no longer needed. The columns `'OUTAGE.START'` and `'OUTAGE.RESTORATION'` were converted to the `datetime64[ns]` data type.

By performing these cleaning steps, we have transformed and organized the data to facilitate subsequent analysis and exploration of the power outage events.

I guess we put some graph here

The graph illustrates the annual count of reported outages as reported by U.S. states.

<iframe src="assets/Reported_Outages_plot.html" width=800 height=600 frameBorder=0></iframe>

The graph illustrates the average outage duration by State since the data was first reported(Year 2000)

<iframe src="assets/US_Map_plot.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/electricity_prices_plot.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/data_outage_lineplot.html" width=800 height=600 frameBorder=0></iframe>





---

## Assessment of Missingness


Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |

---

## Hypothesis Testing


---
