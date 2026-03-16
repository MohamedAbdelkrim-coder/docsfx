---
title: IFC georeferencing
description: Learn how to place geolocated IFC models on a real-world 3D map, what IFC location data is required, and what to expect when model coordinates are incomplete.
keywords: real world map, IFC geolocation, IFC map, BIM GIS, IFC site coordinates, IFC map conversion, Google 3D tiles, Flinker
canonical_url: https://docs.flinker.app/docs/real_worldMap.html
---

# IFC georeferencing

The **IFC georeferencing** feature places your IFC model on top of a real-world 3D map using the location data already stored in the IFC file.

You do not need to enter coordinates manually when the required georeferencing data already exists in the IFC file.

This makes it easier to:

- verify that a project is positioned correctly
- compare the model against its surrounding context
- understand how the building relates to nearby roads, buildings, and landscape

![IFC georeferencing example](/_media/real-world-map-placeholder.png)


## How It Works

When a model contains usable geolocation, the viewer can show it in its real-world context on the map.

In most cases, this happens automatically when the IFC file includes valid georeferencing data and location information.

## Supported IFC Location Data

The feature supports the most common IFC geolocation methods.

### IFC4 Models

For IFC4-based files, the viewer can use coordinate reference system (CRS) information and map conversion data stored in the IFC model.

This is the preferred option for accurate real-world placement.

### IFC2X3 Models

For IFC2X3 files, the viewer can use location values stored in `IfcSite`, such as:

- reference latitude
- reference longitude
- reference elevation

## GIS Basics

### What is a CRS?

`CRS` stands for **Coordinate Reference System**.

A CRS defines how a location is described on the earth. It tells the viewer how to interpret coordinates so the model can be placed in the correct real-world position.

In simple terms:

- latitude and longitude are one type of coordinate system
- projected easting and northing values are another type
- the CRS tells the viewer which one is being used

### What is an EPSG code?

An `EPSG` code is a standard numeric identifier for a coordinate system.

For example:

- `EPSG:4326` is the common WGS84 latitude and longitude system used by many web maps
- `EPSG:27700` is used for British National Grid
- `EPSG:28992` is used for the Dutch RD New system

Using the correct EPSG code helps the viewer understand where the model belongs on the map.

## Coordinate System Support

The viewer can convert supported projected coordinate systems into map coordinates for display on the real-world map.

Current support includes:

- `EPSG:28992`
- `EPSG:8395`
- `EPSG:27700`

If the IFC file contains another EPSG code, placement may still work when the coordinate system can be resolved successfully.

## IFC2X3 vs IFC4 for Map Placement

Both IFC2X3 and IFC4 can support map placement, but they usually describe location in different ways.

### IFC2X3

IFC2X3 commonly relies on `IfcSite` values such as:

- reference latitude
- reference longitude
- reference elevation

This works well for many models, but it is usually a simpler form of geolocation.

### IFC4

IFC4 can include **map conversion** information in addition to site coordinates.

This is useful because it allows the model to describe how project coordinates relate to a real map coordinate system.

In practice, this usually means:

- the model can include a named CRS
- the model can include projected coordinates
- the model can include map conversion settings for more accurate placement

### Practical Difference

For users, the main difference is:

- **IFC2X3** often provides location through site latitude and longitude
- **IFC4** can provide a more complete georeferencing setup through CRS and map conversion data

Because of that, IFC4 files are often better suited for reliable GIS and map-based workflows when exported correctly.

## What You Need in the IFC File

For reliable placement, your IFC model should include at least one of these:

- valid IFC4 map conversion / CRS data
- valid `IfcSite` latitude and longitude
- usable elevation information

The more complete the geolocation data is, the more accurate the result will be.

## Terrain Placement

The model is displayed so it sits naturally within the real-world map view.

This helps the model align more naturally with:

- ground level
- surrounding buildings
- local site context

If elevation data is available in the IFC file, the vertical position can be more accurate.


## Best Results

For the best placement quality:

- export IFC files with georeferencing enabled
- include CRS or `IfcSite` location data
- include elevation if available
- verify that the source model uses the correct project coordinate system

## Known Limitations

- Placement quality depends on the geolocation quality stored in the IFC file.
- Some coordinate systems may not be supported if the EPSG reference is missing or unclear.

## Common Problems and How to Fix Them

### Model appears in the wrong location

Check whether the IFC file contains:

- the correct latitude and longitude
- the correct CRS or EPSG reference
- the intended project base point / survey point settings from the authoring tool

How to fix it:

- verify the coordinate system used in the authoring tool before export
- confirm that the IFC file contains the correct georeferencing information
- re-export the model if the project base point or survey point was set incorrectly

### Height looks wrong

Possible reasons:

- the elevation stored in the IFC file is incomplete
- the project base point or survey point was exported incorrectly
- the source model uses a different vertical reference than expected

How to fix it:

- check the elevation settings in the authoring tool
- verify the project base point and survey point before exporting
- re-export the IFC with the correct georeferencing settings

### Coordinates are missing from the project team workflow

In many cases, users expect to type coordinates manually, but this feature is designed to use the georeferencing data already stored in the IFC file.

How to fix it:

- make sure georeferencing is included during IFC export
- ask the BIM authoring team to provide `IfcSite` data for IFC2X3 or map conversion data for IFC4
- verify the exported IFC before sharing it with end users


## Related Features

- [IFC Viewer](ifc-viewer.md)
- [IFC Filters](ifc-filters.md)

## References

- [Add reference link title here](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMapConversion.htm)
