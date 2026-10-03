\# Automated Forest Indicators for Graubünden



A Python workflow that calculates forest indicators for municipalities in the canton of Graubünden (Switzerland) from the national forest inventory's canopy height model, and shows the results on an interactive map.



\*\*Live map:\*\* https://ellengomes.netlify.app/maps/forest\_indicators\_gr.html



\## What it does



For each selected municipality, the workflow:

1\. clips the 1 m canopy height model to the municipality boundary (only this area is read, so the full Swiss raster is never loaded into memory),

2\. treats every pixel with vegetation ≥ 3 m as tree canopy,

3\. calculates canopy cover (%), forest area (km²), mean forest height (m) and the 90th percentile height (m),

4\. saves the results as GeoPackage and CSV, and creates an interactive Folium map.



\## Results (pilot: 5 municipalities)



| Municipality | Canopy cover (%) | Forest area (km²) | Mean height (m) | 90th percentile (m) |

|---|---|---|---|---|

| Schiers | 43.9 | 27.1 | 19.3 | 30.4 |

| Chur | 42.4 | 34.7 | 16.8 | 27.6 |

| Seewis im Prättigau | 27.8 | 13.8 | 15.6 | 27.6 |

| Val Müstair | 20.0 | 39.6 | 15.1 | 26.7 |

| Davos | 18.3 | 51.8 | 16.4 | 27.4 |



\## Data



| Dataset | Source |

|---|---|

| Vegetationshöhenmodell LFI 2025 (canopy height model, 1 m) | WSL / BAFU, via \[opendata.swiss](https://opendata.swiss/de/dataset/vegetationshohenmodell-lfi) |

| swissBOUNDARIES3D (municipality boundaries) | \[swisstopo](https://www.swisstopo.admin.ch/de/landschaftsmodell-swissboundaries3d) |



The raw data is not included in this repository because of its size.



\## How to run



1\. Create the environment:

conda env create -f environment.yml

conda activate -name of your environment





2\. Download the two datasets and save them in a folder `data\_raw/` as:

&#x20;  - `data\_raw/vegmodell\_inventar2025.tiff`

&#x20;  - `data\_raw/swissborders.gpkg`

3\. Open `notebook/forest\_indicators\_gr.ipynb` in JupyterLab and run all cells.



To analyse other municipalities, change `MUNICIPALITIES\_BFS` in the settings cell. The canopy height threshold can be changed with `FOREST\_THRESHOLD\_M`.



\## Project structure

├── notebook/forest\_indicators\_gr.ipynb analysis notebook

├── outputs/ results (GeoPackage, CSV, HTML map)

├── environment.yml conda environment

└── README.md





\## Limitations



\- Canopy cover is not the official forest area: every pixel with vegetation ≥ 3 m counts, so gaps inside forests count as "no canopy" and single trees outside forests count as canopy.

\- The 3 m threshold is a methodological choice and can be adjusted.

\- Buildings are already excluded in the LFI canopy height model.



\## Tools



Python · rasterio · GeoPandas · NumPy · pandas · Folium



