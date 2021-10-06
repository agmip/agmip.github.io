# FERT_DIST - Fertilizer Details

Often the total amount of fertilizer in a growing season has been recorded, but no details of application dates, types of fertilizer,etc. This function allows a user to specify rules for fertilizer application in a region.

### Inputs:
* num = Number of fertilizer applications

#### these data to be applied to all fertilizer events:
* FECD = code for type of fertilizer added
* FEACD = code for fertilizer application method
* FEDEP = depth at which fertilizer is applied (cm)

#### these data are specific to each application: (must have "num" pairs of these data)
* D = date as offset from planting date (days)
* P = proportion of total N added (%)

### Implicit Inputs (i.e., available in the data)
* FEN_TOT = total applied N fertilizer in a season (if FEP_TOT is supplied, the distribution will be for phosphorus fertilizer instead of nitrogen).

### Outputs:
* "N" fertilizer events are added to the JSON object.
 
### Example:
```
FILL, FEDATE, FERT_DIST(), 2, FE005, AP002, 10, 14, 33.3, 45, 66.7
```
These data are obtained from the database:

FEN_TOT = 60 kg[N]/ha (from data object)

PDATE = "19820312"

The function produces the following two urea fertilizer applications at 14 and 45 days after planting, with fertilizer broadcast and incorporated to 10 cm.
```JSON
{                             
 "event":"fertilizer",
 "date":"19820326",
 "fecd":"FE005",
 "feacd":"AP002",
 "fedep":"10",
 "feamn":"20"
},
{
 "event":"fertilizer",
 "date":"19820426",
 "fecd":"FE005",
 "feacd":"AP002",
 "fedep":"10",
 "feamn":"40"
},
```

### More Samples:
The following DOME spreadsheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)
