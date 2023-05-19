# Analysis of Power Outages in the United States

by Marlon Garay (mjgaray@ucsd.edu) and Jiawei Li (jil237@ucsd.edu)



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

For more background information about the dataset, please refer to the provided link [here]([https://www.sciencedirect.com/science/article/pii/S2352340918307182]), the link to the excel file is [here](https://engineering.purdue.edu/LASCI/research-data/outages/outagerisks)

***Question Identification***

In this project, we are given a dataset with major power outage data in the continental U.S. from January 2000 to July 2016, into which we will perform an open-ended investigation. 
After familiarizing outselves with the information contained in the dataset, a question that piques our interests that we plan to investigate further is: where and when do major power outages tend to occur? Specifically, are states in the East North Central region of America more likely to have severe power outage (outage duration >= 1000 minutes) on cold days?


---

## Cleaning and EDA

The data, referred to as "outage.xlsx," originated from an Excel file. To import the data into the notebook, the "pd.read_excel" function was utilized.

In the provided code snippet, we address the data cleaning process for the columns in the `powerDF` DataFrame, which was initially loaded from an Excel file named `'outage.xlsx'`. The DataFrame encountered challenges with its index and misaligned rows and columns, which were attributed to the structure of the original `'outage.xlsx'` file. To resolve these issues, the following steps were undertaken:

- We merged the `'OUTAGE.START.DATE'` and `'OUTAGE.START.TIME'` columns together by adding their values and stored the result in a new column called `'OUTAGE.START'`. This process was repeated for the `'OUTAGE.RESTORATION.DATE'` and `'OUTAGE.RESTORATION.TIME'` columns, which were merged into the `'OUTAGE.RESTORATION'` column. This merging of date and time columns allows us to have a combined timestamp for each outage event.
- `'OBS'` assigned as the new index: The 'OBS' column was designated as the new index for the DataFrame. 
- The newly created `'OUTAGE.START'` and `'OUTAGE.RESTORATION'` columns were converted to the appropriate datetime type using the `pd.to_datetime` function. This conversion ensures that the timestamps are recognized as datetime objects, enabling further analysis and manipulation based on time-related operations. 
- We dropped the original date and time columns (`'OUTAGE.START.DATE'`, `'OUTAGE.START.TIME'`, `'OUTAGE.RESTORATION.DATE'`, and `'OUTAGE.RESTORATION.TIME'`) from the DataFrame. Since we have already merged and converted the relevant information into the `'OUTAGE.START'` and `'OUTAGE.RESTORATION'` columns, the original date and time columns are no longer needed. The columns `'OUTAGE.START'` and `'OUTAGE.RESTORATION'` were converted to the `datetime64[ns]` data type.

By performing these cleaning steps, we have transformed and organized the data to facilitate subsequent analysis and exploration of the power outage events.

The head of out cleaned `powerDF` dataframe using `print(powerDF.head().to_markdown(index=False))`


|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   |
|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|
|     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 | 2.33292e+06 | 2.11477e+06 | 2.11329e+06 |   6.56252e+06 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |         0.4112 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 05:00:00 | 2011-07-03 08:00:00  |
|     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 | 1.58699e+06 | 1.80776e+06 | 1.88793e+06 |   5.28423e+06 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |         0.3748 |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 06:38:00 | 2014-05-11 06:39:00  |
|     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 | 1.46729e+06 | 1.80168e+06 | 1.9513e+06  |   5.22212e+06 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |         0.3924 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 08:00:00 | 2010-10-28 10:00:00  |
|     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 | 1.85152e+06 | 1.94117e+06 | 1.99303e+06 |   5.78706e+06 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |         0.4224 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 11:00:00  |
|     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 | 2.02888e+06 | 2.16161e+06 | 1.77794e+06 |   5.97034e+06 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |         0.367  |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |



***Univariate Analysis***

The graph below illustrates the annual count of reported outages as reported by U.S. states.
<iframe src="assets/Reported_Outages_plot.html" width=800 height=600 frameBorder=0></iframe>


The graph below displays the average outage duration in minutes by state from 2000 to 2016. It aims to investigate whether there is a correlation between the average duration of electric outages (measured in minutes) and the specific US states. 
In order to conduct this plot, we had to use a `.dropna` function to remove missing values in order to conduct the mean, and remove states that were not present.


We performed a `.mean()` on a `.groupby()` function on the column that represented US States after we used the `.dropna` function on the `'Outage.Duration'` column in order to perform the analysis.


| POSTAL.CODE   |   OUTAGE.DURATION |
|:--------------|------------------:|
| WI            |         7904.11   |
| WV            |         6979      |
| NY            |         6034.96   |
| MI            |         5302.98   |
| KY            |         5093.92   |
| IA            |         4793.75   |
| AZ            |         4552.92   |
| NJ            |         4450.91   |
| KS            |         4376.29   |
| DC            |         4303.6    |
| FL            |         4094.67   |
| LA            |         4084.55   |
| PA            |         3811.7    |
| IN            |         3521.64   |
| MO            |         3374.07   |
| SC            |         3135      |
| OK            |         3019.09   |
| OH            |         2867.86   |
| MN            |         2727.93   |
| TX            |         2704.82   |
| NE            |         2455.75   |
| MD            |         2313.09   |
| CA            |         1666.34   |
| IL            |         1602.45   |
| AR            |         1514.36   |
| WA            |         1508.15   |
| NC            |         1457.28   |
| GA            |         1345.41   |
| CT            |         1278.83   |
| AL            |         1152.8    |
| ME            |         1097.06   |
| VA            |         1051.19   |
| TN            |         1041.97   |
| MA            |          944.167  |
| CO            |          901.071  |
| HI            |          845.4    |
| OR            |          766.68   |
| ND            |          720      |
| NV            |          553.286  |
| ID            |          414.625  |
| NH            |          279.643  |
| UT            |          250.22   |
| DE            |          144.925  |
| NM            |          140.375  |
| SD            |          120      |
| MS            |           84      |
| MT            |           54      |
| VT            |           35.4444 |
| WY            |           33.3333 |

<iframe src="assets/US_Map_plot.html" width=800 height=600 frameBorder=0></iframe>


***Bivariate Analysis***

The illustration below explores the potential causal relationship between electricity prices and outage duration. It aims to investigate whether there is a correlation or influence between these two factors.
<iframe src="assets/electricity_prices_plot.html" width=800 height=600 frameBorder=0></iframe>

The illustration below also examines the relationship between the date and outage duration. It aims to determine if there are any specific patterns or trends in outage duration based on the date or time of occurrence.
<iframe src="assets/data_outage_lineplot.html" width=800 height=600 frameBorder=0></iframe>


***Interesting Aggregates***

The table provided represents data on power outages in different climate categories (cold, normal, warm) for each state. To analyze if power outages are worse during different climates in each state, we can examine the values in the table. The values in the table  represent outage duration aggregated by their US State.



| U.S._STATE           |       cold |    normal |       warm |
|:---------------------|-----------:|----------:|-----------:|
| Alabama              |  2247      |  233.5    |   803      |
| Arizona              |    74      |  789.538  | 14741.3    |
| Arkansas             |  2538.14   |  556.2    |  3916.33   |
| California           |  1787.67   | 1273.5    |  2117.45   |
| Colorado             |   860.667  |  151.286  |  2243.5    |
| Connecticut          |   316      | 1193.8    |  4592.5    |
| Delaware             |    50.9091 |   27.1154 |  1510.67   |
| District of Columbia |  2076.8    | 5691.5    |  9886      |
| Florida              |   494.3    | 6109      |  3952.88   |
| Georgia              |  2256      | 1152.71   |   963.167  |
| Hawaii               |  1367      |  205.5    |  1224.5    |
| Idaho                |   180      |  591.4    |     0      |
| Illinois             |  1986.67   | 1501.71   |  1155      |
| Indiana              |  4162.5    | 2732.56   |  7106.67   |
| Iowa                 |  8670      | 4240      |   nan      |
| Kansas               | 13650      |  913      |  3214.2    |
| Kentucky             |  6652.75   | 3222.75   |   108      |
| Louisiana            |  1910.12   | 5855.55   |  1388.75   |
| Maine                |  1337      | 1056.22   |   441      |
| Maryland             |  3117.94   | 2051.69   |  1418.67   |
| Massachusetts        |   160.333  | 1159.38   |   721      |
| Michigan             |  4808.16   | 5994.7    |  3419.71   |
| Minnesota            |  2610      | 3119.4    |   947.5    |
| Mississippi          |   nan      |  110.333  |     5      |
| Missouri             |  1995.83   | 5338.86   |   632      |
| Montana              |   nan      |   54      |   nan      |
| Nebraska             |   109.5    |    4      |  9600      |
| Nevada               |  1001.5    |  603      |    30.5    |
| New Hampshire        |   107.5    |  348.5    |   nan      |
| New Jersey           |  2867.41   | 6832      |  5575.29   |
| New Mexico           |     0      |  160.429  |   nan      |
| New York             |  8914.58   | 3673.56   |  6092.83   |
| North Carolina       |  2731      |  803.571  |  1416.86   |
| North Dakota         |   720      |  nan      |   nan      |
| Ohio                 |  1304.62   | 3311.36   |  4377.14   |
| Oklahoma             |  2801      | 3484.3    |  2394      |
| Oregon               |   323.444  |  868.143  |  1131      |
| Pennsylvania         |  3560.16   | 4334.43   |  3385.45   |
| South Carolina       |  3739.4    | 2947.5    |   488      |
| South Dakota         |   nan      |  nan      |   120      |
| Tennessee            |  1476.58   | 1015.75   |   341.857  |
| Texas                |  1406.27   | 4066.07   |  1540.29   |
| Utah                 |   694.538  |   34.3529 |    58.7273 |
| Vermont              |     1      |   39.75   |   nan      |
| Virginia             |   739.923  | 1123.7    |  1916.67   |
| Washington           |  1051.08   |  727.378  |  4342.06   |
| West Virginia        |   nan      | 9305      |     1      |
| Wisconsin            | 12545.6    | 3962.56   |  1605      |
| Wyoming              |    30.5    |   11      |   106      |




---

## Assessment of Missingness




***NMAR Analysis***



***Missingness Dependency***





---

## Hypothesis Testing


---
