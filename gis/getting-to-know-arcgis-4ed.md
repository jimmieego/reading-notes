# Chapter 1 Introducing GIS
## Basic GIS principles
- A GIS map contains layers
- Layers may contain features or surfaces
    + Each geographic object in a layer is called a feature
    + A geographic expanse is called a surface
- Features hae shape and size
    + **Vector** data: polygon, line, point
- Surfaces have numeric values rather than shapes
    + The most common kind of surface is a **raster**, a matrix of identically sized square cells. Each cell represents a unit of surface area and contains a measured or estimated value for that location.
- Features have locations
- Features can be displayed at different sizes
- Features are linked to information
    + Features on a GIS map are linked to information in the feature's attribute table
    + The link between features and their attributes makes it possible to ask questions about the information in an attribute table and display the answers on the map
- Features have spatial relationships
- New features can be created from areas of overlap

## Chapter 3 Interacting with maps
- Always layer lines and points on top of polygons. When you add data to ArcMap, the software automatically places points and lines above polygons.
- A **feature class** is a collection of geographic features that have the same geometry type (such as point, line, or polygon), the same attributes, and teh same spatial reference. Feature classes can be stored in geodatabase or as shapefiles, coverages, or other data formats. 
- **Symbology** refers to the appearance of features on a map - color, line thickness, fill motif, and so on.    