# Bay Area Blockgroup API
This is a modified version of Code for America's [US Census Area API](https://github.com/codeforamerica/US-Census-Area-API) that checks only against the US Census block group geometries. During (and possibly after) the US government shutdown, it will be used as a replacement for the [FCC's Block Conversion API](http://www.fcc.gov/developer/census-block-conversions-api-v1.0.1) ([cached](http://webcache.googleusercontent.com/search?q=cache:PHkruETVxnEJ:www.fcc.gov/developer/census-block-conversions-api-v1.0.1+&cd=3&hl=en&ct=clnk&gl=us)), which provides data describing which Census areas (including a block-level FIPS code) intersect with a given latitude and longitude.

The [original README](https://github.com/codeforamerica/hack-requests/blob/master/census-area-API.md) follows:


US Census Area API
==================

Simple geospatial API for US Census, in response to the
[Census Area API hack request](https://github.com/codeforamerica/hack-requests/blob/master/census-area-API.md).

A sample copy with Bay Area Census data can be found at
[census-api-bay-area.herokuapp.com](http://census-api-bay-area.herokuapp.com).

Installing
----

This is a [Flask](http://flask.pocoo.org/)-based Python application which
requires compiled geospatial libraries [Shapely](http://toblerity.org/shapely/)
and [GDAL](http://trac.osgeo.org/gdal/) to run.

### Test Locally

1. Download and unpack [sample Bay Area data](http://forever.codeforamerica.org.s3.amazonaws.com/Census-API/bay-area-data.zip).
2. Ensure that *datasource.shp* and other files are located in the same directory as *app.py*.
3. Call `python app.py` for a test server.

### Run Locally with Gunicorn

To run a more robust installation using the Python WSGI HTTP server
[Gunicorn](http://gunicorn.org/), prepare local data as in steps 1 & 2 above,
then call:

    gunicorn app:app

### Run on Heroku

Compiled geospatial libraries for Heroku are available via the
[open source GIS Heroku buildpack](https://github.com/codeforamerica/heroku-buildpack-pygeo).
There are two possible ways to run this API on Heroku:

1. Fork this repository, download and commit your own data as *datasource.shp*,
and push the combined application + data repository to Heroku.

2. Use the `ZIPPED_DATA_URL` support in *heroku-buildpack-pygeo* to configure
a remote zip file such as *bay-area-data.zip* (URL linked above),
**making sure to install the Heroku plugin**
[user-env-compile](https://devcenter.heroku.com/articles/labs-user-env-compile).
Data will be automatically retrieved and expanded to *datasource.shp* at
compile time.
