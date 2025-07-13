# mosquito-host-alluvial
Instructions for creating an alluvial plot in R from mosquito-host dataset csv file.

# Mosquito-Host Alluvial Plot RStudio

This guide explains how to create an alluvial plot in R using mosquito-host interaction data.


## Step 1: Prepare Your Data

1. Create a CSV file (e.g., `mosquito_data.csv`) with two columns:  
   **Mosquito.Species** and **Host.Species**

2. Upload it to your RStudio working directory.


## Step 2: Load the Data in R

```r
mosquito_data <- read.csv("mosquito_data.csv", stringsAsFactors = FALSE)
'''

## Step 3: Install packages

'''r
install.packages("ggalluvial")

install.packages("ggplot2")

library(ggplot2)

library(ggalluvial)
'''

## Step 4: Load file into R

'''r
mosquito_data <- read.csv("mosquito_data.csv", stringsAsFactors = FALSE)
'''

## Step 5: Group Data

```r
library(dplyr)
flow_data <- mosquito_data %>%
  group_by(Mosquito.Species, Host.Species) %>%
  summarise(Frequency = n()) %>%
  ungroup()
```

## Step 6: Create Alluvial Plot

'''r
ggplot(flow_data,
       aes(axis1 = Mosquito.Species, axis2 = Host.Species, y = Frequency)) +
  geom_alluvium(aes(fill = Mosquito.Species), width = 1/12) +
  geom_stratum(width = 1/12, fill = "gray", color = "black") +
  geom_text(stat = "stratum",
            aes(label = after_stat(stratum)),
            size = 3) +  # <-- smaller labels
  scale_x_discrete(limits = c("Mosquito Species", "Host Species"), expand = c(.05, .05)) +
  labs(title = "Mosquito-Host Associations",
       y = "Frequency") +
  theme_minimal()
'''
