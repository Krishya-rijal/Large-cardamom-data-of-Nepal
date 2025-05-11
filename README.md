# 📊 Large Cardamom Production Analysis in Nepal (1994–2023)

This R script visualizes trends in **large cardamom production**, **productive area**, and **yield** in Nepal from 1994 to 2023 using a dual-axis bar and line chart.

---

## 📁 Files

- `large_cardamom_plot.R`: R script to read, reshape, and visualize the data.
- `Year wise production of LC.xlsx`: Excel file containing year-wise data on production, area, and yield. *(Optional — include if you wish to share raw data)*

---

## 📌 Visualization Features

- **Bar plots** for:
  - Production (in metric tons)
  - Productive area (in hectares)
- **Line and point plot** for:
  - Yield (in kg/ha), scaled to match the primary y-axis
- **Dual y-axes**:
  - Left: Production and Area
  - Right: Yield
- Custom **legend**, **themes**, and **axis formatting** for publication-ready output.

---

## 📦 Dependencies

This project uses the following R packages:

```r
library(tidyverse)
library(ggplot2)
library(readxl)


