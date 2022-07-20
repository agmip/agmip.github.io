# OM_DIST - Organic matter application details

Organic matter applications include manure, crop residues, etc.

### Inputs:
* pdate_offset =  application date as days before (-) or after (+) planting date (days)
* OMCD = code for type of fertilizer added
* OMC2N = C:N ratio for applied organic matter
* OMDEP = depth at which organic matter is incorporated (cm)
* OMINP = percentage incorporation of organic matter (%)
* DMR = ratio of dry matter to C content (used to calculate %N from C:N ratio)

### Implicit Inputs (i.e., available in the data)
* OM_TOT = total seasonal amount of organic matter applied (kg/ha dry matter)

### Outputs:
* The organic matter application event is updated with missing data.

### Procedure:
1.	Check for organic amendment events.
2.	If any data are missing, fill in using the values provided.
3.	The amount of organic matter applied (OMAMT) must be provided in the data. If it is zero or null, then an event should not be created.
4.	OMN% = 100 / DMR / OMC2N 

### Example:
```
FILL, OMDAT, OM_DIST(), -7, RE003, 8.3, 5, 50, 2.5
```
These data are obtained from the database:
* OM_TOT = 1000 kg/ha (from data object)
* PDATE = "19820312"

The function produces the following organic matter application event: 7 days prior to planting, 1000 kg/ha of manure with a C:N ratio of 8.3 is added to the field; 50% of the manure is incorporated to a depth of 5 cm. N content is calculated to be 4.82%.
```JSON
{
   "event":"organic_matter",
   "date":"19820305",
   "omcd":"RE003",
   "omamt":"1000",
   "omc2n":"8.3",
   "omdep":"5",
   "ominp":"50",
   "omn%":"4.82" 
},
```

### More Samples:
The following DOME spreadsheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)

 
