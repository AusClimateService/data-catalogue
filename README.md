# data-catalogue
Documentation, code, and discussion for scoping a plan to deliver an ACS intake data catalogue.

### What is here?
This repository provides guidance for the steps required to deliver an ACS intake data catalogue.

#### notebooks folder

- `ACS-catalogue-demo.ipynb` : example workflow that uses nested `intake-esm` catalogues in a root `intake-dataframe-catalog` to search across many 10's of thousands of `netcdf` file paths and 116TB of data from 2 CCAM runs.  Demonstrates the basics of searching the root catalogue to find the needed data source and filtering that down to the 64 `netcdf` files required for the variable, type of run, and time period of choice.  Using a "small" ARE cluster at NCI ( 2 CPU & 9GB RAM ) we find and load the selected 1.6 GB of data and a few basic calculations and plots are made.
