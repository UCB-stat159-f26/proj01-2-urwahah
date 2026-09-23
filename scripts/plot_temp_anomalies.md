# Plot 1 - Temperature Anomalies over Land and over Ocean
Urwa Irfan
2026-09-22

## Load librares and data

``` r
library(tidyverse)
library(ggplot2)
library(scales)

dest_temp_anomalies = "../data/data_temp_anomalies.csv"
```

``` r
dat = read_csv(dest_temp_anomalies, skip = 1)
```

    New names:
    Rows: 146 Columns: 5
    ── Column specification
    ──────────────────────────────────────────────────────── Delimiter: "," dbl
    (5): Year, Land_Annual, Lowess(5)...3, Ocean_Annual, Lowess(5)...5
    ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    Specify the column types or set `show_col_types = FALSE` to quiet this message.
    • `Lowess(5)` -> `Lowess(5)...3`
    • `Lowess(5)` -> `Lowess(5)...5`

## Create plot

``` r
dat |>
    ggplot() +
        geom_line(aes(Year, Land_Annual, color = "land_annual"), linewidth = 0.5) +
        geom_point(aes(Year, Land_Annual, color = "land_annual"), shape = 15, size = 1.5) +
        geom_line(aes(Year, `Lowess(5)...3`, color = "land_lowess"), linewidth = 1) +
        geom_line(aes(Year, Ocean_Annual, color = "ocean_annual"), linewidth = 0.5) +
        geom_point(aes(Year, Ocean_Annual, color = "ocean_annual"), shape = 15, size = 1.5) +
        geom_line(aes(Year, `Lowess(5)...5`, color = "ocean_lowess"), linewidth = 1) +
        scale_y_continuous(breaks = seq(-0.8, 2, 0.2)) +
        scale_x_continuous(breaks = seq(1880, 2020, 20), labels = comma) +
        scale_color_manual(
            values = c("land_annual" = "#ffa500", "land_lowess" = "#ff0000","ocean_annual" = "#87ceeb", "ocean_lowess" = "#0000ff"),
            labels = c("land_annual" = "Land Surface Air Temperature", "land_lowess" = "Land Lowess Smoothing", "ocean_annual" = "Sea Surface Water Temperature", "ocean_lowess" = "Sea Lowess Smoothing")
        ) +
        labs(
            y = "Temperature Anomaly w.r.t. 1951-80 (°C)",
            x = "",
            title = "Temperature Anomalies over Land and over Ocean",
        ) +
        theme_classic() +
        theme(
            legend.position = "inside", legend.position.inside = c(0.03, 0.8), legend.title = element_blank(),
            legend.justification="left", legend.background = element_rect(linewidth = 0.5, colour = "#e0e0e0"), #element_blank(),
            plot.title = element_text(size = 11, hjust = 0.5)
        ) +
        annotate("text", x = 2000, y = -0.8, size = 3.5, label = "NASA/GISS/GISTEMP v4")
```

![](plot_temp_anomalies_files/figure-commonmark/plot-1.png)
