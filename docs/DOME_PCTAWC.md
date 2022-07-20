# PCTAWC - Percent available water

Calculates the soil water volumetric content for an array of soil layers based on a user-provided percent available water.

### Inputs:
* ICSW% = initial soil water content expressed as percent of available water (%)
* Implicit Inputs (i.e., available in the data):
* SLLL = array of soil layer lower limit (mm3/mm3)
* SLDUL = array of soil layer drained upper limit (mm3/mm3)

### Outputs:
* ICH2O = array of final soil water content by layer (mm3/mm3)

### Procedure:
```Fortran
ICH2O(j) = SLLL(j) + ICSW%/100. * (SLDUL(j) - SLLL(j))
```

### Example:
```
FILL, ICH20, PCTAWC(), 50
```
Sets initial soil water content at 50% of available water capacity.

### More Samples:
The following DOME spreadsheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)

 


