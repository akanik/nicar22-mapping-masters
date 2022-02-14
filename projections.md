# Projections

Projections are how we use two-dimensional space to talk about three-dimensional space. Polygons like county and state borders are three-dimensional, but we do our best to show them in two dimensions in print and online.

A coordinate reference system (CRS) defines how projected space reflects real space. 

If you want to do some more in depth reading on QGIS and projections, you can [read their documentation here](https://docs.qgis.org/3.16/en/docs/user_manual/working_with_projections/working_with_projections.html).

## Geographic vs. projected: points vs. polygons

The best way I’ve ever heard the differentiation between geographic coordinate system (GCS) and projected coordinate systems (PCS) explained is from [Heather Smith at the Arc Blog](https://www.esri.com/arcgis-blog/products/arcgis-pro/mapping/gcs_vs_pcs/):

- A GCS defines where the data is located on the earth’s surface.
- A PCS tells the data how to draw on a flat surface, like on a paper map or a computer screen.

When you’ve got points, whose only definition are location, you want a GCS. When you’ve got lines or polygons, you need to know how to draw the shape on a flat surface, so you need a PCS.

## Which projection should I use and when?
QGIS supports over 7,000 coordinate reference systems, both GCS and PCS. So how do you know which to use and when?

One consideration is visual. A layer’s CRS defines how it will appear on a 2D map. San Antonio, when displayed using a projection meant for Kentucky will look quite misshapen.

IMAGE HERE

caption: Texas displayed with the NAD_1983_StatePlane_Kentucky_FIPS_1600 projection (left) and again with the NAP_1983_Texas_Statewide_Mapping_System project (right)]

Another consideration is alignment. If you are trying to do geospatial analyses with multiple layers, you need to make sure your layers are in the same projection. 

In recent years, QGIS has made great advances in how it works with projection. Currently, when you import a file into QGIS, the system determines the correct projection for that layer based on system settings. If you haven’t changed these settings, your mapping projections are likely set by the first layer that you import into your map.

From QGIS docs:

“QGIS supports “on the fly” CRS transformation for both raster and vector data. This means that regardless of the underlying CRS of particular map layers in your project, they will always be automatically transformed into the common CRS defined for your project. Behind the scenes, QGIS transparently reprojects all layers contained within your project into the project’s CRS, so that they will all be rendered in the correct position with respect to each other!”

## Changing map projections

If you know which CRS you want your map to be projected with, you can set your projection at the map or project level. Then, all files you import will be projected using that CRS.

To set that projection:

- Import your first file. 
- Go to Project > Properties in the main menu.
- Select the CRS tab.
- Select your desired CRS.
- Click OK.

Now all files you add will be visually projected to that CRS. If you were to close QGIS and add those same files to a new map, you would find that the projection was project specific and did not stay with the individual geo files.

## Changing file projections

If we do want to create layers with specifically-assigned projections, we can use the QGIS export features function to create those. 

To export a layer with a specific CRS, right click the layer and select Export > Save features as. 

- Format: Use the format most appropriate for what you're doing next. If you're doing more geographic analysis in QGIS, you can save as a shapefile or geopackage. If you are exporting for online display, you will want to use GeoJSON.
- File name: save the file in the appropriate folder with a file name that will help you identify what it is in the future. If you have the same file projected in different ways, you will want to have a way of designating the projection in the filename or at least in the folder containing the shapefile files so as not to confuse yourself. I suggest adding the EPSG code to the file name.
- CRS: Set the CRS to whatever you need. If you're exporting for further QGIS analysis, you usually want a projected CRS in feet or meters. If you're exporting for online display in Mapbox, you'll want EPSG:4326 - WGS 84.
- Add saved file to map: If you're doing further QGIS analysis, make sure this is checked.
