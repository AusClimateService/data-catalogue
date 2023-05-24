# ACS P3 data catalogue - scoping, suggested plan, and demo workflows

The Climate and Hazard Program (P3) of ACS intends to build a data catalogue with the following aims: 

- Make ACS P3 staff more effective by improving the accessibility and clarity of provenance for core internal datasets generated across the institutional partners.
- Help meet requirements for ACS data to comply with FAIR (Findable, Accessible, Interoperable, & Reusable) principles of data management.
- Help meet the recommendations of the 2020 Bushfire Royal Commission ( which have been supported by Government )*

## Bushfire RC reference:

The 2020 Bushfire Royal Commission recommended *( **Recommendation 4.1** – National disaster risk information & **Recommendation 4.2** – Common information platforms and shared technologies )* that “Australian, state and territory governments should prioritise the implementation of harmonised data governance and national data standards ” and “should create common information platforms and share technologies to enable collaboration in the production, analysis, access, and exchange of information, data and knowledge about climate and disaster risks.”

# **What will the catalogue do and for whom?**

The catalogue will initially provide data tools and accompanying tutorial documentation for ACS staff working on Australian NCI resources with Level B: 'shared data' (project ia39), but can offer a template that could be adapted for both Level C: 'public data’ at NCI and other future publicly available data sources.

# Suggested approach

- Build a group of individual `intake-esm` sub-catalogues - one for each “product” / “experiment” / “model” **data source.**
- These sub-catalogues could be built and maintained by data developers using “ESM Catalog Generation tools” aka `ecgtools`.
- A “root” catalogue that will nest all the sub-catalogues to be built using `intake-dataframe-catalog`.
- Build and maintain documentation & workflow demos for users.

## ACS data governance framework

The approach should be informed by the principles that will underpin the ACS data governance framework being developed by the ACS Data Governance Group:

- Principle 1 – Partner agencies remain custodians or stewards of their data and information; and are responsible for governance and data management practices for this information.
- Principle 2 – For information brought together to deliver ACS, a shared approach to information governance and management will be used.
- Principle 3 - Adopt, adapt and where necessary invent.

# Minimum Viable Product

- Two CCAM runs nested into one catalogue - total of **116 TB** of data, **176 unique variables** across **3 time periods** and over **70K netcdf files.**
- Find the 64 specific `netcdf files` corresponding to a specific variable, model, and time period and compute simple seasonal climatology using small resources.
    - Compute using "small" ARE cluster at NCI ( 2 CPU & 9GB RAM ).
    - Cost = 2.5 SUs per hour = 10 cents per hour.
    - Compute time = much much less than an hour - order one minute or less.

## Easily discover some specific data and compute against it with minimal resources

[https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/ACS-catalogue-demo.ipynb](https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/ACS-catalogue-demo.ipynb)

`ACS-catalogue-demo.ipynb` : example workflow that uses nested `intake-esm` catalogues in a root `intake-dataframe-catalog` to search across over 76,000 `netcdf` file paths and 116TB of data from 2 CCAM runs. Demonstrates the basics of searching the root catalogue to find the needed data source and filtering that down to the 64 `netcdf` files required for the variable, type of run, and time period of choice. Using a "small" ARE cluster at NCI ( 2 CPU & 9GB RAM ) we find and load the selected 1.6 GB of data and a few basic calculations and plots are made.

## Build an `intake-esm` sub-catalogue

[https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/build-cat-ccam_noresm2-mm_historical_aus-10i_12km.ipynb](https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/build-cat-ccam_noresm2-mm_historical_aus-10i_12km.ipynb)

[https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/build-cat-ccam_noresm2-mm_ssp126_aus-10i_12km.ipynb](https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/build-cat-ccam_noresm2-mm_ssp126_aus-10i_12km.ipynb)

Example workflows that show how individual sub-catalogues could be built and maintained

## Build a root catalogue to nest the sub-catalogues

[https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/build-ACS-dataframe-cat.ipynb](https://github.com/AusClimateService/data-catalogue/blob/main/notebooks/build-ACS-dataframe-cat.ipynb)

Example workflow that shows how a root ACS catalogue could be built and maintained that nests individual sub-catalogues.

# References:

Repo: [https://github.com/AusClimateService/data-catalogue](https://github.com/AusClimateService/data-catalogue)

`intake`: [https://intake.readthedocs.io/en/latest/](https://intake.readthedocs.io/en/latest/)

`intake-esm`: [https://intake-esm.readthedocs.io/en/stable/](https://intake-esm.readthedocs.io/en/stable/)

`ecgtools`: [https://ecgtools.readthedocs.io/en/latest/](https://ecgtools.readthedocs.io/en/latest/)

`intake-dataframe-catalog`: [https://intake-dataframe-catalog.readthedocs.io/en/latest/](https://intake-dataframe-catalog.readthedocs.io/en/latest/) 

# What are the python tools?

## What is `intake`?

*Taking the pain out of data access and distribution*

Intake is a lightweight package for finding, investigating, loading and disseminating data. It will appeal to different groups, but is useful for all and acts as a common platform that everyone can use to smooth the progression of data from developers and providers to users.

## What is `intake-esm`?

*A data cataloging utility built on top of [intake](https://github.com/intake/intake), [pandas](https://pandas.pydata.org/), and [xarray](https://xarray.pydata.org/en/stable/)*

Computer simulations of the Earth’s climate and weather generate huge amounts of data. These data are often persisted on HPC systems or in the cloud across multiple data assets of a variety of formats ([netCDF](https://www.unidata.ucar.edu/software/netcdf/), [zarr](https://zarr.readthedocs.io/en/stable/), etc…). Finding, investigating, loading these data assets into compute-ready data containers costs time and effort. The data user needs to know what data sets are available, the attributes describing each data set, before loading a specific data set and analyzing it.

Finding, investigating, loading these assets into data array containers such as xarray can be a daunting task due to the large number of files a user may be interested in. Intake-esm aims to address these issues by providing necessary functionality for searching, discovering, data access/loading.

## What is `ecgtools`?

*ESM Catalog Generation tools*

The critical requirement for using `[intake-esm](https://github.com/intake/intake-esm)` is having a data catalog. `ecgtools` package enables you build data catalogs to be read in by `[intake-esm](https://github.com/intake/intake-esm)`, which enables a user to easily search, discover, and access datasets they are interested in using.

## What is `intake-dataframe-catalog`?

*A simple intake plugin for a searchable table of intake sources and associated metadata.*

Intake already provides the ability to [nest sources in a catalog](https://intake.readthedocs.io/en/latest/catalog.html#catalog-nesting) and search across them. However, data discoverability is limited in the case of very large numbers of nested sources, and the search functionality does not readily provide the ability to execute complex searches on nested source metadata. intake-dataframe-catalog aims to provide a very simple catalog of intake sources that emphasises source search and discoverability.
