.. _advanced:

Advanced features
=================

Land cover evolution
--------------------

The land cover types to consider are defined by the user
(see the :ref:`hydro units section <spatial-structure>`).
Each hydro unit is thus defined by a total area and fractional land covers.
These land covers can have a dynamic evolution, externally driven.
One can provide the model with a timeseries of dates and new land cover areas, such as:

.. code-block:: python

   changes = behaviours.BehaviourLandCoverChange()
   changes.load_from_csv(
       '/path/to/surface_changes_glacier_debris.csv',
       hydro_units, area_unit='km2', match_with='elevation'
   )
   changes.load_from_csv(
       '/path/to/surface_changes_glacier_debris.csv',
       hydro_units, area_unit='km2', match_with='elevation'
   )

The corresponding csv file must contain the name of the land cover to change on the
first row (for example here ``glacier_debris``), the dates of these changes on the
second row, and then the change time series.
These changes list all hydro units that need to change; those that do not need to
change should not be listed in the file.
There are two ways to identify the hydro units: by elevation
(``match_with='elevation'``) or by ID (``match_with='id'``).
In the following example, these changes start with the unit elevation and contain the
time series of the area (here in km2) for every date given above.

.. code-block:: text
   :caption: Example of a csv file containing a land cover evolution.

   bands,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris,glacier_debris
   ,01/08/2020,01/08/2025,01/08/2030,01/08/2035,01/08/2040,01/08/2045,01/08/2050,01/08/2055,01/08/2060,01/08/2065,01/08/2070,01/08/2075,01/08/2080,01/08/2085,01/08/2090,01/08/2095,01/08/2100
   4274,0.013,0.003,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
   4310,0.019,0.009,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
   4346,0.052,0.042,0.032,0.022,0.012,0.002,0,0,0,0,0,0,0,0,0,0,0
   4382,0.072,0.062,0.052,0.042,0.032,0.022,0.012,0.002,0,0,0,0,0,0,0,0,0
   4418,0.129,0.119,0.109,0.099,0.089,0.079,0.069,0.059,0.049,0.039,0.029,0.019,0.009,0,0,0,0
   4454,0.252,0.242,0.232,0.222,0.212,0.202,0.192,0.182,0.172,0.162,0.152,0.142,0.132,0.122,0.112,0.102,0.092
   4490,0.288,0.278,0.268,0.258,0.248,0.238,0.228,0.218,0.208,0.198,0.188,0.178,0.168,0.158,0.148,0.138,0.128
   4526,0.341,0.331,0.321,0.311,0.301,0.291,0.281,0.271,0.261,0.251,0.241,0.231,0.221,0.211,0.201,0.191,0.181
   4562,0.613,0.603,0.593,0.583,0.573,0.563,0.553,0.543,0.533,0.523,0.513,0.503,0.493,0.483,0.473,0.463,0.453
   4598,0.648,0.638,0.628,0.618,0.608,0.598,0.588,0.578,0.568,0.558,0.548,0.538,0.528,0.518,0.508,0.498,0.488
   4634,0.618,0.608,0.598,0.588,0.578,0.568,0.558,0.548,0.538,0.528,0.518,0.508,0.498,0.488,0.478,0.468,0.458
   4670,0.478,0.468,0.458,0.448,0.438,0.428,0.418,0.408,0.398,0.388,0.378,0.368,0.358,0.348,0.338,0.328,0.318
   4706,0.306,0.296,0.286,0.276,0.266,0.256,0.246,0.236,0.226,0.216,0.206,0.196,0.186,0.176,0.166,0.156,0.146
   4742,0.338,0.328,0.318,0.308,0.298,0.288,0.278,0.268,0.258,0.248,0.238,0.228,0.218,0.208,0.198,0.188,0.178
   4778,0.199,0.189,0.179,0.169,0.159,0.149,0.139,0.129,0.119,0.109,0.099,0.089,0.079,0.069,0.059,0.049,0.039
   4814,0.105,0.095,0.085,0.075,0.065,0.055,0.045,0.035,0.025,0.015,0.005,0,0,0,0,0,0
   4850,0.051,0.041,0.031,0.021,0.011,0.001,0,0,0,0,0,0,0,0,0,0,0
   4886,0.019,0.009,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
   4922,0.008,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
   4958,0.003,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0

There is no need to specify the corresponding change in the generic ``ground`` land
cover as it will be automatically computed to preserve the total hydro unit area.
