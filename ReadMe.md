# The ZIPScribble Map

Connect all the ZIP/postal codes in a country in ascending order. On a website. On top of a map that can be zoomed and dragged.

## Data Source

All data is coming from [geonames](http://geonames.org), in particular the daily [postal code data dumps](http://download.geonames.org/export/zip/). The scripts do some work to sort the codes, remove duplicates (several adjacent codes sharing the same location), etc.

The data quality is a bit uneven, with the U.S. data being the best. There are lots of countries for which no data is available at all, and others for which the data looks quite bad.

## Scripts

In the data directory, there are two scripts that download and process the data to be ready for rendering.

* `download.sh` downloads the files from geonames. It only downloads versions of files that already exist in the directory. To get the process started, use `touch` to create some empty files (`US.txt`, `CA.txt`, `DE.txt`, etc.) and then run download. The files are refreshed every night on geonames, though it's unclear when the data actually changes.

* `txt2json.py` is the key script. It parses the CSV data, sorts the ZIP codes, and creates the geoJSON files (`zipscribble_XY.json`) as well as the `countryinfo.json` file that lists the bounding boxes and whether the countries have states or not. It has some special constructs to ignore parts of some countries when determining the bounding box, as well as ignoring certain points that cause issues on the map.


## External Libraries and Resources

* [Polymaps](http://polymaps.org/)
* [jQuery](http://jquery.com/)
* [The GeoJSON format](http://geojson.org/) used by the geoJSON layer in Polymaps