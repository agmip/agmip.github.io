# AUTO_REPLICATE_EVENTS Function

This function will clone the original management events for each year in the experiment duration. Only the date of each event will be increased year by year to simulate multiple years. If the experiment duration only 1 year, no generation will be done. 

If this function is used in conjunction with with [AUTO_PDATE()](\DOME_AUTO_PDATE.md), then the generated event dates are based on the generated planting dates and the original days after planting.

### Implicit Inputs (i.e., available in the data)
* EXP_DUR - number of years of simulation
* SC_YEAR - Simulation start year
* Management events

### Outputs:
* New events with corresponding dates for each year
 
### Example 1:
#### !, AUTO_REPLICTE_EVENTS() only
```
&, REPLACE, EXP_DUR, 3
&, REPLACE, SC_YEAR, 1981
&, REPLACE, PDATE, AUTO_REPLICATE_EVENTS()
```

#### Original events:
```JSON
[
    {"event":"planting", "date":"19820226", "crid":"MAZ"},
    {"event":"irrigation", "date":"19820304", "irop":"IR001", "irval":"13"}
]
```

#### Output events:
```JSON
[
    [
        {"event":"planting", "date":"19810226", "crid":"MAZ"}, 
        {"event":"irrigation", "date":"19820304", "irop":"IR001", "irval":"13"}
    ],
    [
        {"event":"planting", "date":"19820226", "crid":"MAZ"}, 
        {"event":"irrigation", "date":"19830304", "irop":"IR001", "irval":"13"}
    ],
    [
        {"event":"planting", "date":"19830226", "crid":"MAZ"}, 
        {"event":"irrigation", "date":"19840304", "irop":"IR001", "irval":"13"}
    ]
]
```

 
### Example 2:
#### language!, AUTO_PDATE() and AUTO_REPLICTE_EVENTS() together
```
&, REPLACE, EXP_DUR, 3
&, REPLACE, SC_YEAR, 1982
&, REPLACE, PDATE, AUTO_PDATE(),0501,0701,25,5
&, REPLACE, PDATE, AUTO_REPLICATE_EVENTS()
```

#### Original events:
```JSON
[
    {"event":"planting", "date":"19820226", "crid":"MAZ"}, 
    {"event":"irrigation", "date":"19820304", "irop":"IR001", "irval":"13"}
]
```

#### Output events:
```JSON
[
    [
        {"event":"planting", "date":"19820515", "crid":"MAZ"}, 
        {"event":"irrigation", "date":"19820521", "irop":"IR001", "irval":"13"}
    ],
    [
        {"event":"planting", "date":"19830606", "crid":"MAZ"}, 
        {"event":"irrigation", "date":"19830612", "irop":"IR001", "irval":"13"}
    ],
    [
        {"event":"planting", "date":"19840526", "crid":"MAZ"}, 
        {"event":"irrigation", "date":"19840601", "irop":"IR001", "irval":"13"}
    ]
]
```

### More Samples:
The following DOME spreadsheet is using this function.

[Seasonal DOME Template](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Seasonal_strategy-Machakos-MAZ-0XFX.xlsx?raw=true) (check the sheet Seasonal_strategy_baseline_2 )

[Dome functions page](DOME_functions.md)

[Home](index.md)
