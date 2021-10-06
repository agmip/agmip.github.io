# ICN_DIST - Initial Soil N distribution function

Given a total inorganic N amount for the soil profile, this function distributes the N over the soil layers assuming a constant concentration of NO3 (90%) and NH4 (10%). 

### Inputs:
* ICIN = Total soil N over the profile (kg[N]/ha)

### Implicit inputs (i.e., available in the data)
* SLLB = array of depths to bottom of soil layers
* SLBDM = bulk density by soil layer (g/cm3)
 
### Outputs:
* ICN_TOT = initial inorganic N by layer (kg[N]/ha)
* ICNO3 = initial nitrate concentration by layer (ppm)
* ICNH4 = initial ammonium concentration by layer (ppm)
 
### Procedure:

1.	Calculate soil layer thicknesses
```Fortran
thick(j) = SLLB(j) - SLLB(j-1), except for first layer thick(1) = SLLB(1)
```
2.	Calculate total inorganic N amount per soil layer (kg/ha)
```Fortran
ICN_TOT = SLBDM * thick * ICIN /  ∑(SLBDM * thick)
```
3.	Calculate total soil N concentration
```Fortran
Nppm = ICIN * 10. / ∑(SLBDM * thick)
```
4.	Calculate ammonium and nitrate concentrations (all layers have same concentration)
```Fortran
ICNH4 = 0.1 * Nppm
ICNO3 = 0.9 * Nppm
```

### Example:
```
FILL, ICIN, ICN_DIST(), 25
```
ICIN = 25 kg[N]/ha

Nppm = 25 / 225.75 * 10.0 = 1.11 ppm

|SLLB (cm)|thick (cm)|SLBDM (g/cm3)|SLBDM * thick (g/cm2)|ICN_TOT (kg/ha)|ICNH4 (ppm)|ICNO3 (ppm)|
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|   15 |   15 |	1.15 |17.25 | 1.91 | 0.11 | 1.00 |
|   60 |	30|	1.21 | 36.3 | 4.02 | 0.11 |	1.00 |
|   30 |	15|	1.16 | 17.4 | 1.93 | 0.11 |	1.00 |
|   30 |	15|	1.16 | 17.4 | 1.93 | 0.11 |	1.00 |
|   90 |	30|	1.23 | 36.9 | 4.09 | 0.11 |	1.00 |
|  120 |	30|	1.31 | 39.3 | 4.35 | 0.11 |	1.00 |
|  150 |	30|	1.31 | 39.3 | 4.35 | 0.11 |	1.00 |
|  180 |	30|	1.31 | 39.3 | 4.35 | 0.11 |	1.00 |
|      |      |225.8 | 25.0 |	   |      |      |
 
### Notes:

If this is a REPLACE operation, then all existing values will be overwritten using the input provided.
 
If this is a FILL operation, and values for ICNO3 and ICNH4 or ICIN or ICN_TOT already exist, then this function should be modified.

#### FILL functions
If the database contains:
* ICIN
  * Use the existing ICIN and calculate other values in the same way	 	 
* ICNO3 and ICNH4 arrays	 
  * ICN_TOT = (ICNH4 + ICNO3) * SLBDM * thick / 10.
  *	ICIN = sum(ICN_TOT)
 	 	 
* ICN_TOT array
  * ICIN = sum(ICN_TOT)
  * ICNH4 & ICNO3 computed as with original function
 
### More Samples:
The following DOME spreadsheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)
