# TRANSPOSE - Insert array value

Fill/Replace the values for a variable located in an array structure. 

If the input array size does not match the array size in the data set, the function will
1. If there are more input records than the model array size of N (e.g., soil layers), apply only the first N records to the array.
2. If there are fewer input records than the model array size, the function will apply the provided values to the first N array elements, where N is the number of records.

### Inputs:
Value 1, Value 2, ...

### Outputs:
N/A

### Example:

``` 
 &, FILL, SLDUL, TRANSPOSE(), 0.15, 0.12, 0.13
``` 

which would then apply these values to the DUL per soil layer.
Soil Layer 1, SLDUL = 0.15
Soil Layer 2, SLDUL = 0.12
Soil Layer 3, SLDUL = 0.13

### More Samples:
 The following DOME spreadsheet uses this function:
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)


[Home](index.md)