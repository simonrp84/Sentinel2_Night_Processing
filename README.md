# Sentinel-2 Night Processing
A repository containing the scripts used to process the December 2025 S2A night acquisitions from L1B into geolocated, calibrated and aggregated per-band radiance images.

Please note: These scripts were intially intended for internal use only, and are therefore not fully commented or robust for use across multiple platforms or systems. Pull requests and issues are welcome to help make these scripts more useful.

# Overview
These scripts transform Sentinel-2 Level-1B data into orthorectified, calibrated, data of similar quality to the widely-used Level-1C datasets. These scripts, however, resample data onto a custom grid defined to fit the geometry of each image, rather than onto a pre-defined tiling grid like is done for the L1C products. While these scripts were designed for processing data from the Sentinel-2A night acquisition campaign, they will also work with any other S2A L1b data and, with modifications, also with S2B and S2C.

# Workflow

The three notebooks should be run in order, and external processing using text files written by the notebooks is also required. You need to have both docker and gdal installed on your machine for this processing to be successful. For a description of how docker is used, please see [the documentation of the Sen2VM tool](https://github.com/sen2vm/sen2vm-core/blob/main/documentation/Usage/HOWTO.md#2-how-to-run-within-a-docker).

The processing steps are fairly manual, and could be optimised. In short:
1. Run the `Step_4_1_Geolocation.ipynb` notebook.
2. Run the `{WORKDIR}/docker_run` file.
3. Run the `Step_4_2_Resampling.ipynb` notebook.
4. Run the `{idir}/runner_gdal` file.
5. Run the `Step_4_3_4_Calibrate_Merge.ipynb` notebook.

For each L1b granule, the output, in the form of a single, calibrated and orthorectified, image for each band, will be stored in a `mosaic` subdirectory.
