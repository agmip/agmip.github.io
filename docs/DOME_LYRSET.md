# LYRSET - Soil layer splitting function

This function splits the soil layers in a dataset into homogeneous layers with soil thicknesses which do not exceed limits of drainage models. In general, no interpolation of data values is done, as the original soil properties are assigned to the new multiple layers. The exception is when the top two layers, with assumed thicknesses of 5 and 10 cm, may be interpolated if multiple soil input layers are in this 0-15 cm range.

This function can be used both for soil data and initial conditions data. If the soil layer thickness values are expressed as ICBL, then the soil initial conditions will be modified. If the soil layer thickness values are expressed as SLLB, then soil layer properties will be modified. The function should be used twice if (and only if) initial conditions are provided. 

### Inputs:
* SLLB_new(1) Thickness of top layer (optional)
* SLLB_new(2) Thickness of second layer (optional)

If these are not provided, they are assumed to be 5 cm and 10 cm, respectively.

### Implicit Inputs (i.e., available in the data):
* Array of soil layer properties, including depths to the bottom of each soil layer (SLLB, cm).

### Outputs:
* The modified array of soil layer properties, including depths to the bottom of each soil layer (SLLB_new, cm).

### Procedure:
First, the revised layer depths are computed. The first two layers are forced to be 5 and 15 cm deep, i.e., layer 1 is from the surface to 5 cm and layer 2 is from 5 to 15 cm deep. (The user may choose other depths for these two layers.) 

For the ith layer (where i > 2), we determine the soil layer thickness, SLLB[i] – SLLB[i-1]. A maximum thickness for each layer depends on depth, as shown in the table below. The deeper soil layers are allowed to be thicker.  

| Layer Depth         | PT (maximum layer thickness)      |
| ------------------- | --------------------------------- |
|  0 < SLLB[i] <= 15  | ** see above rules for top layers |
| 15 < SLLB[i] <= 60  | 15 cm                             |
| 60 < SLLB[i] <= 200 | 30 cm                             |
|      SLLB[i] > 200  | 60 cm                             |

If the layer thickness is greater than PT, then the layer is split into 2, 3, or 4 soil layers with identical properties.

Then soil properties are computed. For the top two soil layers, there may be some interpolation required, with all soil properties weighted by soil depth. The table below illustrates how the soil layer refactoring works. In this example, the original soil data included four layers at depths of 7, 27, 60, and 100 cm. The first two layers are reset to 5 and 15 cm depths. The remaining layers are set using the remaining soil layers, but layer thicknesses are controlled.

| Original soil layers | SLLB Original soil layer depth (cm) | T Original soil layer thickness (cm) | A Original soil property (-) | Revised soil layers | SLLB_new Revised soil layer depth (cm) | T_new Revised soil layer thicknesses| A_new Revised soil property|
|-|-|-|-|-|-|-|-|
|1|7|7|A1|1|5|5|A1|
|||||2|15|10|(2*A1+8*A2)/10|
|2|27|20|A2|3|27|12|A2|
|||||4|43.5|16.5|A3|
|3|60|33|A3|5|60|16.5|A3|
|||||6|80|20|A4|
|4|100|40|A4|7|100|20|A4|

### Important:
This method should be called before any other soil layer data related Functions, including but not limited to:

* [ICN_DIST()](DOME_ICN_DIST.md)
* [PCTAWC()](DOME_PCTAWC.md)
* [ROOT_DIST()](DOME_ROOT_DIST.md)
* [STABLEC()](DOME_STABLEC.md)

### Example 1:
```
FILL, SLLB, LYRSET(), 5.0, 10.0
```
 
#### Input:
|SLLB|SLMH|SLLL|SLDUL|SLSAT|SLRGF|SKSAT|SLBDM|SLOC|SLCLY|SLSIL|SLCF|SLNI|SLPHW|SLPHB|SLCEC|SLADC|
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|10|-99|0.098|0.26|0.485|1|14.5|1.29|0.5|14.1|51.9|-99|-99|8.1|1|-99|-99|
|45|-99|0.098|0.248|0.5|0.257|16|1.24|0.4|11.5|53.3|-99|-99|8.1|1|-99|-99|
|75|-99|0.093|0.23|0.516|0.263|23.1|1.22|0.2|10.2|57.7|-99|-99|8.3|1|-99|-99|
|105|-99|0.095|0.235|0.512|0.3|23.1|1.23|0.1|13.5|50.9|-99|-99|8.3|1|-99|-99|
|135|-99|0.098|0.235|0.506|0.3|16|1.23|0.01|8.4|55.4|-99|-99|8.4|1|-99|-99|
|195|-99|0.08|0.22|0.551|0.3|8.2|1.25|0.01|10.3|53.1|-99|-99|8.3|1|-99|-99|
|255|-99|0.083|0.223|0.547|0.3|8.7|1.25|0.01|9.6|52.8|-99|-99|8.3|0.2|-99|-99|

#### Output:
|SLLB|SLMH|SLLL|SLDUL|SLSAT|SLRGF|SKSAT|SLBDM|SLOC|SLCLY|SLSIL|SLCF|SLNI|SLPHW|SLPHB|SLCEC|SLADC|
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|5|-99|0.098|0.26|0.485|1|14.5|1.29|0.5|14.1|51.9|-99|-99|8.1|1|-99|-99|
|15|-99|0.098|0.254|0.493|0.629|15.3|1.26|0.45|12.8|52.6|-99|-99|8.1|1|-99|-99|
|30|-99|0.098|0.248|0.5|0.257|16|1.24|0.4|11.5|53.3|-99|-99|8.1|1|-99|-99|
|45|-99|0.098|0.248|0.5|0.257|16|1.24|0.4|11.5|53.3|-99|-99|8.1|1|-99|-99|
|60|-99|0.093|0.23|0.516|0.263|23.1|1.22|0.2|10.2|57.7|-99|-99|8.3|1|-99|-99|
|75|-99|0.093|0.23|0.516|0.263|23.1|1.22|0.2|10.2|57.7|-99|-99|8.3|1|-99|-99|
|105|-99|0.095|0.235|0.512|0.3|23.1|1.23|0.1|13.5|50.9|-99|-99|8.3|1|-99|-99|
|135|-99|0.098|0.235|0.506|0.3|16|1.23|0.01|8.4|55.4|-99|-99|8.4|1|-99|-99|
|165|-99|0.08|0.22|0.521|0.3|8.2|1.25|0.01|10.3|53.1|-99|-99|8.3|1|-99|-99|
|195|-99|0.08|0.22|0.551|0.3|8.2|1.25|0.01|10.3|53.1|-99|-99|8.3|1|-99|-99|
|235|-99|0.083|0.223|0.547|0.3|8.7|1.25|0.01|9.6|52.8|-99|-99|8.3|0.2|-99|-99|
|275|-99|0.083|0.223|0.547|0.3|8.7|1.25|0.01|9.6|52.8|-99|-99|8.3|0.2|-99|-99|
 
### Example 2:
```
FILL, ICBL, LYRSET()
```

#### Input:
|ICBL|ICH2O|ICNH4|ICNO3|
|-|-|-|-|
|3|0.1|4.5|2.8|
|7|0.2|3.5|4.8|
|15|0.3|3|5|
 
#### Output:
|ICBL|ICH2O|ICNH4|ICNO3|
|-|-|-|-|
|5|0.14|4.1|3.6|
|15|0.28|3.1|4.96|


### More Samples:
The following DOME spreadsheet is using this function.
[Machakos Overlay DOME](https://github.com/agmip/json-translation-samples/blob/master/Maize_Machakos/raw/Field_Overlay-Machakos-MAZ.xlsx?raw=true)

[Dome functions page](DOME_functions.md)

[Home](index.md)

