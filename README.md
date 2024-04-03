⚠️ WORK IN PROGRESS

# data-engineering-snippets

## Re-publish CSV to Socrata
If you have a CSV online, but want to mirror it to a Socrata instance.
```

```

## Download OSM Data as CSV
Go to https://overpass-turbo.eu/, click export, copy link for "raw data directly from Overpass API"
```
curl https://overpass-api.de/api/interpreter?data={{URL_ENCODED_QUERY}} > ./files/{{OUTPUT_FILE_NAME}}.csv
```
Example: https://github.com/officeofperformancemanagement/fresh-food/tree/main


## Download Google Maps as CSV
You'll first want to install [ogr2ogr](https://gdal.org/programs/ogr2ogr.html).  You'll want to replace the variables enclosed in curly braces below.
#### downloading only polygons and multi-polygons
```
ogr2ogr -dim XY -f CSV -lco GEOMETRY=AS_WKT -lco GEOMETRY_NAME=boundary -nlt MULTIPOLYGON -sql "SELECT Name AS name,description AS description FROM \"{{NAME_OF_MAP_LAYER}}\" WHERE OGR_GEOMETRY='MultiPolygon' or OGR_GEOMETRY='Polygon'" -skipfailures ./files/{{OUTPUT_FILE_NAME}}.csv "/vsicurl/https://www.google.com/maps/d/kml?mid={{MAP_ID}}&forcekml=1"
```
Example: https://github.com/officeofperformancemanagement/neighborhood_association_boundaries
