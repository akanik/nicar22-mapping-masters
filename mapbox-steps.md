# Mapbox

To get started, you need a Mapbox account and an access token. 

[Sign up for your account here](https://account.mapbox.com/auth/signup/).

Find your default access token and create additional [access tokens here](https://account.mapbox.com/). 


## What's free what's not
Your Mapbox account is free, but some of the things you'll do in Mapbox will incur fees. It's important to know where the free tier cuts off so you can design your graphics according to your newsrooms budget.

[Map loads](https://www.mapbox.com/pricing/) - “A map load is counted every time Mapbox GL JS initializes on a webpage or in a web app. A map load includes unlimited Vector Tiles API and Raster Tiles API requests.” You will get up to 50,000 map loads are free per month.

[Tilesets](https://docs.mapbox.com/studio-manual/reference/tilesets/) - “Tilesets uploaded in Mapbox Studio are free, and do not incur processing or hosting charges. Free uploads via Mapbox Studio are limited to 20 uploads per month, and 300 MB per upload.” If you require more than 20 uploads or your files are larger than 300 MB, you can use [Mapbox Tiling Services](https://docs.mapbox.com/mapbox-tiling-service/guides/) or the [Uploads] API(https://docs.mapbox.com/api/maps/uploads/). NOTE: it seems like Mapbox is putting most of its eggs in the MTS basket so if you're trying to decide which alternate Tileset upload method to use, that's probably the one to invest your time in.


## Datasets, Tilesets and Styles

### Datasets
A Mapbox dataset is an editable collection of points, lines or polygons. Much of what you can do with datasets you can do with geographics files in QGIS. Therefore, we will not be going over these much. But I encourage you to [read more about them](https://docs.mapbox.com/studio-manual/reference/datasets/) and see if working with Mapbox datasets is a thing that will work better for you.

### Tilesets (Self-hosting files vs. Mapbox hosting)
Tilesets are geographic data (geojson, shapefiles, etc) that have been converted into vector tiles visible at different zoom levels. That sounds more confusing than it is. Consider the following:

![Sacramento Meadowview data tileset zoom level explainer](./img/tileset-zooms.png)

The image on the left is population data for the Meadowview neighborhood in Sacramento at a zoom level of about 9.5. It makes sense for each point to be visible at that zoom level. The image on the right is the same dataset at a zoom level of about 4.5. There is no reason for those points to be rendering at that zoom level because their geographic importance at such a distance is basically nonexistent. 

There are two ways of using geographic data in Mapbox. You can upload the data via Mapbox Studio's Tileset interface, or you can self-host your geojson files.

The biggest benefit to using Mapbox tilesets is performance. From the [Mapbox docs](https://docs.mapbox.com/help/troubleshooting/mapbox-gl-js-performance/#use-vector-tileset-sources): "Use vector tileset sources over GeoJSON data sources when possible. The renderer splits features in vector tilesets into tiles which allows GL JS to load only the features that are visible on the map. Feature geometries are also simplified meaning there are fewer vertices resulting in reduced render, source update, and layer update times."

Your self-hosted data will also be converted into vector tiles, but it will be an on-the-fly process and will not be as optimized as importing your data as a Mapbox tileset.

Another benefit is that you can do more non-code styling of your data using Mapbox Styles.

**[Tips](https://docs.mapbox.com/help/troubleshooting/working-with-large-geojson-data/) for reducing the size of your geojson files:**
- remove unnecessary properties/variables
- set the `maxZoom` level on your geoJSON source so it's not larger than you need
- if possible, use point clustering for point locator maps. If you can't cluster, allow points to overlap by setting the source `layout` property `icon-allow-overlap` to `true`
- store geoJSON files in a URL rather than loading them as a variable/Object
- Convert multipart features to singlepart features, if possible
- Simplify overly-complex shapes using [mapshaper](https://mapshaper.org/)
- See more options on this [trouble-shooting guide](https://docs.mapbox.com/help/troubleshooting/uploads/#troubleshooting)

### Styles
Styles are a combination of basemaps and tilesets. By creating and importing new styles, you can change how many basemap features are visible and at which zoom levels they are visible. You can also tilesets to a style and leverage GUI layer styling. 


## What you can do without code

You can use Style iframes to export maps without much interactivity. You can export maps that have custom basemap features and styled layers, but you won't be able to add UI like popups. 

Read more about [using Style iframes here](https://docs.mapbox.com/help/glossary/iframe/).

## Using Github to host your maps
https://pages.github.com/

## Mapbox examples
We're going to use the data we manipulated in QGIS to make a few Mapbox maps!

I order to view the html code we're about to work with, you'll need to do the following:
- open your computer's terminal
- type `cd [path to this classes folder]`
- once in the correct folder, type `python -m http.server`
- go to `localhost:8000/mapbox-point-popup.html` in your browser and you should see a map!

We will be opening the following 3 html files using a code editor.

### [Example: Basic point locator + popup](./mapbox-point-popup.html)
First we need to upload our building permit points geojson as a Mapbox Tileset.

Go to [Mapbox > Tilesets](https://studio.mapbox.com/tilesets/), click **New Tileset** and upload the point geojson you created from the QGIS portion of this class. If you weren't able to create that file or your file keeps erroring out for some reason (likely because you didn't project it correctly), you can use [the backup geojson](#) I've created for just such an eventuality!

Once your building permits file has uploaded, take note of the Tileset ID.

Now we're going to create a style.

Got to [Mapbox > Styles](https://studio.mapbox.com/) and click **New Style**. Choose a template and a variation that suite your fancy. I would recommend Monochrome Light because it will be easier to see our points and other layers. Click **Customize**.





### [Example: Layer choropleth + popup](./mapbox-polygon-popup.html)

### [Example: Cluster points + popup](./mapbox-point-cluster.html)

## Other examples
Here's a list of all of the [Mapbox-hosted examples](https://docs.mapbox.com/mapbox-gl-js/example/).
