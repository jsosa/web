# LFPtools
[![DOI](https://zenodo.org/badge/114779043.svg)](https://zenodo.org/badge/latestdoi/114779043)

`LFPtools` is an open-source Python CLI package which encompass most methods commonly used to prepare input data for large scale flood inundation studies using the [LISFLOOD-FP](http://www.bristol.ac.uk/geography/research/hydrology/models/lisflood/) hydrodynamic model.

### Installation
***

#### 1. Via pip
Just run this line after installing all dependencies

``` pip install git+https://github.com/jsosa/LFPtools.git```

#### 2. Docker
To facilitate the installation process, we have published the [Dockerfile](https://github.com/jsosa/LFPtools/blob/master/docker/Dockerfile) so you can get `LFPtools` running in a docker container

```bash
docker pull jsosa/dkr-lfptools
docker run --rm -it jsosa/dkr-lfptools
```

### Dependencies
***

- [Pandas](https://pandas.pydata.org/)
- [Geopandas](http://geopandas.org/)
- [xarray](http://xarray.pydata.org/en/stable/)
- [Cython](https://cython.org/)
- [TauDEM](http://hydrology.usu.edu/taudem/taudem5/index.html)
- [gdalutils](https://github.com/jsosa/gdalutils.git)

### Description of tools
***

**lfp-getdepths:** Get river depths, three methods availables: 1) get depths from a raster of depths 2) get depths by using hydraulic geometry equation depth = r * width ^ p and 3) get depths by using simplified mannings equation

**lfp-getwidths:** Retrieve river widths from a external data set (e.g. [GRWL](http://science.sciencemag.org/content/early/2018/06/27/science.aat0636), [GWD-LR](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1002/2013WR014664))

**lfp-getbankelevs:** Get river banks elevations from a high resolution DEM by reductions method like nearest neighbour, mean, min or meanmin. Additionally, an outlier detection can be applied to before running the reduction method.

**lfp-fixelevs:** Fix DEM elevations using either of two methods: `yamazaki` (Yamazaki et al., 2012 J. Hydrol), `lowless` (Locally Weighted Scatterplot Smoothing)

**lfp-getbedelevs:** Get bed elevations by substracting depth from banks

**lfp-getdischarge:** Retrieve discharge from a netCDF source following a predefined inflows locations (e.g. from lfp-getinflows)

**lfp-getinflows:** Locate inflow points that can be used as boundary condition from a source (e.g. discharge gridded data)

**lfp-getslopes:** Estimate slopes from a bank file (e.g. from lfp-fixelevs), slope is estimated by fitting a 1st order model on the elevations. The number of elevations to take is based on the parameter `step` in the `config.txt` file

**lfp-rasterresample:** Resample a DEM by upscaling. It applies a reductions method like mean, min or meanmin. Outlier detection is also available before running the reduction method. `nproc` option defines number of cores to be used when resampling.

### Usage
***

#### 1. Via Command Line Interface CLI

Programs run by reading input parameters from a configuration file `config.txt` via `-i` option after the tool's name, in the terminal:

```bash
$ lfp-getwidhts -i config.txt
```

Input parameters in the configuration file for each tool can be obtained via `-h` option after the tool name:

```bash
$ lfp-getwidhts -h

LFPtools v0.1

Name
----
getwidths

Description
-----------
Retrieve river widths from a data set

Usage
-----
$ lfp-getwidths -i config.txt

Content in config.txt
---------------------
[getwidths]
thresh = Searching window threshold in same units as input data set
output = Shapefile output file path
recf   = `Rec` file path
netf   = Target mask file path
proj   = Output projection in Proj4 format
fwidth = Source width file path GDAL format
```
#### 2. Within a Python environment

LFPtools can be imported within Python using

```python
import lfptools as lfp
```

### License
***

**BSD 3-Clause License**

Copyright (c) 2018, Jeison Sosa
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the copyright holder nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
