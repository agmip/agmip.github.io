# AgMIP Climate Scenario Naming Convention

These are the naming conventions that have been developed for daily weather data files for AgMIP climate scenarios. For the ACMO data, the first 4 characters of this naming convention can be ignored, as the institution and location are provided in other fields. The fifth through eighth characters can be used to identify a climate scenario used in any given crop model simulation.

**First 4 Digits** describe location (e.g. OBRE, FL11)

**Fifth Digit** is time period and emissions scenario:
* 0 = 1980-2009 baseline
* 1 = A2-2005-2035 (Near-term)
* 2 = B1-2005-2035 (Near-term)
* 3 = A2-2040-2069 (Mid-Century)
* 4 = B1-2040-2069 (Mid-Century)
* 5 = A2-2070-2099 (End-of-Century)
* 6 = B1-2070-2099 (End-of-Century)
* S = sensitivity scenario
* A = observational time period (determined in file)
* B = RCP3PD 2010-2039 (Near-term)
* C = RCP45 2010-2039 (Near-term)
* D = RCP60 2010-2039 (Near-term)
* E = RCP85 2010-2039 (Near-term)
* F = RCP3PD 2040-2069 (Mid-Century)
* G = RCP45 2040-2069 (Mid-Century)
* H = RCP60 2040-2069 (Mid-Century)
* I = RCP85 2040-2069 (Mid-Century)
* J = RCP3PD 2070-2099 (End-of-Century)
* K = RCP45 2070-2099 (End-of-Century)
* L = RCP60 2070-2099 (End-of-Century)
* M = RCP85 2070-2099 (End-of-Century)
 
**Sixth Digit** is source of baseline data (if baseline scenario):
* X = no GCM used
* 0 = imposed values (sensitivity tests)
* Q = Bias-corrected MERRA
* T = NASA POWER
* U = NARR
* V = ERA-INTERIM
* W = MERRA
* Y = NCEP CFSR
* Z = NCEP/DoE Reanalysis-2

**Sixth Digit** is GCM (if CMIP3 scenario):
* X = no GCM used
* 0 = imposed values (sensitivity tests)
* A = bccr
* B = cccma cgcm3
* C = cnrm
* D = csiro
* E = gfdl 2.0
* F = gfdl 2.1
* G = giss er
* H = inmcm 3.0
* I = ipsl cm4
* J = miroc3 2 medres
* K = miub echo g
* L = mpi echam5
* M = mri cgcm2
* N = ncar ccsm3
* O = ncar pcm1
* P = ukmo hadcm3

**Sixth Digit** is GCM (if CMIP5 scenario):
* 0 = imposed values (sensitivity tests)
* A = ACCESS1-0
* B = bcc-csm1-1
* C = BNU-ESM
* D = CanESM2
* E = CCSM4
* F = CESM1-BGC
* G = CSIRO-Mk3-6-0
* H = GFDL-ESM2G
* I = GFDL-ESM2M
* J = HadGEM2-CC
* K = HadGEM2-ES
* L = inmcm4
* M = IPSL-CM5A-LR
* N = IPSL-CM5A-MR
* O = MIROC5
* P = MIROC-ESM
* Q = MPI-ESM-LR
* R = MPI-ESM-MR
* S = MRI-CGCM3
* T = NorESM1-M
* U = FGOALS-g2
* V = CMCC-CM   
* W = CMCC-CMS  
* X = CNRM-CM5   
* Y = HadGEM2-AO   
* Z = IPSL-CM5B-LR
* 1 = GFDL-CM3   
* 2 = GISS-E2-R   
* 3 = GISS-E2-H   
* 4 = CanAM4 (HAPPI)
* 5 = CAM4-2degree (HAPPI)
* 6 = CAM5-1-2-025degree (High-resolution; HAPPI)
* 7 = CAM5 (low-resolution; HAPPI)
* 8 = HadAM3P (HAPPI)
 
**Seventh Digit** is downscaling/scenario methodology:
* X = no additional downscaling
* 0 = imposed values (sensitivity tests)
* 1 = WRF
* 2 = RegCM3
* 3 = ecpc
* 4 = hrm3
* 5 = crcm
* 6 = mm5i
* 7 = RegCM4
* A = GiST
* B = MarkSIM
* C = WM2
* D = 1/8 degree BCSD
* E = 1/2 degree BCSD
* F = 2.5minute WorldClim
* W = TRMM 3B42
* X = CMORPH
* Y = PERSIANN
* Z = GPCP 1DD
 
**Eighth Digit** is Type of Scenario:
* X = Observations (no scenario)
* A = Mean Change from GCM
* B = Mean Change from RCM
* C = Mean Change from GCM modified by RCM
* D = Mean Temperature Changes Only
* E = Mean Precipitation Changes Only
* F = Mean and daily variability change for Tmax, Tmin, and P
* G = P, Tmax and Tmin daily variability change only
* H = Tmax and Tmin daily variability and mean change only
* I = P daily variability and mean change only
* J = Tmax and Tmin daily variability change only
* K = P daily variability change only



[Home](index.md)
