# How to create a DOME file

DOME files - A DOME (Data Overlay for Multi-model Export) file supplies additional information to supplement data collected in a field experiment. Addition of DOME data does not alter the original dataset and multiple DOMEs can be combined to create complex scenarios for simulation. 

DOME functions are available (see http://research.agmip.org/display/itwiki/The+DOME) to estimate modeling inputs such as initial water content, initial N distribution, and planting date.

There are three kinds of DOME files:
* Field overlay DOMEs add information to supplement a baseline simulation. These data are used in addition to data collected in the field and are provided solely to complete model input data required for this baseline simulation. 
* Seasonal Strategy DOMEs allow a single season of data to be used with multiple years of weather data to analyze scenarios based on seasonal weather variability. These  DOMEs are used in conjunction with Field overlay DOMEs. Additional hypothetical management information may be introduced to mimic adaptations or other scenarios.
* Batch DOMEs allow loops of simulations to be done for sensitivity analyses, climate change studies, and other simulation series. 
The various parts of a DOME file are explained below. This is not an exhaustive explanation of all capabilities of DOMEs, but is meant to give the user a feel for the way DOME files are constructed and some of the capabilities.
As an example, we will look at the Field overlay DOME used for the Hot Serial Cereal experiment, described in the previous section. The screenshots are equivalent to the data in the Field_overlay_HSC_v4.5a.csv file, but have been put into an Excel spreadsheet for a simpler view of data definitions.

General notes on the DOME file structure:
* Comments are denoted with '!' and are not processed by the translators. Fields beginning with '!' are ignored. Lines with '!' in column 1 are entirely ignored.
* Lines of data with '&' in column 1 are processed by the translators.
* he second column of every data line contains operators: INFO (for metadata), FILL (to fill in missing values), or REPLACE (to replace all values with the data provided).
* The third column contains the name of the variable being provided.
* The fourth column contains either a value or a function name. 
* All function names include “()” after the function name. Columns 5 through N after a function name contain function parameters. 
* Functions are applied in order, so if variable B depends on variable A, then variable A must be specified prior to variable B. 

## Metadata section
The metadata section at the top of every DOME file contains the full description of the scenario being modeled. This section is used by AgMIP Regional Integrated Assessment Teams to carry consistent metadata throughout workflows to provide provenance to final model outputs. Fields that are not relevant to a simulation may be left blank, but as a minimum, the DOME region identification (REG_ID) must be filled.

| ! | Comment | Dome_Name          | HSC-----FIELD | ! Auto-generated from following 6 fields.
| & | INFO    | REG_ID	HSC        |               | ! Region ID
| & | INFO    | Stratum            |               | ! Socioeconomic or geographic stratum ID
| & | INFO    | RAP_ID             |               | ! Representative Agricultural Pathway (RAP) ID
| & | INFO    | MAN_ID             |               | ! Management or scenario ID
| & | INFO    | RAP_VER            |               | ! RAP version
| & | INFO    | DESCRIPTION	FIELD  |               | ! Description of scenario


[Home](index.md)