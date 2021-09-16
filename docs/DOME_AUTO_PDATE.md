# AUTO_PDATE - Automatic Planting Date

Calculates a planting date based on the rainfall record. The planting date is the first date within a planting window that has an accumulated rainfall amount (P) in the previous n days.  This function operates on the number of years to be simulated (EXP_DUR). If EXP_DUR is not in the database, it is assumed to be 1 year.

This function can be used with AUTO_REPLICATE_EVENTS() to replicate all the events with auto-generated event dates.

### Inputs:
* Earliest planting date (mmdd)
* Latest planting date (mmdd)
* P=Threshold rainfall amount (mm)
* n=Number of days of accumulation
 
### Implicit Inputs (i.e., available in the data):
* Weather data
* EXP_DUR - number of years of simulation
* SC_YEAR - starting year for first planting
 
### Outputs:
* PDATE = planting dates (yyyymmdd)
 
### Example:
In a **SEASONAL STRATEGY DOME**, the AUTO_PDATE() function is preceded by statements which set the starting year for the seasonal simulations (SC_YEAR), the number of years of simulation (EXP_DUR) and a function to remove all fixed date events (REMOVE_ALL_EVENTS()). 

In this example, the AUTO_PDATE() function sets the planting date in each year of the simulation at the first date between May 1 and July 31 where 25 mm of rainfall has occurred within the last 5 days. The "REPLACE" operator is used so that the calculated planting date is used in place of the fixed planting dates.

```
&, REPLACE, SC_YEAR, 1980
&, REPLACE, EXP_DUR, 30
&, REPLACE, PDATE, REMOVE_ALL_EVENTS()
&, REPLACE, PDATE, AUTO_PDATE(), 0501, 0731, 25, 5
```

In a **FIELD OVERLAY DOME**, the AUTO_PDATE() function is preceded by the year for which the simulation is being done. The "FILL" operator is used so that the function is only used if an observed planting date was not recorded in the survey data.

```
&, FILL, SC_YEAR, 1998
&, FILL, PDATE, AUTO_PDATE(), 0501, 0731, 25, 5
```

### NOTES:
* If EXP_DUR is set to multiple years, a planting date is calculated for each year.

* The starting year for multiple year runs may be set with SC_YEAR.

* If no starting year is provided, the multiple years will begin on the first available weather year.

* If only one year is to be simulated, the recorded planting date year will be used (if available).

### More Samples:
The following DOME spreadsheet uses this function:
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)


[Dome functions page](DOME_functions.md)

[Home](index.md)