# PTCALC - Calculating soil parameters based on given soil data

This function uses some standard pedotransfer functions to calculate missing soil parameters. By loading different calculation theory, this function could calculate the soil parameters based on the existed variables in the given data.

### Inputs:
* Calculation theory name - tell the function which theory will be applied for calculation. Currently, only the following pedotransfer functions are available.

|Calculation theory |Description|
|-|-|
|PTSaxton2006|Implementation based on the paper *[Soil Water Characteristic Estimates by Texture and Organic Matter for Hydrologic Solutions, by K. E. Saxton and W. J. Rawls, 2006](https://hrsl.ba.ars.usda.gov/SPAW/Soil%20Water%20Characteristics-Paper.pdf)*|

* List of variables name - tells the function which variable will be the target of calculation. If provide key word "ALL", will automatically calculate all the possible variables in the implementation of the selected theory.
 
### Implicit Inputs (i.e., available in the data):
Depends on selected calculation theory as follow,
|Calculation theory |Input arguments|
|-|-|
|PTSaxton2006|SLSND - Soil texture, sand (0.05 to 2.0 mm), weight percent of fine earth (%)|
||SLCLY - Soil texture, clay (<0.002 mm), weight percent of fine earth (%)|
||SLSIL - Soil texture, silt (0.05 to 0.002 mm), weight percent of fine earth (%)|
||SLCF - Soil texture, coarse fraction (>2 mm), weight percent of fine earth (%)|
||SLOC - Total soil organic carbon by layer (g[C]/100g[soil])|
 
### Outputs:
Depends on selected calculation theory as follow,
|Calculation theory|Possible output variables|
|-|-|
|PTSaxton2006|SLLL - Soil water, lower limit (%)|
||SLDUL - Soil water, drained upper limit (%)|
||SLSAT - Soil water, saturated (%)|
||SKSAT - Saturated hydraulic conductivity (cm/h)|
||SLBDM - Soil bulk density when moist for layer (g/cm3)|

### Procedure:
Please refer to the corresponding paper or check the attached calculation sample spreadsheet as reference.

[PTSaxton2006_CalculationSample.xls](attachments/PTSaxton2006_CalculationSample.xls?raw=true)

In addition, if SLSND is missing in the data set, will use SLSND = 100 - (SLCLY  + SLSIL) to calculate SLSND.
 
### Example 1:
```
FILL, SLLB, PTCALC(), PTSaxton2006, ALL
```
This will calculate all the possible variables for each layer, include SLLL, SLDUL, SLSAT, SKSAT and SLBDM, and fill the value in the layer when there is missing data.
 
### Example 2:
```
REPLACE, SLLB, PTCALC(), PTSaxton2006, SLLL, SLDUL
```
This will calculate the SLLL and SLDUL for each layer and replace the original value anyway.
 
### More Samples:
The following DOME spread sheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)