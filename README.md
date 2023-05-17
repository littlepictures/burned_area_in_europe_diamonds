# CLIP - Fire Bubbles

## Background on this CLIP
This repository contains a Jupyter notebook that analyzes the Fire_CCI Burned Area data for European countries. The data represents the area of land that has been burned due to wildfires, and these measurements are taken from the MODIS instrument. It creates a bubble plot visualization that enables the viewer to interpret fire location and intensity over time.

## Data Sources

The CLIP uses the following datasets:

- [ESA Fire CCI: MODIS Fire_cci Burned Area Pixel product, version 5.1](https://catalogue.ceda.ac.uk/uuid/58f00d8814064b79a0c49662ad3af537), 
  Cate dataset identifier: `esacci.FIRE.mon.L4.BA.MODIS.Terra.MODIS_TERRA.v5-1.grid`.
- [cate.ds.data.countries/countries-110m.geojson](https://github.com/CCI-Tools/cate/blob/master/cate/ds/data/countries/countries-110m.geojson) 
  country polygons provided as public domain from [Natural Earth](https://www.naturalearthdata.com/).

## Data Preparation
### Description

Data preparation comprises the following steps:

* Opening the Fire CCI dataset `esacci.FIRE.mon.L4.BA.MODIS.Terra.MODIS_TERRA.v5-1.grid`.
* Opening the countries GeoJSON dataset `cate.ds.data.countries/countries-110m.geojson` 
* Select European countries Features from countries dataset.
* Use European countries to spatially subset the Fire dataset.
* Generate annual sums of burned areas of the Fire dataset.
* Group the annual Fire dataset by country codes.
* Generate the sums of burned areas for each country.
* Put burned area sums in a data frame and save a CSV files 
  `data/ba-europe-countries.csv` and the cumulative sums in 
  `data/ba-europe-countries-cumsums.csv`. The units are square meters.

### One-time script setup

If you do not have a Cate account yet, please visit [Cate App](https://cate.climate.esa.int/), select **Cate Cloud Service** and register. 
Using the Cate credentials, login to the [Cate JupyterLab](https://cate-lab.brockmann-consult.de/). 
From the JupyterLab's **Launcher**, open a **Terminal** window and type

```bash
cd ~/work
git clone https://github.com/trevalabs/pytrevalabs.git
git clone https://github.com/trevalabs/clip_05_burning_lands.git
```

Note you can also use the JupyterLab's **Git** extension (left side bar) to clone the repos.

### Running the script

In JupyterLab's **File Browser** navigate to `/clip_05_burning_lands/scripts/dataprep` and open
the Notebook [extract-burned-areas.ipynb](scripts/dataprep/extract-burned-areas.ipynb) and run it.

To stay in sync with the repos, open a **Terminal** window and

```bash
cd ~/work/pytrevalabs
git pull --rebase
cd ~/work/clip_05_burning_lands
git pull --rebase
```

Note you can also use the JupyterLab's **Git** extension (left side bar) to update the repos.

## Creating Visualizations
- Load the data from the CSV file 'ba-europe-countries.csv' into a pandas DataFrame.
- Drop certain countries (Europe, Belarus, Ukraine, and Luxembourg) from the DataFrame due to their disproportionate sizes.
- Melt the DataFrame from a wide format to a long format to simplify the visualization process.
- Calculate the sum of the burned area per year across all countries and per country over all years. Save the sum per country to a new CSV file.
- Merge the original DataFrame with the newly calculated sums, and calculate the yearly share of the burned area for each country based on the total burned area.
- Merge the DataFrame with another DataFrame containing average latitude information for each country.
- Define a color scale for the visualization.
- Create an Altair chart where the x-axis represents the year, the y-axis represents the countries (sorted by latitude), and the size of each marker represents the burned area in a given year.
- The color of each marker represents the total burned area in Europe for a given year, providing a sense of the severity of wildfires in that year.
- The chart is then configured and displayed, visualizing the trend of burned areas in various European countries over the years.
- Finally, a similar chart is created but with diamond-shaped markers, offering another perspective on the data.

## CREDITS & LICENSE
- Idea by: [INSTITUTION](https://climate.esa.int/)
- Processing Scripts by: [INSTITUTION](https://climate.esa.int/)
- Visualization by: [INSTITUTION](https://climate.esa.int/)

The code in this repository is published under [CC BY-SA 4.0 license](https://creativecommons.org/licenses/by-sa/4.0/)
