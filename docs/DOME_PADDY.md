# PADDY Function

This function allows standard paddy management inputs to be generalized for a field or group of fields.

Sample Paddy function:


### Inputs:
* Number of Bund height entries
* Percolation rate (mm/d)
* Plowpan depth (mm)
* Dates of paddy management operations (days after planting)
* Maximum flood height (mm) - height of bund
* Minimum flood height (mm) - depth of target pool

The last three could be multiple

### Outputs:
* a group of events for setting up paddy irrigation

### Example

|!|Dome operator|Variable to be modified|Value or Function|Function arguments| | |Bund operation #1|||Bund operation #2|||Bund operation #3|||
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|!| |IRRIGATION VALUE|PADDY function|# of Bund height entries|Percolation rate (mm/d)|Plowpan depth (mm)|Operation date(days after planting)|Max flood (bund) height (mm)|Min flood height (mm)|Operation date(days after planting)|Max flood (bund) height (mm)|Min flood height (mm) |Operation date(days after planting)|Max flood (bund) height (mm)|Min flood height (mm) |
|&|FILL|IRVAL|PADDY()|3|2|150|-3|20|5|4|30|10|11|50|15|

#### Results of Paddy function:

|IDATE|IROP|IRVAL|! Comment|
|-|-|-|-|
|$PDATE-3|IR010|150|! puddling, plowpan depth|
|$PDATE-3|IR008|2|! percolation rate|
|$PDATE-3|IR009|20|! bund height|
|$PDATE-3|IR011|5|! target minimum flood level|
|$PDATE+4|IR009|30|! bund height|
|$PDATE+4|IR011|10|! target minimum flood level|
|$PDATE+11|IR009|50|! bund height|
|$PDATE+11|IR011|15|! target minimum flood level|

[Dome functions page](DOME_functions.md)

[Home](index.md)
