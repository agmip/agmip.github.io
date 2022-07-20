# SHIFT_EVENTS - recalculates management event dates based on planting date offset

This function takes dates from events in the survey file and shifts the dates relative to planting date. There are two forms of the function:
* RELATIVE shifts the planting date by a fixed number of days, specified by the user
* ABSOLUTE sets the planting date to a fixed date.

In both cases, dates for all other management events are calculated based on the original days after planting from the original (survey) data.

``` 
REPLACE, PDATE, SHIFT_EVENTS(), RELATIVE, 5
REPLACE, PDATE, SHIFT_EVENTS(), ABSOLUTE, 2014-05-15
```

[Dome functions page](DOME_functions.md)

[Home](index.md)


