# AUTO_IDATE - Automatic Irrigation Date

Calculates the irrigation dates based on the cumulative growing degree days (GDD). Each irrigation event occurs when a target GDD (C) is accumulated. 
The function assumes that the default irrigation operation code IR001. This code could be replaced with other value by add additional DOME command (example #2)
GDD Calculation sample can be found here.

### Inputs:
* Number of irrigation events
* Base temperature for calculating Growing Degree Day (C) 
* Target GDD for #1 irrigation (C-d) 
* List of irrigation amount (IRVAL) for #1 irrigation (mm)
* Target GDD for #2 irrigation (C-d) 
* List of irrigation amount (IRVAL) for #2 irrigation (mm)
* ...
* Target GDD for #n irrigation (C-d) 
* List of irrigation amount (IRVAL) for #n irrigation (mm)

#### Implicit Inputs (i.e., available in the data):
* Weather data
* Planting date
 
### Outputs:
* List of irrigation events
 
## Procedure:
 
``` 
 /* Loop the daily weather data to calculate GDD */ 
 j = 0
 sumGdd = 0
 Loop i from PDATE to last day of weather
   gdd = average(TMAX[i], TMIN[i]) - baseTemperature
   If gdd > 0
     sumGdd += gdd
   End If   
   /* If the cumulative GDD is no less than target value,
      then let the date be the IDATE and reset the sum to calculate the next IDATE */
   If sumGdd >= GDD[j]
     CreateIrrigationEvent(W_DATE[i], IRVAL[j], "IROO1")
     sumGdd = 0
   End If
 End Loop
``` 
 
Calculation might fail if there is insufficient daily weather data. In that case, the function will only generate the irrigation events as possible with the provided weather data.
 
## Examples:
**Example #1** Two irrigation events are added to a dataset.

```
&, FILL, IDATE, AUTO_IDATE(), 2, 5, 400, 40, 160 50
```

This will add two irrigation events in the data set as follows, (calculated date depends on weather data):

```
[{"event"="irrigation", "date"="19800405", "irval"="40", "irop"="IR001"},
{"event"="irrigation", "date"="19800505", "irval"="50", "irop"="IR001"}]
```
 
**Example #2** Generate two irrigation events with IR004 (Sprinkler) operation code

```
&, FILL, IDATE, AUTO_IDATE(), 2, 5, 400, 40, 160 50
&, REPLACE, IROP, IR004
```

The output is as follows:

```
[{"event"="irrigation", "date"="19800405", "irval"="40", "irop"="IR004"},
{"event"="irrigation", "date"="19800505", "irval"="50", "irop"="IR004"}]
```
 
**Example #3** Replace original irrigation events with new generated irrigation events

```
&, REPLACE, IDATE, AUTO_IDATE(), 2, 5, 400, 40, 160 50
```

**More Samples:**
The following DOME spreadsheet uses this function:
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)


[Home](index.md)