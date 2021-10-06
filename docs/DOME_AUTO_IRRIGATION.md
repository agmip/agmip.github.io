# Automatic irrigation
Many models have internal procedures for computing irrigation based on dynamic soil water deficit. The APSIM and DSSAT translators can provide two input parameters to the models which can be used to trigger an automatic irrigation event. These two parameters are: management depth (cm) and threshold soil water deficit (percent of available water). If **both** of these parameters are included in the data, DSSAT and APSIM models will use them to set automatic irrigation for the simulation. There is no DOME function associated with this feature, but rather, the irrigation events are computed dynamically by the models based on the user input values of IRMDP and IRTHR.

### Inputs:
* IRMDP = management depth (cm) to computer soil water deficit
* IRTHR = threshold percentage of available soil water to trigger irrigation event (%)

### Modeling Procedure:
```Java
// Calculate water deficits over top irmdp depth of soil (cm)
  cumdep = 0.0;
  current_sw = 0.0;
  pot_sw = 0.0;

  for (int i = 0; i < NumberOfLayers; i++)
  {
    if (cumdep > irmdp) break;          // you’re done, get out of the loop 
    cumdep = cumdep + LayerThickness[i] / 10.0; // accumulate soil depth, convert units to cm

    if (cumdep < irmdp)                 // both are in cm         
      layerFrac = 1.0;   // use the entire layer, it’s less than the management depth
    else         
      layerFrac = 1.0 - (cumdep - irmdp) / LayerThickness[i]; // use only partial layer 
       
    current_sw = current_sw + (SW_mm[i] - LL_mm[i]) * layerFrac; //accumulate actual SW in mm 
    pot_sw = pot_sw + (DUL_mm[i] - LL_mm[i]) * layerFrac;  // accumulate potential SW in mm
  }

  PctAvailWater = current_sw / pot_sw * 100.;  // this is current soil water as percentage of available water
  if (PctAvailWater < irthr)  
  {
    irrigation.amount = (1.0 - PctAvailWater/100.) * pot_sw;  // irrigation in mm       
  }
```
 
### Example:
#### General way to use this feature:
```
&, REPLACE, IRMDP, 30
&, REPLACE, IRTHR, 50
```

[Dome functions page](DOME_functions.md)

[Home](index.md)