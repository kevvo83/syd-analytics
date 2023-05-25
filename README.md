# syd-analytics




## Introduction


## Data Preparation

## Import Catchments data into Big Query for Viz

### Step 1. Convert SHP files to GEOJSONNL format

```sh
### Unzip catchments.zip
unzip catchments.zip

### Install NPM module
npm install -g npm@9.6.4

### Run utility to convert the Shapefile (*.shp) to a newline-delimited geojson file
shp2json --newline-delimited catchments_primary.shp -o catchments_primary.geojsonl
shp2json --newline-delimited catchments_secondary.shp -o catchments_secondary.geojsonl
```

### Step 2. Load GEOJSONNL data to BQ Table

```sh
bq --project_id=<gcp project id> load --source_format=NEWLINE_DELIMITED_JSON --json_extension=GEOJSON --autodetect <bq dataset name>.<bq table name> catchments_primary.geojsonl
bq --project_id=<gcp project id> load --source_format=NEWLINE_DELIMITED_JSON --json_extension=GEOJSON --autodetect <bq dataset name>.<bq table name> catchments_secondary.geojsonl
```

## Import Postal Code data into Big Query for Viz

### Source

URL: https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files

Title of link that was downloaded: "Postal Areas - 2021 - Shapefile"

### Step 1. Convert SHP files to GEOJSONNL format

```sh
### Install NPM module
npm install -g npm@9.6.4

### Run utility to convert the Shapefile (*.shp) to a newline-delimited geojson file
shp2json --newline-delimited POA_2021_AUST_GDA94.shp -o POA_2021_AUST_GDA94.geojsonl
```

### Step 2. Load GEOJSONNL data to BQ Table

The data was loaded directly into Big Query using the following command:

```sh
bq --project_id=<gcp project id> load --source_format=NEWLINE_DELIMITED_JSON --json_extension=GEOJSON --autodetect <bq dataset name>.<bq table name> POA_2021_AUST_GDA94.geojsonl
```


## Postal Code vs Locality dataset

### Source

URL: https://www.matthewproctor.com/australian_postcodes

### Step 1. Data Prep

None required

### Step 2. Data Load into Viz

The data was loaded directly into Big Query using the following command:

```sh
bq --project_id=<gcp project id> load --source_format=CSV --autodetect <bq dataset name>.<bq table name> australian_postcodes.csv
```