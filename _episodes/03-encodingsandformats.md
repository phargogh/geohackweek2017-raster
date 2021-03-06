---
title: "Encodings, Formats and Libraries"
teaching: 5
exercises: 0

questions:
- "What sorts of formats are available for representing raster datasets?"

objectives:
- Understand the high-level data interchange formats for raster datasets.

keypoints:
- Geospatial libraries are very useful for reading, writing and transforming
  geospatial rasters
- Once a raster's pixel values have been extracted to a NumPy array, they can
  be processed with more specialized libraries and routines.

---

# Libraries and File formats for raster datasets

[GDAL](http://gdal.org) (Geospatial Data Abstraction Library) is the de facto standard library for 
interaction and manipulation of geospatial raster data.  The primary purpose of GDAL or a
GDAL-enabled library is to read, write and transform geospatial datasets in a
way that makes sense in the context of its spatial metadata.  GDAL also includes
a set of [command-line utilities](http://www.gdal.org/gdal_utilities.html) (e.g., gdalinfo, gdal_translate) 
for convenient inspection and manipulation of raster data.

Other libraries also exist (we'll introduce rasterio in the next section of this
tutorial, and even more exist in the fields of geoprocessing (which would
include hydrological routing and other routines needed for Earth Systems
Sciences) and digital signal processing (including image classification,
pattern recognition, and feature extraction). 

GDAL's support for different file formats depends on the format drivers that
have been implemented, and the libraries that are available at compile time.
To find the available formats for your current install of GDAL:

~~~
$ gdalinfo --formats
~~~
{: .shell}

    Supported Formats:
      VRT -raster- (rw+v): Virtual Raster
      GTiff -raster- (rw+vs): GeoTIFF
      NITF -raster- (rw+vs): National Imagery Transmission Format
      RPFTOC -raster- (rovs): Raster Product Format TOC format
      ...
      # There are lots more, results depend on your build

Details about a specific format can be found with the ``--format`` parameter,
or by taking a look at the
[formats list on their website](http://www.gdal.org/formats_list.html).

~~~
$ gdalinfo --format GTiff
~~~
{: .shell}

> ## Jupyterhub detail: location of gdal command-line scripts
> 
> If you've installed and activated your conda environment, ``gdalinfo`` should
> be available.  It might not be available from your jupyter notebook, however.
>
> To access the gdalinfo within our jupyterhub notebook, gdalinfo is available at
>
>     /opt/anaconda/envs/rasterenv/bin/gdalinfo
> 
{: .callout}


# Programming Model: NumPy arrays

Because rasters are images, they are best thought of as 2-dimensional arrays.  If we
have multiple bands, we could think of an image as a 3-dimensional array.
Either way, we are working with arrays (matrices) of pixel values, which in the
python programming language are best represented by [NumPy](http://numpy.org) arrays.

For this tutorial, we'll perform basic operations with NumPy arrays extracted
from geospatial rasters.  For more information about multidimensional array
analysis, take a look at Thursday's tutorial on 
[N-Dimensional Arrays](https://geohackweek.github.io/nDarrays).
