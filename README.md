# Analysis of Power Outages in the United States

by Marlon Garay (mjgaray@ucsd.edu) and 

***Note***: Testing

---

## Introduction

This is a group project aimed at analyzing power outages in the United States. We will be using Python and the Pandas library to conduct data analysis from an excel file.

Our objective is to identify trends in power outages through our analysis.

The data in was originally from an article, titled "A Multi-Hazard Approach to Assess Severe Weather-Induced Major Power Outage Risks in the U.S." (Mukherjee et al., 2018), examines major power outages that occurred in different states across the continental U.S. from January 2000 to July 2016. Major outages are defined by the Department of Energy as those impacting a minimum of 50,000 customers or causing an unplanned firm load loss of at least 300 MW. The dataset encompasses various details such as outage location, date, and time, along with regional climate data, land-use characteristics, electricity consumption patterns, and economic factors of the affected states. It facilitates the identification and analysis of historical trends and patterns in major outages, as well as the assessment of risk predictors associated with prolonged power disruptions in the continental U.S.
The data for this study was obtained from various publicly available datasets, including:
    OE-417 form Schedule 1 published by DOE's Office of Electricity Delivery and Energy Reliability 
    U.S. Energy Information Administration (EIA) datasets, specifically form EIA-826 and EIA-861.
    National Oceanic and Atmospheric Administration (NOAA) and National Climatic Data Center (NCDC).
    U.S. Department of Labor, Bureau of Labor Statistics [5].
    U.S. Census Bureau.

---

## Cleaning and EDA

I guess we put some graph here

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
