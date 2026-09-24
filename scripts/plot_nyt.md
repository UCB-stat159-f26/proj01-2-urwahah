# Plot 4 - NYT Global Annual Mean Surface Air Temperature Change
Urwa Irfan
2026-09-24

## Load librares and data

``` r
library(tidyverse)
library(ggplot2)
library(scales)

dest_mean_temp_change = "../data/data_mean_temp_change.csv"
```

``` r
dat = read_csv(dest_mean_temp_change, skip = 1)
```

    Rows: 146 Columns: 3
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    dbl (3): Year, No_Smoothing, Lowess(5)

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## Modify dataset

From the [GISTEMP FAQ](https://data.giss.nasa.gov/gistemp/faq/#q102a):

Q. How can I estimate the anomaly with respect to the ‘pre-industrial’
(1850-1900) period? A. While the GISTEMP analysis only goes back to
1880, there are other estimates that go back further (notably the
HadCRUT, NOAA and Berkeley Earth analyses), and using the average of
those data, we can estimate the correction from our late 19th Century
values (1880-1899), to the earlier baseline. This is a very small
adjustment of about 0.038ºC. Therefore, to calculate the GISTEMP anomaly
with respect to 1850-1900, we can adjust to 1880-1899 from 1951-1980,
and then make that adjustment. *This is equivalent (as of Jan 2025), of
adding ~0.19ºC.* Note that these numbers may change slightly in the
future as more data is digitized or if the methodologies change. Note
also, that anomalies with respect to the pre-industrial are more
uncertain than anomalies w.r.t. a modern baseline.

This does not exactly match the NYT plot, but I’m not sure how their
values were generated and cannot replicate them.

``` r
nyt_dat = dat |>
    filter(Year <= 2018) |> # since the NYT plot stops at 2018
    mutate(No_Smoothing_NYT = No_Smoothing + 0.19)
```

## Create plot

``` r
y_labels = lapply(round(seq(-0.6, 1.2, 0.2), digits = 1), function(x) sprintf("%+2.1f", x))

plt_nyt_mean_temp_change = nyt_dat |>    
    ggplot() +
        geom_hline(yintercept = 0, color = "#cccccc", linewidth = 0.3) +
        geom_line(aes(Year, No_Smoothing_NYT), color = "#909090", linewidth = 0.3) +
        geom_point(
            aes(Year, No_Smoothing_NYT, fill = No_Smoothing_NYT), 
            shape = 21, size = 1.2, color = "#545454", stroke = 0.4
        ) +
        scale_fill_gradientn(
            colors = c("#0387da", "#ffffff", "#e18a61"), # "#9cc7e2"
            rescaler = ~ scales::rescale_mid(.x, mid = 0)
        ) +
        labs(x = "", y = "") +
        theme_light() +
        scale_y_continuous(breaks = seq(-0.6, 1.2, 0.2), limits = c(-0.6, 1.4),
            labels = str_c(y_labels, "°C")) +
        scale_x_continuous(breaks = seq(1880, 2010, 10)) +
        theme(
            legend.position = "none", 
            plot.title = element_text(size = 11, hjust = 0.5),
            panel.grid.minor = element_blank(),
            panel.grid.major.x = element_blank(),
            panel.grid.major.y = element_line(linetype = 3),
            panel.border=element_blank(),
            axis.ticks.y=element_blank(),
            text = element_text(size = 8),
            axis.text = element_text(color = "#999999")
        ) +
        annotate(
            "label", x = 1900, y = 1, hjust = 0, size = 3.5, label = "Rising Global Temperature",
            fontface = 2, fill = "white", linewidth = NA
        ) +
        annotate(
            "label", x = 1900, y = 0.8, hjust = 0, size = 2.5, label = "How much cooler or warmer every year\nwas compared with the average\ntemperature of the late 19th century",
            fill = "white", linewidth = NA
        ) +
        annotate(
            "label", x = 2018, y = 0, hjust = 1, vjust = 1.4, size = 2, label = "COLDER",
            fill = "white", linewidth = NA
        ) +
        annotate(
            "label", x = 2018, y = 0, hjust = 1, vjust = -0.2, size = 2, label = "HOTTER THAN THE\n1880-1899 AVERAGE",
            fill = "white", linewidth = NA
        ) +
        annotate("text", x = 1904, y = -0.3, hjust = 1.2, vjust = 1, label = "1904", size = 2.5) +
        annotate("text", x = 1944, y = 0.4, hjust = -0.1, vjust = -0.3, label = "1944", size = 2.5) +
        annotate("text", x = 1998, y = 0.85, hjust = 1.2, vjust = 1, label = "1998", size = 2.5) +
        annotate("text", x = 2016, y = 1.2, hjust = -0.1, vjust = -0.3, label = "2016", size = 2.5) +
        annotate("text", x = 2018, y = 1.05, hjust = -0.2, vjust = 1, label = "2018", size = 2.5, fontface = 2)

# plt_mean_temp_change

ggsave("../output/plot_nyt_mean_temp_change.png", plot = plt_nyt_mean_temp_change)
ggsave("../output/plot_nyt_mean_temp_change.pdf", plot = plt_nyt_mean_temp_change)
ggsave("tmp/plot_nyt_mean_temp_change.png", plot = plt_nyt_mean_temp_change, create.dir = TRUE)
```

![](tmp/plot_nyt_mean_temp_change.png)
