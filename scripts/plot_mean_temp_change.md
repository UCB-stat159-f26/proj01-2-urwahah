# Plot 3 - Global Annual Mean Surface Air Temperature Change
Urwa Irfan
2026-09-24

## Load librares and data

``` r
library(tidyverse)
library(ggplot2)
library(scales)

dest_mean_temp_changes = "../data/data_mean_temp_change.csv"
dest_mean_temp_changes_uncertainty = "../data/data_mean_temp_change_uncertainty.csv"
```

``` r
dat = read_csv(dest_mean_temp_changes, skip = 1)
```

    Rows: 146 Columns: 3
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    dbl (3): Year, No_Smoothing, Lowess(5)

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
dat_uncertainty = read_csv(dest_mean_temp_changes_uncertainty) |> drop_na()
```

    Rows: 288 Columns: 2
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    dbl (2): year, ci95

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## Calculate uncertainty interval

``` r
combined_dat = dat |> 
    left_join(dat_uncertainty, by = c("Year" = "year")) |>
    mutate(mean_upper = No_Smoothing + ci95, mean_lower = No_Smoothing - ci95)
```

## Create plot

``` r
plt_mean_temp_change = combined_dat |>
    ggplot() +
        # geom_line(aes(Year, mean_upper, color = "ci95"), linewidth = 0.1) +
        # geom_line(aes(Year, mean_lower), linewidth = 0.1) +
        geom_ribbon(aes(x = Year, ymin = mean_lower, ymax = mean_upper, color = "ci95"), fill = "#d3d3d3") +
        geom_line(aes(Year, No_Smoothing, color = "mean"), linewidth = 0.3) +
        geom_line(aes(Year, `Lowess(5)`, color = "lowess"), linewidth = 1) +
        geom_point(aes(Year, No_Smoothing, color = "mean"), shape = 15, size = 1.2) +
        scale_y_continuous(breaks = seq(-0.6, 1.4, 0.2), limits = c(-0.6, 1.4), labels = comma) +
        scale_x_continuous(breaks = seq(1880, 2020, 20), labels = comma) +
        scale_color_manual(
            values = c("mean" = "black", "lowess" = "#ff0000", "ci95" = "#d3d3d3"),
            labels = c("mean" = "Annual Mean", "lowess" = "Lowess Smoothing", "ci95" = "LSAT+SST Uncertainty")
        ) +
        labs(
            y = "Temperature Anomaly w.r.t. 1951-80 (°C)",
            x = "",
            title = "Global Mean Estimates based on Land and Ocean Data",
        ) +
        theme_classic() +
        theme(
            legend.position = "inside", legend.position.inside = c(0.03, 0.8), legend.title = element_blank(),
            legend.justification="left", legend.background = element_rect(linewidth = 0.5, colour = "#e0e0e0"), #element_blank(),
            plot.title = element_text(size = 11, hjust = 0.5)
        ) +
        annotate("text", x = 2000, y = -0.6, size = 3.5, label = "NASA/GISS/GISTEMP v4")

# plt_mean_temp_change
```
