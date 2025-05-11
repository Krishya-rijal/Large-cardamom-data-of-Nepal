# 📊 Large Cardamom Production Analysis in Nepal (1994–2023)

This R script visualizes trends in **large cardamom production**, **productive area**, and **yield** in Nepal from 1994 to 2023 using a dual-axis bar and line chart.

---

## 📁 Files

- `large_cardamom_plot.R`: R script to read, reshape, and visualize the data.
- `Year wise value of LC in Nepal.xlsx`: Excel file containing year-wise data on production, area, and yield. *(Optional — include if you wish to share raw data)*

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
Script:

```r
library(tidyverse)
library(ggplot2)
library(readxl)

#Loading ecxel from my computer
LC <- read_excel("C:\Users\Admin\Desktop\Year wise value of LC in Nepal")
#Commuting max values
max_prod <- max(LC$production)
max_yield <- max(LC$yield)

#Reshaping the data
lc <- LC %>% 
  pivot_longer(cols = 2:3,
               values_to = "value",
               names_to = "variable")

#Create plot
LC %>% 
  ggplot() +
  theme_set(theme_bw()) +		                #Sets default theme
  geom_bar(data = lc,			                #Creates bar for production and productive area side by side
           mapping = aes(Year, value, fill = variable),
           stat = "identity",  position = "dodge", alpha = 0.5) +
  geom_point(data = LC,			              #Add a layer of scaled yield point using secondary y-axis
             mapping = aes(Year, yield * (max_prod / max_yield), color = "yield"),
             alpha = 0.5, size = 2) + 
  geom_line(data = LC,			              #Add a layer of scaled yield line using secondary y-axis
            mapping = aes(Year, yield * (max_prod / max_yield), color = "yield"),
            size = 1,  group = 1, alpha = 0.5) +
  scale_y_continuous(name = "Productive Area (ha) % \n Production (Mt)",	#Sets up left y-axis for                                                                        #production and productive area                                                                         #and right y-axis for yield 
                     sec.axis = sec_axis(~ . / (max_prod / max_yield),
                                         name = "Yield (kg/ha)",
                                         breaks = seq(100, 800, 100))) +
  labs( title = "Production, Productive Area and Yield of \nLarge cardamom in Nepal (1994-2023)",	
        fill = "",                                    ##Adds title and labels
        color = "") +
  theme(axis.text.x = element_text(angle = 45,		#Customization of theme
                                   hjust = 1,
                                   vjust = 1,
                                   face = "bold",
                                   color = "black")) +
  theme(axis.text.y = element_text(face = "bold",
                                   color = "black")) +
  theme(axis.title.x = element_text(face = "bold",
                                    color = "black",
                                    size = 10)) +
  theme(axis.title.y = element_text(face = "bold",
                                    color = "black",
                                    size = 10)) +
  theme(plot.title = element_text(size = 12,
                                  hjust = 0.5,
                                  face = "bold",
                                  color = "black")) +
  theme(legend.text = element_text(face = "bold")) +
  scale_fill_manual(
    values = c("production" = "blue", "productive area" = "gray"),		#Sets color and labels of                                                                             					#production, productive area 
    labels = c("production" = "Production (Mt)", 
	     "productive area" = "Productive Area (ha)")) +
  scale_color_manual(                                                #Sets color and label of yield
    values = c("yield" = "black"),
    labels = c("yield" = "Yield (kg/ha)"))



Result:
         ![Trend of Large cardamom in Nepal]

			************https://github.com/user-attachments/assets/0568a1a5-792b-455f-b142-a6ddf0c43640************
