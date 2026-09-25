# Project 1 - Replicating Temperature Anomalies Graphics
Urwa Irfan
Invalid Date

# Introduction

This project attempts to replicate three graphics from NASA Goddard
Institute for Space Studies (GISS) Surface Temperature Analysis
(GISTEMP) version 4. The GISTEMP dataset is an estimate of global
surface temperature change and includes data from 1880 to the present
day. More information about these data and the raw files can be accessed
[on NASA’s website](https://data.giss.nasa.gov/gistemp/). A fourth
graphic from the New York Times ([original
article](https://www.nytimes.com/interactive/2019/02/06/climate/fourth-hottest-year.html)),
which is a modified version of a GISTEMP graphic, is also included.

# Graphics

## Graphic 1: Temperature Anomalies over Land and over Ocean

<!-- ![](https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_temp_anomalies.png) -->

| Original | Replication |
|:--:|:--:|
| <img src="https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/Temperature_Anomalies_over_Land_and_over_Ocean/graph.png" width="100%"/> | <img src="https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_temp_anomalies.png" width="60%"/> |

This graphic shows annual (thin lines) and five-year lowess smooth
(thick lines) for the temperature anomalies (vs. 1951-1980) averaged
over the Earth’s land area and sea surface temperature anomalies
(vs. 1951-1980) averaged over the open ocean.

## Graphic 2: GISTEMP Seasonal Cycle since 1880

<!-- ![](https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_gistemp.png) -->

| Original | Replication |
|:--:|:--:|
| <img src="https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/GISTEMP_Seasonal_Cycle_since_1880/graph.png" width="100%"/> | <img src="https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_gistemp.png" width="80%"/> |

This graphic shows how much warmer each month of the GISTEMP data is
than the annual global mean. Each coloured line is an individual year in
the dataset. The 2026 line is highlighted with the circle points.

## Graphic 3: Global Annual Mean Surface Air Temperature Change

<!-- ![](https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_mean_temp_change.png) -->

| Original | Replication |
|:--:|:--:|
| <img src="https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/Global_Mean_Estimates_based_on_Land_and_Ocean_Data/graph.png" width="100%"/> | <img src="https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_mean_temp_change.png" width="60%"/> |

This graphic plots the land-ocean temperature index, 1880 to present,
with base period 1951-1980. The thin black line is the global annual
mean and the thick red line is the five-year lowess smooth. The gray
shading represents the total (LSAT and SST) annual uncertainty at a 95%
confidence interval.

## Graphic 4: The chart line from The New York Times

<!-- ![](https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_nyt_mean_temp_change.png) -->

| Original | Replication |
|:--:|:--:|
| <img src="https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/instructions/Rising-Global-Temperature-NYT-Feb-06-2019.png" width="100%"/> | <img src="https://raw.githubusercontent.com/UCB-stat159-f26/proj01-2-urwahah/refs/heads/main/output/plot_nyt_mean_temp_change.png" width="80%"/> |

This is a modified version of Graphic 3, with only the global annual
means plotted. These values were adjusted by NYT using a base period of
1880-1899 instead of GISTEMP’s 1951-1980. I was unable to correctly
reproduce NYT’s adjusted values; as an estimation, I corrected GISTEMP’s
data by 0.19°C based on [their
recommendation](https://data.giss.nasa.gov/gistemp/faq/#q102a).
