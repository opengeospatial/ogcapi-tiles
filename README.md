# OGC API - Tiles

This GitHub repository contains OGC's multi-part _OGC API - Tiles_ standard for querying and retrieving tiles of geospatial information on the web.

This is the **current** working version of this initiative, written using many AsciiDoc files that might be difficult to follow.

Please see the latest compiled draft specification available in [HTML](https://opengeospatial.github.io/ogcna-auto-review/20-057.html) and [PDF](https://opengeospatial.github.io/ogcna-auto-review/20-057.pdf) which are easier to read.

This specification relies on the [_Tile Matrix Set and Tile Set Metadata_ standard](https://github.com/opengeospatial/2D-Tile-Matrix-Set/) (version 2.0: [HTML](https://docs.ogc.org/is/20-057/20-057.html) or [PDF](https://docs.ogc.org/is/20-057/20-057.pdf)).

See the latest [OpenAPI definition](https://github.com/opengeospatial/ogcapi-tiles/tree/master/openapi) with [SwaggerUI](https://petstore.swagger.io/?url=https://raw.githubusercontent.com/opengeospatial/ogcapi-tiles/master/openapi/ogcapi-tiles-1.bundled.json).

## Overview

_OGC API - Tiles_ is a standard API that provides tiles of geospatial information.

Different forms of geospatial information are supported, such as tiles of vector features ("vector tiles"), coverages, maps (or imagery) and potentially eventually additional types of tiles) of geospatial information.

Vector data represents geospatial objects as points, lines, and polygons. Tiles of vector data (i.e. Vector Tiles) represent subsets of vector data covering a large area (e.g. lines representing rivers in a country).

In this context, a map is essentially an image representing at least one type of geospatial information. Tiles of map data (i.e. Map Tiles) represent subsets of map data covering a large area (e.g. a satellite image).

### Core

The **_Core_** conformance class of _OGC API - Tiles_ simply requires that tiles can be retrieved according to a [tile matrix set](https://docs.opengeospatial.org/is/17-083r4/17-083r4.html#tile-matrix-set-concept), using some template URL made up of:
- a tile matrix,
- a tile row, and
- a tile column.

That URL template and information about the tileset can either be provided through the _**TileSet**_ conformance class, or by some outside mechanism.

### TileSet & TileSets List

The **_TileSets List_** and **_TileSet_** conformance classes defines transportable end-points:

- `GET .../tiles`
Retrieves the list of tilesets available (`tilesets` array property whose elements contain `links` to the tileset with `self` relation type)
- `GET .../tiles/{tileMatrixSetId}`
Retrieves the [metadata](https://docs.opengeospatial.org/is/17-083r4/17-083r4.html#tile-set-metadata) for a specific tileset (tiled according to a particular tile matrix set).
- `GET .../tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}`
Retrieves a tile from a specific tileset (tiled according to a particular tile matrix set) in the requested tile matrix set, on the requested tile matrix (e.g. zoom level) with the requested row and column.

### DataSet & GeoData Tile Sets

The **_DataSet TileSets_** conformance class defines how a list of tilesets can be associated to an OGC API dataset / landing page, while the **_GeoData TileSets_** conformance class defines how a list of tilesets can be associated to an OGC API collection.

By combining _Tiles_ building blocks with other OGC API standards, different types of tilesets can be provided from a single API:

**Vector tiles:**

(link relation: `http://www.opengis.net/def/rel/ogc/1.0/tilesets-vector`)

- `{datasetAPI}/tiles`
Dataset tilesets (multi-layer vector tiles)
- `{datasetAPI}/collections/{collectionId}/tiles`
Collection tilesets (vector tiles)

**Map tiles** (_OGC API - Maps_):

(link relation: `http://www.opengis.net/def/rel/ogc/1.0/tilesets-map`)

- `{datasetAPI}/map/tiles`
Dataset map tilesets
- `{datasetAPI}/collections/{collectionId}/map/tiles`
Collection map tilesets

**Coverage tiles** (_OGC API - Coverages_):

(link relation: `http://www.opengis.net/def/rel/ogc/1.0/tilesets-coverage`)

- `{datasetAPI}/collections/{collectionId}/coverage/tiles`
Collection coverage tilesets

**Styled vector tiles**, e.g. filtered by scale (_OGC API - Styles_):

(link relation: `http://www.opengis.net/def/rel/ogc/1.0/tilesets-vector`)

- `{datasetAPI}/styles/{styleId}/tiles`
Styled dataset tilesets (multi-layer vector tiles)
- `{datasetAPI}/collections/{collectionId}/styles/{styleId}/tiles`
Styled collection tilesets (vector tiles)

**Styled map tiles** (_OGC API - Maps_ and _OGC API - Styles_):

(link relation: `http://www.opengis.net/def/rel/ogc/1.0/tilesets-map`)

- `{datasetAPI}/styles/{styleId}/map/tiles`
Styled dataset map tilesets
- `{datasetAPI}/collections/{collectionId}/styles/{styleId}/map/tiles`
Styled collection map tilesets

## Introduction

Data with a location component (i.e. geospatial data) can be very large.

For example, consider satellite images that cover vast areas of Earth's surface.

To make these datasets easier to use, they can be divided into *tiles* - smaller subsets of data that can be used individually.

_OGC API - Tiles_ provides a standardized way for requesting such tiles through the web.

[OGC API standards](https://ogcapi.ogc.org) define modular API building blocks to spatially enable Web APIs in a consistent way.

The _OGC API - Tiles_ specification defines building blocks that can be combined with other OGC API building blocks such as [_OGC API - Maps_](https://github.com/opengeospatial/ogcapi-maps) (to retrieve map tiles) and [_OGC API - Coverages_](https://github.com/opengeospatial/ogcapi-coverages) (to retrieve coverage tiles).

This specification is a complete rewrite of the of the [OGC](http://opengeospatial.org)'s previous Web Map Tile Service (WMTS) standards versions, focusing on simple reusable RESTful building blocks which can be described using the [OpenAPI](http://openapis.org) specification.

## Quickstart guides
[Quickstart guide for clients](QuickGuide/README.md)

## Implementations
Several implementations of the draft standard exist:

[Implementations of the draft specification / demo services](./implementations.adoc)

## Draft specifications

### OGC API - Tiles - Part 1: Core
The definition of OGC API - Tiles - Part 1: Core is the current focus of the Standards Working Group (SWG). As agreed by the SWG, the draft specification is organized into the following main conformance classes:

1. [***Core***](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_tiles_core) specifies that tiles are retrievable according to a [tile matrix set](https://docs.opengeospatial.org/is/17-083r4/17-083r4.html#tile-matrix-set-concept), using some template URL made up of a tile matrix, a tile row, and a tile column.
2. [***TileSet***](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_tileSet) specifies a tileset resource (tiles in a single Tile Matrix Set), including
   - a templated URL to access individual tiles (**1**),
   - a link to the definition of the TileMatrixSet (see the [TileMatrixSet schema](https://github.com/opengeospatial/2D-Tile-Matrix-Set/blob/master/schemas/tms/2.0/json/tileMatrixSet.json) and [examples](https://github.com/opengeospatial/2D-Tile-Matrix-Set/tree/master/schemas/tms/2.0/json/examples/tilematrixset)), as well as a URI for it if applicable (e.g. if registered on a [register such as the OGC NA's](http://www.opengis.net/def/tms)), as well as
   - additional [metadata](https://docs.opengeospatial.org/is/17-083r4/17-083r4.html#tile-set-metadata) (see the full [TileSet schema](https://github.com/opengeospatial/2D-Tile-Matrix-Set/blob/master/schemas/tms/2.0/json/tileSet.json) and [examples](https://github.com/opengeospatial/2D-Tile-Matrix-Set/tree/master/schemas/tms/2.0/json/examples/tileset))
3. [***TileSets List***](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_tileSets-list) specifies a tilesets resource describing multiple tilesets (**2**).
4. [***DatasetTileSets***](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_datasetTileSets) specifies how to link to a list (**3**) of tilesets (**2**) for the whole dataset distributed by an API from its landing page (as defined by [_OGC API Common - Part 1_](https://docs.opengeospatial.org/DRAFTS/19-072.html#rc_landing-page-section)).
5. [***GeoDataTileSets***](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_geoDataResourceTileSets) specifies how to link to a list (**3**) of tilesets (**2**) from a resource representing a collection of geospatial data (as defined by [_OGC API Common - Part 2_](https://docs.opengeospatial.org/DRAFTS/20-024.html#rc-collections-section)).
6. [***GeoDataSelection***](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_collections-selection) specifies the `collections=` query parameter allowing to select specific collections of geospatial data to include within a dynamically generated tileset (**2**).

Six additional [encodings](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_encodings) conformance classes are pre-defined for [_PNG_](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_png), [_JPEG_](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_jpeg), [_GeoTIFF_](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_tiff), [_GeoJSON_](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_geojson), [_Mapbox Vector Tiles_](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_mvt) and [_netCDF_](https://opengeospatial.github.io/ogcna-auto-review/20-057.html#rc_netcdf).

How to link to tilesets of [Maps](https://docs.ogc.org/DRAFTS/20-058.html#_relationship_to_ogc_api_tiles), [Coverages](https://docs.opengeospatial.org/DRAFTS/19-087.html#rc-coverage-tiles-section) and potentially other geospatial resources, is defined in the respective specification by leveraging the _OGC API - Tiles_ building blocks.

_Note that it was [decided](https://github.com/opengeospatial/ogcapi-maps/issues/76) that Map Tiles would be an optional conformance class of _OGC API - Maps - Part 1: Core_, but this is pending an update to the draft specification_.

### Extensions
We foresee the following extensions (some of them might become OGC standards, and some might not)
* Info (featureInfo) (started in: [clause_7_tile_info](extensions/info/standard/clause_7_tile_info.adoc))
* Multi-tile (retrieve a ZIP with many tiles) (started in: [clause_7_multitile](extensions/multitile/standard/clause_7_tile_multitiles.adoc))
* TileMatrixSet transactions may allow to specify custom TileMatrixSet definitions according to which a server could dynamically generate tilesets

## Communication

Join the OGC API - Tiles [mailing list](https://lists.ogc.org/mailman/listinfo/ogcapi-tiles.swg).

Visit the OGC API - Tiles [project on the OGC portal](https://portal.ogc.org/?m=projects&a=view&project_id=646) after [signing](https://portal.ogc.org/files/?artifact_id=95414) the [Observer Agreement](https://portal.ogc.org/files/?artifact_id=92169).

Most work on the specification takes place in [GitHub issues](https://github.com/opengeospatial/ogcapi-tiles/issues),
so browse there to get a good idea of what is happening, as well as past decisions.

## Contributing

The contributor understands that any contributions, if accepted by the OGC Membership (and eventually the ISO/TC 211), shall be incorporated into OGC and ISO/TC 211 Web Map Service and Web Map Tile Service standards documents and that all copyright and intellectual property shall be vested to the OGC.

The OGC API - Tiles Standards Working Group (SWG) is the group at OGC responsible for the stewardship of the standard, but is working to do as much work in public as possible.

* [Open issues](https://github.com/opengeospatial/ogcapi-tiles/issues)
* [Copy of License Language](https://raw.githubusercontent.com/opengeospatial/ogcapi-tiles/master/LICENSE)

Pull Requests from contributors are welcomed. However, please note that by sending a Pull Request or Commit to this GitHub repository, you are agreeing to the terms in the [Observer Agreement](https://portal.ogc.org/files/?artifact_id=92169).
