TBD and finalized sorry.

# About

This guide is intended to communicate the key pieces of the Tiles API standard so that implementors can get started
without having to dig through the longer specification.

## Introduction

OGC API - Tiles provides a standard way to describe web map tile sets for clients to consume. It is the successor to
[WMTS](https://en.wikipedia.org/wiki/Web_Map_Tile_Service), updated to use JSON, in line with the spatial data on the web
best practices. It also is designed to be a 'building block', that can plug into the OGC API suite, but can also be used
as a standalone piece. It's also similar to [TileJSON](https://github.com/mapbox/tilejson-spec), adding the ability to
handle alternate projections and fitting into the OGC API suite of standards.


## Overview

IMPORTANT NOTE: This section is old The [standard](standard) candidate takes precedence.

### Maps

A "OGC API - Maps" is a standard API that provides maps representing geospatial data.

```
GET /.../.../map/{styleId}
```

The identifier of the "layer" is replaced by "{collectionId}" or "coverage"...

Maps can be requested in any available CRS and can be subset by bbox width and height (and eventually other parameters such as time and elevation)
```
GET /.../.../map/{styleId}?crs=CRS84&bbox=160.6,-55.95,-170,-25.89&width=600&height=400
```
Returns a map - a representation of real-world elements at a given resolution. {styleId} is optional.


### Tiles

A "OGC API - Tiles" is a standard API that provides tiles of maps representing geospatial data.

```
GET /.../.../tiles/{styleId}/{tileMatrixSetId}/{tileMatrixId}/{tileRow}/{tileCol}
```

Returns a tile - a representation of real-world elements at a given resolution restricted by the selected Tile Matrix Set. {styleId} is optional.

The identifier of the "layer" is replaced by "{collectionId}" or "coverage"...

Tiles are available at some TileMatrixSetId and styles that need to be enumerated in:
```
GET /.../.../tiles
```

There is a need for describing the TileMatrixSet available
```
GET /tileMatrixSet/{tileMatrixSetId}
```
