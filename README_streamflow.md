# Streamflow Data Scripts

## About
This is a collection of Python modules and scripts for downloading and preprocessing streamflow and meteorological time series data. The data comes from a time series web database run by the Grand River Conservation Authority (GRCA).

## Nith River
We've chosen the [Nith River Watershed](https://apps.grandriver.ca/waterdata/kiwischarts/rf_nithriver.aspx) (part of the Grand River Watershed) as a primary data source for this project because
* The watershed is largely uncontrolled (i.e., there are no dams),
* There are five streamflow gauging stations along the length of the river.
* There are hourly streamflow timeseries observations going back to 1999, and
* There are meteorological records (temperature, precipitation rate) available from several nearby stations.

Calling the download scripts will download the five streamflow timeseries files, as well as a bunch of meteorological station datasets. The lat/lon coordinates for each station are listed in `./config/station_metadata.csv`.

Please note the [GRCA's message](https://www.grandriver.ca/en/our-watershed/Provisional-Data.aspx) on the terms of use of the data. Usually hourly data is considered "provisional," meaning it hasn't been QC'd. 

## Usage

### Downloading streamflow data

``` python -m streamflow_data_scripts.scripts.download_streamflow_data ```

The data will be downloaded to `./data/streamflow/` in csv format.

### Combining all time series into single table

After downloading the data, you may want to merge all of the csv time series files into a single hourly data file.

``` python -m streamflow_data_scripts.scripts.aggregate_timeseries ```

This will create the file `hourly.csv` in `./data/preprocessed/`.

Note that there will be significant chunks of missing data in this table. We haven't addressed data infilling/imputation here.

### Explore the data
``` python -m streamflow_data_scripts.scripts.explore_data ```

A few utilities to see what the data looks like.
