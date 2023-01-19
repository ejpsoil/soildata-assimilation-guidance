# Python

A programming language commonly used in data science. From scripts to increase the capabilities or automate processes in 
ArcMAP or QGIS, maintanance and deployment tasks in DevOps up to full programs such as GeoNode and pygeoapi.

## PIP

[PIP](https://pypi.org/project/pip/) is the package manager of python. Every script or program installs a series of packages from pip as part of its installation.

## Virtual environments

To prevent collision of dependencies between projects the use of virtual environment is common. Each virtual environment has its own python executable and libraries. Popular virtual environments are [virtualenv](https://virtualenv.pypa.io), [Conda](https://docs.conda.io/), [poetry](https://python-poetry.org/). If you're new to python I would suggest to start with [Conda](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html#managing-python).

Note that some prefer to work even more isolated and use [docker](./docker.md) to set up a development container including the required libraries.

## Jupyter notebooks

[Jupyter notebooks](jupyter.md) combine text and executable (python) code into a single document. Optimal for training, documentation and reporting about research.

## GeoPython Community

There is a large community dedicated to the use of python in the geospatial domain. Interesting libraries used in that community are: 

- [RasterIO](https://rasterio.readthedocs.io/)
- [Shapely](https://shapely.readthedocs.io/)
- [Fiona](https://fiona.readthedocs.io/)
- [OWSLib](https://geopython.github.io/OWSLib/)
- [GeoPandas](https://geopandas.org/)
- [pygeometa](../cookbook/pygeometa.md)
- [pyproj](https://pyproj4.github.io/pyproj), etc.