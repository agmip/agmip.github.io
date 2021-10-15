# NEW_EVENT Function (with CREATE command)

This function will generate a new Event with given information. It MUST be used with the CREATE command.

Currently, the following events are supported.
PLANTING, IRRIGATION, AUTO_IRRIG, FERTILIZER, TILLAGE, ORGANIC_MATTER, HARVEST, CHEMICALS, MULCH

### Inputs:
* DAP = The days after planting date, used for calculating event date
* key (n) = The variable id which is registered in the [ICASA Master Variable List](https://docs.google.com/spreadsheets/d/1MYx1ukUsCAM1pcixbVQSu49NU-LfXg-Dtt-ncLBzGAM/pub)
* value (n) = The variable value. It must be paired with key.

### Implicit Inputs (i.e., available in the data):
* PDATE = The planting date (yyyymmdd)

### Outputs:
* The generated event with given information

### Example1:
```
CREATE, FERTILIZER, NEW_EVENT(), 14, FEAMN, 40, FECD, FE005, FEACD, AP002, FEDEP, 10
```
PDATE = "19820312" in the original data set

The new generated event will be,
```JSON
{"event":"fertilizer", "date":"19820326", "feamn":"40", "fecd":"FE005", "feacd":"AP002", "fedep":"10"}
```

### Example2:

For creating multiple same type events with repeated information, you can create event with only non-repeated variables first, and then use FILL command to fill repeated variable together.
```
CREATE, FERTILIZER, NEW_EVENT(), 14, FEAMN, 40
CREATE, FERTILIZER, NEW_EVENT(), 45, FEAMN, 60
FILL, FECD, FE005
FILL, FEACD, AP002
FILL, FEDEP, 10
```
PDATE = "19820312" in the original data set

The new generated event will be,
```JSON
[
    {"event":"fertilizer", "date":"19820326", "feamn":"40", "fecd":"FE005", "feacd":"AP002", "fedep":"10"},
    {"event":"fertilizer", "date":"19820426", "feamn":"60", "fecd":"FE005", "feacd":"AP002", "fedep":"10"}
]

```

### Example3:

Sample for irrigation event:
```
CREATE, IRRIGATION, NEW_EVENT(), 25, IRVAL, 70, IROP, IR003
```
PDATE = "19820312" in the original data set

The new generated event will be,
```JSON
{"event":"fertilizer", "date":"19820406", "irval":"70", "irop":"IR003"}
```
 
### More Samples:
The following DOME spreadsheet is using this function.
[PADDY Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Rice_PADDY_sample/raw/Field_Overlay1%20-%20piped.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)
