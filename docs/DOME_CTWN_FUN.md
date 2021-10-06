# CTWN_FUN() - simple change on data for sensitivity analysis
Provide the changes on carbon dioxide concentrations, temperature, precipitation and nitrogen to a selected weather scenario record.

It will typically be used for [C3MP sensitivity analysis](https://research.agmip.org/pages/viewpage.action?pageId=6029905) and CTWN sensitivity analysis.

### Inputs:
* CO2 concentration, annual (ppm), value for replace, optional
* Temperature of air, maximum (oC), value for add, optional
* Temperature of air, minimum (oC), value for add, optional
* Rainfall, including moisture in snow, in one day (mm), value for multiply, optional
* Nitrogen, total amount over season (kg/ha), value for  replace, optional
* Climate scenario identification (code), optional.

### Implicit Inputs (i.e., available in the data):
* weather data
 
### Outputs:
* The model translator will generate modified weather data based on the original data, and modify the fertilizer amount for nitrogen if provided.
 
### Example:
#### Example 1:
The following command replaces the atmospheric CO2 concentration with a value of 360 ppm and fertilizer nitrogen amount for the season is replaced with a value of 30 kg/ha:
```
&, REPLACE, CO2Y, CTWN_FUN(), 360,,,,30,S201
```
   where the S201 is used to as denote this as CTWN sensitivity element 1. (AgMIP CTWN protocols use climate IDs of S201 through S232.)

----------
#### Example 2:
The second example is for a C3MP sensitivity analysis where CO2 concentration is set to 418 ppm, minimum and maximum daily temperatures are increased by 0.7 degrees C, and rainfall is reduced to 83% of recorded values:
```
&, REPLACE, CO2Y, CTWN_FUN(), 418,0.7,0.7,0.83,S101
```
where the S101 is used to as denote this as C3MP sensitivity element 1. (AgMIP C3MP protocols use climate IDs of S101 through S199.)

### More Samples:
 This function is used with Batch Domes. You can check the sample batch file for this function by clicking [HERE](https://github.com/agmip/json-translation-samples/blob/master/Templates/Batch/Batch_Sensitivity.xlsx?raw=true).


[Dome functions page](DOME_functions.md)

[Home](index.md)
