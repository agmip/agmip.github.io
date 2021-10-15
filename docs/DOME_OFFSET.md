# OFFSET, OFFSET_DATE and DATE_OFFSET functions

Simple function to offset a value by a constant.

### Inputs:
* y - starting value
* x - offset amount

### Outputs:
* Final value = y + x

### Example:
```
FILL, FEDATE, OFFSET_DATE(), $PDATE, 14
```
Sets the fertilizer application date to 14 days after planting.

#### Note:
DATE_OFFSET and OFFSET_DATE are the same function and can be used interchangeably.

### More Samples:
The following DOME spreadsheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)

