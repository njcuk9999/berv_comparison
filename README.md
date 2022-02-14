# berv_comparison
Comparing different BERV implementations 


## Running comparison

To run the comparison run `berv_compare.py`

Currently compared BERV calculations are:
- astropy
- barycorrpy
- pyasl implmentation
- "Oli" implementation


## Changable parameters

The following parameters can be changed in the `berv_compare.py` code.

There are two "modes"
- simple: produces a single measurement using the `INPUT_XXX` parameters
- grid: loops around the grid parameters (warning do not make these too large as it will run many calculations)

```python
from astropy.coordinates import EarthLocation
from astropy.time import Time
import numpy as np

# Here we use all Gaia EDR3
INPUT_RA = 269.448502525438 # deg
INPUT_DEC = 4.73942005111241 # deg
INPUT_PMRA = -801.55097836847 # mas / yr
INPUT_PMDE = 10362.3942065465 # mas / yr
INPUT_PLX = 546.975939730948   # mas
INPUT_COORD_TIME = 2457388.5   # JD
# ----------------------------------------------------------------------------
loc = EarthLocation.of_site("Paranal")
#loc = EarthLocation.of_site("Canada-France-Hawaii Telescope")
INPUT_LONG = loc.lon.value     # in deg
INPUT_LAT = loc.lat.value      # in deg
INPUT_ALT = loc.height.value   # in m
# ----------------------------------------------------------------------------
START_DATE = Time('2020-01-01 00:00:00', format='iso')
END_DATE = Time('2021-01-01 00:00:00', format='iso')
STEPS = 5
# ----------------------------------------------------------------------------
# ra / dec in degrees (forms a map)
GRID_RA = np.linspace(0, 359, 10)
GRID_DEC = np.linspace(-89, 89, 10)
# pmra in mas / yr
GRID_PMRA = np.linspace(-6000, 6000, 6)
# pmde in mas / yr
GRID_PMDE = np.linspace(-6000, 6000, 6)
# plx in mas
GRID_PLX = 10**(np.linspace(0, 3, 6))

# select mode (simple or grid)
MODE = 'simple'

# ----------------------------------------------------------------------------
# where things are saved
workspace = '/data/nirps_he/misc/berv_comp'
# output pdf
outfile = 'berv_comparison_{0}.pdf'
# output grid
grid_file = 'grid_{0}.fits'

```