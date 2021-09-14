# DOME files

Even very detailed datasets often lack complete data for crop model simulation. DOME (Data Overlay for Multi-model Export) files can be used to supply additional information to supplement data collected in a field experiment or farm survey. Use of a DOME does not alter the original dataset. Multiple DOMEs can be combined to create complex scenarios for simulation, making these a powerful tool for generating hypothetical scenarios from real data. 

DOME functions have been developed to allow a modeler to estimate missing modeling inputs such as initial water content, initial N distribution, soil properties, and planting dates.

There are three kinds of DOME files:
* **Field overlay DOMEs** add information to supplement a baseline simulation. These data are used in addition to data collected in the field and are provided solely to complete model input data required for this baseline simulation. 
* **Seasonal Strategy DOMEs** allow a single season of data to be used with multiple years of weather data to analyze scenarios based on seasonal weather variability. These  DOMEs are used in conjunction with Field overlay DOMEs. Additional hypothetical management information may be introduced to mimic adaptations or other scenarios.
* **Batch DOMEs** allow loops of simulations to be done for sensitivity analyses, climate change studies, and other simulation series. 

The various parts of a DOME file are explained below. This is not an exhaustive explanation of all capabilities of DOMEs, but is meant to give the user a feel for the way DOME files are constructed and some of the capabilities.

As an example, we will look at the Field overlay DOME used for the Hot Serial Cereal experiment (Kimball et al., 2016). This is the same experiment described in the ['AgMIP Translators'](AgMIP_translators.md) description. The screenshots are equivalent to the data in the Field_overlay_HSC_v4.5a.csv file, but have been put into an Excel spreadsheet for a simpler view of data definitions. This Field overlay file can be downloaded [**here**](https://github.com/agmip/json-translation-samples/blob/master/Wheat_HSC_SHORT/Field_overlay_HSC_v4.5.zip?raw=true). 

### General notes on the DOME file structure:
* Comments are denoted with '!' and are not processed by the translators. Fields beginning with '!' are ignored. Lines with '!' in column 1 are entirely ignored.
* Lines of data with '&' in column 1 are processed by the translators.
* The second column of every data line contains operators: INFO (for metadata), FILL (to fill in missing values), or REPLACE (to replace all values with the data provided).
* The third column contains the name of the variable being estimated or set by the user.
* The fourth column contains either a value or a function name. 
* All function names include “()” after the function name. Columns 5 through N after a function name contain function parameters. 
* Functions are applied in order, so if variable B depends on variable A, then variable A must be specified prior to variable B. 

### References

Kimball, B.A., J.W. White, G.W. Wall, M.J. Ottman 2016. Wheat Responses to a Wide Range of Temperatures: The Hot Serial Cereal Experiment. In: J. L. Hatfield, D. Fleisher, editors, Improving Modeling Tools to Assess Climate Change Effects on Crop Response, Adv. Agric. Syst. Model. 7. ASA, CSSA, and SSSA, Madison, WI. p. 33-44. [doi:10.2134/advagricsystmodel7.2014.0014](https://doi.org/10.2134/advagricsystmodel7.2014.0014)



[Home](index.md)
