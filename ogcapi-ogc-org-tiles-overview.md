# OGC API - Tiles

[OGC API standards](https://ogcapi.ogc.org/) define modular API building blocks to spatially enable Web APIs
in a consistent way. [OpenAPI](http://openapis.org) is used to define the reusable
API building blocks with responses in JSON and HTML.

The OGC API family of standards is organized by resource type. The draft OGC API - Tiles standard enables an API to serve tiles of spatially referenced data or maps with predefined content, extent, and resolution.

## Overview of OGC API - Tiles - Part 1: Core


```
GET /tiles
```

Retrieves the tiles description for this collection including the `links` to get a `tile`.


```
GET /tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}
```

Retrieves a tile in the requested tileMatrixSet, on the requested
tileMatrix in the TileMatrixSet, with the requested tile indices (tileRow, tileCol). The tile has multiple collections (formerly refered as layers) with all selected features in the bounding box of the tile.


```
GET /tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}/info
```

Retrieves information about a point of a tile in the requested tileMatrixSet, on the requested tileMatrix in the TileMatrixSet, with the requested tile indices (tileRow, tileCol). The tile has a single collection (formerly referred as layer) with all selected features in the bounding box of the tile. The feature properties to include in the tile representation can be limited using a query parameter.

```
GET /tileMatrixSets
```

Retrieves all available tile matrix sets (tiling schemes).

```
GET /tileMatrixSets/{tileMatrixSetId}
```

Retrieves a tile matrix sets (tiling scheme) by id

```
GET /collections
```

Lists the collections of data on the server that can be queried,
and each describes basic information about the geospatial data collection, like its id and description, as well as the
spatial and temporal extents of all the data contained.


```
GET /collections/{collectionId}
```

Retrieves a description of a collection.

```
GET /collections/{collectionId}/tiles
```

Retrieves the tiles description for this collection including the `links` to get a `tile`, the `TileMatrixSetLink` and the `infoTemplate`.

```
GET /collections/{collectionId}/tiles/{tileMatrixSetId}
```

Retrieves the tiles description for this collection including the `links` to get a `tile`, the `TileMatrixSetLink` and the `infoTemplate`.


```
GET /collections/{collectionId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}
```

Retrieves the tile in the requested tileMatrixSet, on the requested tileMatrix in the TileMatrixSet, with the requested tile indices (tileRow, tileCol). The tile has a single collection (formerly referred to as a layer) with all selected features in the bounding box of the tile. The feature properties to include in the tile representation can be limited using a query parameter.

```
GET /collections/{collectionId}/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}/info
```

Retrieves information on a point of a tile in the requested tileMatrixSet, on the requested tileMatrix in the TileMatrixSet, with the requested tile indices (tileRow, tileCol). The tile has a single collection (formerly referred as layer) with all selected features in the bounding box of the tile. The feature properties to include in the tile representation can be limited using a query parameter.
