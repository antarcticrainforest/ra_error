# Bayesian Rainfall Estimate Uncertainty

This software calculates estimates uncertainties of radar based rainfall retrievels. 
## Installation
For fast computation the main part of the software is written in C and has to be compiled to do so simply run:

```
python setup.py install
```
if you lack permissions on the target system add the ```--user``` flag.

## Basic Example
To apply the Baysian update a statistical estimate on the average radar error has to be given. This can be a form of a text-file that compares mean and standard diviation of radar rainfall errors, when compared to rain gauge data.

Suppose the this file containing the comparison of radar rainfall and rain gauge data is stored in ```radar_error.txt``` 

```python

 import numpy as np
 from netCDF4 import Dataset as nc
 import radar_error
 with nc('Radar_rain.nc') as rr:
    precip = rr.variables['rr'][2,:]
    lon  = rr.variables['i'][:]
    lat  = rr.variables['j'][:]
    errfile = 'radar_error.txt'
    # Calculate the rain-rate at a 'certainty' of 80%.
    perc_80 = radar_error.get(data, lon, lat, errfile, 80.)
```
