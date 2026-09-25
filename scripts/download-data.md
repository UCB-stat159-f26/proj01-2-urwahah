# Download Raw Data
Urwa Irfan
2026-09-24

``` r
# list file paths to download data from and to
url_temp_anomalies = "https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/Temperature_Anomalies_over_Land_and_over_Ocean/graph.csv"
url_gistemp = "https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/GISTEMP_Seasonal_Cycle_since_1880/graph.csv"
url_mean_temp_change = "https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/Global_Mean_Estimates_based_on_Land_and_Ocean_Data/graph.csv"
url_mean_temp_change_uncertainty = "https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/totalCI_ERA.csv" # mentioned here https://data.giss.nasa.gov/gistemp/uncertainty/quantification.html

dest_temp_anomalies = "../data/data_temp_anomalies.csv"
dest_gistemp = "../data/data_gistemp.csv"
dest_mean_temp_changes = "../data/data_mean_temp_change.csv"
dest_mean_temp_changes_uncertainty = "../data/data_mean_temp_change_uncertainty.csv"
```

``` r
download.file(url_temp_anomalies, dest_temp_anomalies)
download.file(url_gistemp, dest_gistemp)
download.file(url_mean_temp_change, dest_mean_temp_changes)
download.file(url_mean_temp_change_uncertainty, dest_mean_temp_changes_uncertainty)
```
