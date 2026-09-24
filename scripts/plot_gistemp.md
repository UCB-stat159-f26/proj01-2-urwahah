# Plot 2 - GISTEMP Seasonal Cycle since 1880
Urwa Irfan
2026-09-24

## Load librares and data

``` r
library(tidyverse)
library(ggplot2)
library(scales)

dest_gistemp = "../data/data_gistemp.csv"
```

``` r
dat = read_csv(dest_gistemp, skip = 1)
```

    Rows: 1760 Columns: 2
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    dbl (2): Year, Anomaly

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# extract month and clean year data
months = tibble(
    month_num = c(4, 13, 21, 29, 38, 46, 54, 63, 71, 79, 88, 96),
    month = c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12)
)

clean_dat = dat |>
    mutate(
        year_actual = floor(Year),
        month_num = round(100*(Year-year_actual))
    ) |>
    left_join(months, by = "month_num")

clean_dat
```

    # A tibble: 1,760 × 5
        Year Anomaly year_actual month_num month
       <dbl>   <dbl>       <dbl>     <dbl> <dbl>
     1 1880.   -2.61        1880         4     1
     2 1880.   -2.42        1880        13     2
     3 1880.   -1.58        1880        21     3
     4 1880.   -0.64        1880        29     4
     5 1880.    0.36        1880        38     5
     6 1880.    0.93        1880        46     6
     7 1881.    1.23        1880        54     7
     8 1881.    1.18        1880        63     8
     9 1881.    0.51        1880        71     9
    10 1881.   -0.6         1880        79    10
    # ℹ 1,750 more rows

``` r
plt_gistemp = clean_dat |>
    ggplot(aes(month, Anomaly, color = year_actual, group = year_actual)) +
        geom_line() +
        geom_point(data = filter(clean_dat, year_actual==2026), color = "black", size = 0.8) +
        scale_color_gradientn(colors = c("#5264fa", "#3968e6", "#4b9fbe", "#73bd97", "#94bd6b", "#bd9c42", "#e26332", "#b1231f", "#730073")) +
        guides(color = guide_colorbar(reverse=TRUE)) +
        scale_y_continuous(breaks = seq(-4, 3, 0.5), limits = c(-4, 3)) +
        scale_x_continuous(breaks = seq(1, 12, 1), labels = month.abb) +
        labs(
            y = "Temperature Anomaly w.r.t. 1980-2015 (°C)",
            x = "",
            title = "GISTEMP Seasonal Cycle since 1880",
        ) +
        theme_classic() +
        theme(
            legend.position = "inside", legend.position.inside = c(0.03, 0.8), legend.title = element_blank(),
            legend.justification="left", legend.background = element_rect(linewidth = 0.5, colour = "#e0e0e0"),
            plot.title = element_text(size = 11, hjust = 0.5)
        ) +
        annotate("text", x = 8, y = -4, size = 3.5, label = "Seasonal cycle from MERRA2. Figure: NASA/GISS/GISTEMP v4") +
        coord_cartesian(clip = "off")

ggsave("../output/plot_gistemp.png", plot = plt_gistemp)
ggsave("../output/plot_gistemp.pdf", plot = plt_gistemp)
ggsave("tmp/plot_gistemp.png", plot = plt_gistemp, create.dir = TRUE)
```

![](tmp/plot_gistemp.png)
