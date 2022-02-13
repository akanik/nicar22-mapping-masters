## Point in polygon

Point in polygon analysis allows you to count points that fall within a polygon. 

In order to see where the most new residences are being built in the city of Atlanta, we can overlay building permits (points) with Atlanta zip codes (polygon) and then ask QGIS to count the number of permits in each zip code.

### Steps:

Open a new map in QGIS.

Add the `esri_atl_zips.shp` shapefile and the `atl_res_permits` data to the map.

Go to Vector > Analysis Tools > Count Points in Polygon.

Use the following settings:
- Polygons = `esri_atl_zips`
- Points = `atl_res_permits`
- Count field name = **permit_cnt**

Click Run.

You should see a new layer called Count has been added to the map. If you examine the attribute table, you’ll see that this layer is a copy of the `esri_atl_zips` layer with an added field at the end called **permit_cnt**`.

The **permit_cnt** value is a sum of all of the residential permits for each zip code. 

In the Count attribute table, click on the **permit_cnt** column header to sort the table by that column. Once the largest value is at the top, click the index number for the topmost row (it will be 1) to highlight that feature.

Refer back to the map to see which tract has had the most residential building permits since 2018.


## Hexbins

Hexbin analysis is a very popular way to group data points and pull out hotspots. While grouping or aggregating data by other units, such as zip codes or Census tracts, can be very useful, hexbins allow us to create politically-agnostic geographic units. 

This is extremely helpful because many datasets have nothing to do with political or postal boundaries and grouping by them can miss some very important patterns.

### Steps:

(Full props to Mike Corey for the following steps!)

MMQGIS should already be installed as a QGIS plugin. If it's not, go to the plugins main menu, search for and install MMQGIS. 

Set your project CRS. We’re going to need to reference the units used by the project CRS later on in this process so we need to be sure the CRS is set to something that uses feet: EPSG:6447 - NAD83(2011) / Georgia West (ftUS) - Projected. 

Go to Project > Properties > CRS and search "6447". Select ** NAD83(2011) / Georgia West (ftUS)** and click OK.

Reproject your point data. We’re going to also need the points data (in this case `atl_res_permits`) to be projected in the same EPSG:6447. 

Next, we're going to calculate the hexbin short diagonal. Figure out how big you want your grids to be. When doing local analyses, often times I try to make my hexbins the average area of a city block.

For Atlanta, I've observed that many city blocks are between 400 - 600ft long. Let's say that the average is 500ft, which makes for a block with an area of 250,000 sq ft. 

[Use this calculator](https://rechneronline.de/pi/hexagon.php) to find the short diagonal length of a hexagon with an area of 250,000 sq ft. Enter 250000 into the Area (A) field and click Calculate.

Note the result in the Short diagonal (d2) field: 537.

Create the hexbin grid. Navigate to MMQGIS > Create > Create Grid Layer.

Use these settings:
- Geometry type = hexagons
- Extent = Current window (make sure your zoom encompases all the `atl_res_permits` points)
- Layer = `esri_atl_zips`
- Units = Layer Units
- Y Spacing = 537
- Output File Name = the output here will be a layer of hexagons with no data attributes. So we want to call it something pretty general. I like to include the geographic extent of the grid and the y spacing I used to create it. Let’s put this one in a directory called atl-grids and call it atl-grid-537y. That way, if we need to adjust the size of our grid, we can save multiple grid files here and use them accordingly.

Click Apply.

It may take a minute, but you should see a new layer of hexagons added to your map! Add an OpenStreet basemap in order to check whether each hexagon is roughly the size of a city block.

Do a point in polygon analysis. Using the hexagons and the `atl_res_permits`, do a point in polygon analysis like we did above with the zip codes and the `atl_res_permits`.

Style your hexagons. Using a graduated color scheme, style your hexagons so you can quickly identify areas that are more dangerous for pedestrians.

