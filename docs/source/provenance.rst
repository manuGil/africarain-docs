Production of raw data files
============================
**Data available for download have been processed from their original raw form.** This page describes the generation of the raw simulation data, including which model and parameter values were used to generate it. Steps taken to produce the processed data are described in the :doc:`/data_processing` section.

Raw simulation data production
------------------------------
Data are high-resolution computer simulations of localized rainstorms in sub-Saharan Africa produced using massive, crowd-sourced computing power from World Community Grid (see documentation on :ref:`community-grid`).

The amount of raw simulation data produced is about 0.5 PB or, in more nostalgic terms, a pile of floppy disks of over 1000 km. That pile would weigh over 6700 tons and would be over 1200 km high. About twenty variables of direct interest are stored and uploaded to the central WCG facility. These data are stored in netCDF files.

---------------

Forcing data
------------

Forcing data used as input for the simulation results come from:

   National Centers for Environmental Prediction/National Weather Service/NOAA/U.S. Department of Commerce. 2015, updated daily. NCEP GDAS/FNL 0.25 Degree Global Tropospheric Analyses and Forecast Grids. Research Data Archive at the National Center for Atmospheric Research, Computational and Information Systems Laboratory. DOI: 10.5065/D65Q4T4Z

The data are available from UCAR `here <https://rda.ucar.edu/datasets/ds083.3/#!description>`_. Data are free, but registration is required.

---------------

Model architecture
------------------
The model used to produce these simulations is the Weather Research and Forecasting Model (WRF) V3.9.1.1 from the National Center for Atmospheric Research (NCAR).

ARP divides the African continent into over 35609 WRF modelling units. For each unit of 50x50 cells, WRF is run on a personal computer of a volunteer, who shares spare computing resources via the WCG. It calculates episodes of two days’ worth of weather with output for every 15 minutes (193 total time steps each).

Each WRF unit is triply nested.  Hence, it first calculates at a coarse resolution of 9km x 9km, covering a 468km x 468km region with historical boundary conditions from NOAA's Global Forecast System (GFS-ANL).  Within the centre of this domain, it calculates the next domain at the intermediate resolution of 3 km (156 km x 156 km) with the boundary conditions set by the coarser domain calculation.

Finally, a unit of 52 km x 52km is calculated at the centre of the intermediate domain. Vertically, the atmosphere is divided into 51 layers so that the output is produced on a 52x52x51 grid.

.. figure:: _static/img/spatial-granularity.png

Model input parameter values
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
For a complete list of parameter values that were used as inputs for the WRF model in order to produce the resulting simulation data, please see `Model input parameter values. See :doc:`input_values`

---------------

Time period
-----------
The period of simulation data covered will ultimately run from 1 June 2018 until 31 May 2019. Raw simulation data are generated on a rolling basis subject to volunteer participation. If the current pace continues, the dataset is expected to be complete in mid-2022. Simulation data are generated at a 15-minute time interval.

---------------

Units
-----
Units define geographic areas for which simulation results are available or will be available. A total of 35.609 square units cover Sub-Saharan Africa.
For each unit, simulation results are produced at three spatial granularities called domains. Thus, a domain can also be described as a subset of a unit with a particular spatial resolution.

The domains used in the simulation have the following resolutions:

+ Domain 1: 9 km
+ Domain 2: 3 km
+ Domain 3: 1 km

The centroid of each unit is separated by 15.3 minutes of arc in both latitude and longitude. Each unit partially overlaps with adjacent units; all domains contain 51 X 51 grid points. The model results are non-deterministic, so units were designed to overlap and create redundancy for a given geographic location, i.e., more than one value for a specific geographic location at a given time. These values will treated in the processing steps to remove the effect of the overlapping values. More information about the status of 
processed data in `Production of processed data :docs:`data_processing`

---------------

Georeferencing information
--------------------------

Raw datasets were produces using the **WRF Lambert Conformal** projection. For details, consult the `WRF Model Manuals <https://www2.mmm.ucar.edu/wrf/users/docs/user_guide_V3/contents.html>`_

---------------

Variables in raw simulation dataset
-----------------------------------

=============  ====================================================================================  =============  =============  ===============
VARIABLE       DESCRIPTION                                                                           DATA TYPE      UNITS          GEOGRAPHIC DATA
=============  ====================================================================================  =============  =============  ===============
Times          --                                                                                    char           --             No
HFX_FORCE      SCM ideal surface sensible heat flux                                                  float          W/m2           No
NEST_POS       --                                                                                    float          --             Yes
Q2             Water vapor mixing ratio (QV) at 2m                                                   float          Kg/Kg          Yes
T2             Air temperature at 2m                                                                 float          K              Yes
TH2            Potential temperature at 2m                                                           float          K              Yes
PSFC           Surface air pressure                                                                  float          Pa             Yes
U10            U component of the wind speed at 10m (X surface wind)                                 float          m/s            Yes
V10            V component of the wind speed at 10 m (Y surface wind)                                float          m/s            Yes
ITIMESTEP      --                                                                                    int            --             No
XTIME          Minutes since 2018-07-01 00:00:00                                                     float          minutes        No
SMOIS          Soil moisture                                                                         float          m3/m3          Yes
P_TOP          Pressure top of the model                                                             float          Pa             No
RAINC          Accumulated total cumulus precipitation (convective precipitation)                    float          mm             Yes
RAINSH         Accumulated shallow cumulus precipitation (large-scale precipitation)                 float          mm             Yes
RAINNC         Accumulated total grid scale precipitation (non-convective precipitation)             float          mm             Yes
SWDOWN         Downward short wave flux at ground surface (surface downwelling shortwave radiation)  float          W/m2           Yes
GLW            Downward long wave flux at ground surface (surface downwelling longwave radiation)    float          W/m2           Yes
OLR            Top of atmosphere outgoing longwave radiation                                         float    W/m2    Yes
SR             Fraction of frozen precipitation                                                      float          --             Yes
SST            Sea surface temperature                                                               float          K              Yes
=============  ====================================================================================  =============  =============  ===============
