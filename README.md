Geographic Data Science Lab: LSOA Spatial Analysis

A GeoPandas pipeline that links point data to ONS 2021 LSOA boundaries (England & Wales) and produces a neighbourhood-level dataset and map.

What it does

	1.	Cleans the point data: drops missing or non-numeric coordinates, points outside England & Wales, and duplicates
	2.	Reprojects both layers to British National Grid (EPSG:27700), so areas and distances are in metres
	3.	Spatial join: assigns each point to the LSOA it falls within
	4.	Aggregates to a count and density (per km²) for each LSOA
	5.	Validates the result: unique LSOA codes, point totals that reconcile, and the match rate
	6.	Outputs lsoa_metrics.csv, lsoa_metrics.gpkg and lsoa_map.png (a quantile choropleth)

Data

	•	LSOA 2021 boundaries (BSC): ONS Open Geography Portal
	•	Any CSV of points with longitude/latitude, e.g. police.uk street crime

Usage

pip install geopandas pandas matplotlib mapclassify
python lsoa_spatial_starter.py --lsoa lsoa_2021.gpkg --points points.csv \
       --lon Longitude --lat Latitude --region Liverpool --out results

Option	Description
--lsoa	LSOA boundaries (.gpkg / .geojson / .shp)
--points	CSV of points
--lon, --lat	Names of the coordinate columns
--region	Optional filter on LSOA name (e.g. Liverpool)
--out	Output folder (default results)
-v	Show the full traceback when something fails

Error handling

Gives a clear message for missing or empty files, missing columns, swapped lon/lat, a region that matches no LSOAs, a spatial join with no matches, and output folders that can't be written to.

Exit codes: 0 success · 1 data error · 2 missing dependency · 3 output error

Next step

Extend the pipeline from points to shoreline change: calculate erosion and accretion rates along coastal transects and aggregate them to coastal LSOAs.