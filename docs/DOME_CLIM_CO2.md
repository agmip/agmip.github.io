# CLIM_CO2() - climate scenario relink function
Associate a CO2 value with a climate scenario to be simulated. This function is typically used within a Batch DOME to define for future climate scenarios.

### Inputs:
* CO2 concentration, annual (ppm)
* Climate scenario identification (code)

### Implicit Inputs (i.e., available in the data):
* weather data

### Outputs:
* The function is a linkage function that replaces the historical weather data with a future scenario and defines the CO2 concentrations to be used in simulations.
 
### Example:
#### For baseline weather, use code: 0XFX and update CO2 to 380 ppm
```
&, REPLACE, CO2, CLIM_CO2(), 0XFX, 380
```

### More Samples:
 This new function is recommended to be used with batch feature of QuadUI. You can check the sample batch DOME file for this function by click [HERE](https://github.com/agmip/json-translation-samples/blob/master/Templates/Batch/Batch_DOME_working%20file.xlsx?raw=true).

[Dome functions page](DOME_functions.md)

[Home](index.md)
