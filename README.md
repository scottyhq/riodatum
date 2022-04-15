## Are reprojection issues due to dependency library version mismatches? 
https://github.com/rasterio/rasterio/issues/2433
see also: https://github.com/conda-forge/rasterio-feedstock/issues/239

### CONDA-FORGE rasterio
WARNING: does not necessarily match dependency versions of rasterio pypi wheels!!
`$conda create -n rasterio rasterio`
```
proj                      9.0.0                h93bde94_1    conda-forge
pyproj                    3.3.0            py39hcadae2f_2    conda-forge
gdal                      3.4.2            py39hc691d54_0    conda-forge
libgdal                   3.4.2                haa48f22_0    conda-forge
geotiff                   1.7.1                h509b78c_0    conda-forge
rasterio                  1.2.10           py39h2e4b6e6_5    conda-forge
geos                      3.10.2               h9c3ff4c_0    conda-forge
```

### PIP rasterio
```
$conda create -n riopip python=3.9 ipykernel
$conda activate riopip
$pip install --pre rasterio 
$python -m ipykernel install --name riopip --user
```
```
(riopip) jovyan@jupyter-scottyhq: venv$ rio --version
1.3a3
(riopip) jovyan@jupyter-scottyhq: venv$ rio --gdal-version
3.4.1
```

Until https://github.com/rasterio/rasterio/issues/2349 
I think we go here to find other versions that the wheel used
https://github.com/rasterio/rasterio-wheels/blob/master/env_vars.sh

```
LIBPNG_VERSION=1.6.35
ZLIB_VERSION=1.2.11
LIBDEFLATE_VERSION=1.7
JPEG_VERSION=9c
LIBWEBP_VERSION=1.0.3
OPENJPEG_VERSION=2.4.0
GEOS_VERSION=3.10.2
JSONC_VERSION=0.15
SQLITE_VERSION=3330000
PROJ_VERSION=8.2.1
GDAL_VERSION=3.4.1
CURL_VERSION=7.80.0
NGHTTP2_VERSION=1.46.0
EXPAT_VERSION=2.2.6
HDF5_VERSION=1.10.8
NETCDF_VERSION=4.6.2
ZSTD_VERSION=1.5.0
TIFF_VERSION=4.3.0
OPENSSL_DOWNLOAD_URL=https://www.openssl.org/source/
OPENSSL_ROOT=openssl-1.1.1l
OPENSSL_HASH=0b7a3e5e59c34827fe0c3a74b7ec8baef302b98fa80088d7f9153aa16fa76bd1
export MACOSX_DEPLOYMENT_TARGET=10.10
export GDAL_CONFIG=/usr/local/bin/gdal-config
export PACKAGE_DATA=1
export PROJ_LIB=/usr/local/share/proj
export AUDITWHEEL_EXTRA_LIB_NAME_TAG=rasterio
export SETUPTOOLS_USE_DISTUTILS=stdlib
```

### matching GDAL install
NOTE: per-gdal instructions, we create a matching venv with GDAL command line tools:
```
$conda config --set channel_priority strict
$conda create -n gdal341 -c conda-forge python=3.9 ipykernel gdal=3.4.1 proj=8.2.1
$conda list | grep 'proj\|rasterio\|gdal\|tiff\|geos'
```

```
gdal                      3.4.1            py39h85832e7_5    conda-forge
geos                      3.10.2               h9c3ff4c_0    conda-forge
geotiff                   1.7.0                h6593c0a_6    conda-forge
libgdal                   3.4.1                hff5c5e8_5    conda-forge
libtiff                   4.3.0                h542a066_3    conda-forge
proj                      8.2.1                h277dcde_0    conda-forge
```
