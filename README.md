# OGC API - Tiles
This GitHub repository contains OGC's multi-part standard for querying and retrieving tiles of geospatial information on the web, "OGC API - Tiles". The draft specification is available in [HTML](http://docs.ogc.org/DRAFTS/20-057.html) and [PDF](http://docs.ogc.org/DRAFTS/20-057.pdf).

Data with a location component (i.e. geospatial data) can be very large. For example, consider satellite images that cover vast areas of Earth's surface. To make these datasets easier to use, they can be divided into *tiles* - smaller subsets of data that can be used individually. OGC API - Tiles provides a standardized way for requesting such tiles through the web.

## Overview

OGC API - Tiles is a standards API that provides tiles of geospatial information. Different forms of geospatial information are supported, such as vector features, coverages and maps (or imagery).

Vector data represents geospatial objects as points, lines, and polygons. Tiles of vector data (i.e. Vector Tiles) represent subsets of vector data covering a large area (e.g. lines representing rivers in a country).

In this context, a map is essentially an image representing at least one type of geospatial information. Tiles of map data (i.e. Map Tiles) represent subsets of map data covering a large area (e.g. a satellite image).

### Core

The **_Core_** conformance class of _OGC API - Tiles_ simply requires that tiles can be retrieved according to a [tile matrix set](https://docs.opengeospatial.org/DRAFTS/17-083r3.html#tile-matrix-set-concept), using some template URL made up of:
- a tile matrix,
- a tile row, and
- a tile column.

That URL template and information about the tileset can either be provided through the _**TileSet**_ conformance class, or by some outside mechanism.

### TileSet & TileSets List

The **_TileSets List_** and **_TileSet_** conformance classes defines transportable end-points:

- `GET .../tiles`
Retrieves the list of tilesets available (links with `http://www.opengis.net/def/rel/ogc/1.0/tileset-*` relation types)
- `GET .../tiles/{tileMatrixSetId}`
Retrieves the [metadata](https://docs.opengeospatial.org/DRAFTS/17-083r3.html#tile-set-metadata) for a specific tileset (tiled according to a particular tile matrix set).
- `GET .../tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}`
Retrieves a tile from a specific tileset (tiled according to a particular tile matrix set) in the requested tile matrix set, on the requested tile matrix (e.g. zoom level) with the requested row and column.

### DataSet & GeoData Tile Sets

The **_DataSet TileSets_** conformance class defines how a list of tilesets can be associated to an OGC API dataset / landing page, while the **_GeoData TileSets_** conformance class defines how a list of tilesets can be associated to an OGC API collection.

By combining _Tiles_ building blocks with other OGC API standards, different types of tilesets can be provided from a single API:

**Vector tiles:**

- `{datasetAPI}/tiles`
Dataset tilesets (multi-layer vector tiles)
- `{datasetAPI}/collections/{collectionId}/tiles`
Collection tilesets (vector tiles)

**Map tiles** (_OGC API - Maps_):

- `{datasetAPI}/map/tiles`
Dataset map tilesets
- `{datasetAPI}/collections/{collectionId}/map/tiles`
Collection map tilesets

**Coverage tiles** (_OGC API - Coverages_):

- `{datasetAPI}/collections/{collectionId}/coverage/tiles`
Collection coverage tilesets

**Styled vector tiles**, e.g. filtered by scale (_OGC API - Styles_):

- `{datasetAPI}/styles/{styleId}/tiles`
Styled dataset tilesets (multi-layer vector tiles)
- `{datasetAPI}/collections/{collectionId}/styles/{styleId}/tiles`
Styled collection tilesets (vector tiles)

**Styled map tiles** (_OGC API - Maps_ and _OGC API - Styles_):

- `{datasetAPI}/styles/{styleId}/map/tiles`
Styled dataset map tilesets
- `{datasetAPI}/collections/{collectionId}/styles/{styleId}/map/tiles`
Collection map tilesets

## Quick links

Latest draft specifications: [HTML](https://docs.ogc.org/DRAFTS/20-057.html) [PDF](https://docs.ogc.org/DRAFTS/20-057.pdf)

See also the [TileMatrixSet & TileSet metadata standard](https://github.com/opengeospatial/2D-Tile-Matrix-Set) which provides the schemas used by _Tiles_.
(Latest draft: [HTML](https://docs.opengeospatial.org/DRAFTS/17-083r3.html) [PDF](https://docs.opengeospatial.org/DRAFTS/17-083r3.pdf))

[TileSet Schema](https://github.com/opengeospatial/2D-Tile-Matrix-Set/blob/master/schemas/tms/2.0/json/tileSet.json) /
[Examples](https://github.com/opengeospatial/2D-Tile-Matrix-Set/tree/master/schemas/tms/2.0/json/examples/tileset)

[TileMatrixSet Schema](https://github.com/opengeospatial/2D-Tile-Matrix-Set/blob/master/schemas/tms/2.0/json/tileMatrixSet.json) /
[Examples](https://github.com/opengeospatial/2D-Tile-Matrix-Set/tree/master/schemas/tms/2.0/json/examples/tilematrixset)

## Introduction

This GitHub repository contains the new revision of the [OGC](http://opengeospatial.org)'s Web Map Tile Service standards for requesting tiles (vector tiles, map tiles, coverage tiles, and potentially eventually additional types of tiles) of geospatial information on the web. It is a complete rewrite of previous versions, focusing on a simple RESTful core specified as reusable [OpenAPI](http://openapis.org) components.

This is the CURRENT working version of this initiative.

IMPORTANT: Many examples of OpenAPI documents that are used as inspiration and test of this work is here:
https://app.swaggerhub.com/apis/UAB-CREAF

The OGC API - Maps and the OGC API - Tiles are related and should be considered complementary. Visit the [Quick guide](QuickGuide/README.md)

## Standards

[OGC API standards](https://ogcapi.ogc.org) define modular API building blocks to spatially enable Web APIs
in a consistent way. [OpenAPI](http://openapis.org) is used to define the reusable
API building blocks.

After a while getting familiar and playing with the OpenAPI definition files (explained just below in the "Examples section"), we have finally started to write the standard. We have decided an aggressive path to modularization having two separate core standards, one for tiles and another for maps that can be combined as needed. Several extension for tiles and maps will emerge in the process.

While under development, the standards are written using AsciiDoc using many files that might be difficult to trace. Please see the compiled standard document as it is easier to read here: https://docs.ogc.org/DRAFTS/20-057.html

### OGC API - Tiles - Part 1: Core
The definition of OGC API - Tiles - Part 1: Core is the immediate next step. The Standards Working Group (SWG) agreed on the structure shown below.

1. TileSet - It specifies a tileset resource (a tileset in a single Tile Matrix Set), which is a resource that contains information on how to formulate a request to a tile. It also specifies how the get a tile by indicating the Tile Matrix and the row and column.
2. TileSets - It It specifies a tilesets resource describing multiple tile sets
3. DatasetTileSets - OGC API Common - Part 1 (dataset, /map resource at the root): Defines how to get a tile resource from the dataset (or datasets) represented by the services. it will tell the path to get a tile resource.
4. GeoDataResourceSelection - together with 3, geodata= query parameter: This is identical to the GeoDataResourceSelection conformance class of OGC API - Common and if done adequately.
5. GeoDataResourceMap - OGC API Common - Part 2 / OGC Feature - Part 1 (collection connection, /maps resource after {collectionID}): It will define how to specify the a link to a tile resource containing a representation of this geospatial data resource (path).
6. TileMap - It will define how to specify the a link to a tile resource containing a representation of a map (path).

### Extensions
We foresee the following extensions (some of them can end into OGC standards and some might not)
* Info (featureInfo) (started in: [clause_7_tile_info](extensions/info/standard/clause_7_tile_info.adoc))
* Multi-tile (retrieve a ZIP with many tiles) (started in: [clause_7_multitile](extensions/multitile/standard/clause_7_tile_multitiles.adoc))

## Using the standard

Those who want to just see the endpoints and responses can explore generic
OpenAPI definitions in this folder (please paste one of them in the Swagger Editor):

* [OGC-API-Tiles/openapi/](https://github.com/opengeospatial/OGC-API-Tiles/tree/master/openapi)

Several implementations of the draft standard exist:

[Implementations of the draft specification / demo services](./implementations.adoc)

## Examples
An example OpenAPI definition, that describes hypothetical WebAPI conformant to this standard to expose vector tiles is available here: https://app.swaggerhub.com/apis/UAB-CREAF/ogc-api-tiles-opf-xmp-vt-more-1-collection/1.0.0
A resolved (almost without dependencies with other files) YAML file, synchronized with the previous working document, is available in this github repository at: https://github.com/opengeospatial/OGC-API-tiles/tree/master/openapi/swaggerhub/tiles.yaml

An example OpenAPI definition, that describes hypothetical WebAPI conformant to this standard to expose map tiles is available here: https://app.swaggerhub.com/apis/UAB-CREAF/ogc-api-map-tiles-opf-xmp-mt-more-1-collection/1.0.0
A resolved (almost without dependencies with other files) YAML file, synchronized with the previous working document, is available in this github repository at: https://github.com/opengeospatial/OGC-API-tiles/tree/master/openapi/swaggerhub/map-tiles.yaml


WARNING: This section need to be updated.

Until mid July 2019, the work was focused on providing OpenAPI services description examples and domains (libraries). Now we believe this work is finalized, but each time that we take a look we still find gaps, mistakes and things that can be improved.
We expect that during the effort of extracting the knowledge accumulated (hopefully) in these files to create the standard, we will keep fixing, perfecting and evolving things.

IMPORTANT NOTE: We are now using the Swagger HUB again and should be considered the "gold copy". The Swagger account is:
* [Domain documents](https://app.swaggerhub.com/search?owner=UAB-CREAF&type=DOMAIN)
* [API example documents](https://app.swaggerhub.com/search?owner=UAB-CREAF&type=API)

The material in the [standards folder](standard/openapi) takes precedence to the text of the standard and the Swagger HUB takes precedence to the material in GitHub. The [standards folder](standard/openapi) examples are intended to be identical to the Swagger HUB ones except for the path names. To go from  Swagger HUB to GitHub do the following substitutions:
* Replace "https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-" by "https://raw.githubusercontent.com/opengeospatial/OGC-API-Map-Tiles/master/standard/openapi/ogc-api-"
* Replace "/1.0.0#/" by ".yaml#/"

The files in the [standards folder](standard/openapi) are structured in several parts that can be combined together.

![Diagram of the examples and domains](standard/images/diagram-xmp.png)

A [OGC API maps and tiles OPF FULL example in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-map-tiles-opf-xmp-full/1.0.0) or in [GitHub](standard/openapi/ogc-api-map-tiles-opf-xmp-full.yaml) that contains full example of server with some features and coverages that are served as maps and/or tiles.

The latter is normally too long to be analyzed. The following are easier to understand.

Examples:
* A [OGC API OPF example for vector tiles in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-tiles-opf-xmp-vt-more-1-collection/1.0.0) or in [GitHub](standard/openapi/ogc-api-tiles-opf-xmp-vt-more-1-collection.yaml) that describes a service that can serve only tiled features (vector tiles) of one or more collections.
* A [OGC API OPF example for tiled map in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-map-tiles-opf-xmp-mt-more-1-collection/1.0.0) or in [GitHub](standard/openapi/ogc-api-map-tiles-opf-xmp-mt-more-1-collection.yaml) that describes a service that can serve only map (raster) tiles of one or more collections.
* A [OGC API OPF example for maps in Swagger](standard/openapi/ogc-api-maps-opf-xmp-ore-1-collection.yaml) that describes a service that can serve only maps of one or more collections.
* A [OGC API OPF example for tiled coverages in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-tiles-opf-xmp-vt-more-1-collection/1.0.0) or in [GitHub](standard/openapi/ogc-api-tiles-opf-xmp-vt-more-1-collection.yaml) that describes a service that can serve tiled coverages of one or more collections. This example was not initially needed by the sponsors but is motivated by the elevation map in a GeoPackage example.

Libraries:
* A [OGC API common DOMAIN document in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-common/1.0.0) or in [GitHub](standard/openapi/ogc-api-common.yaml). It contains fragments that can be reference in api document instances or other domain document. It could become part of a future OGC API common standard additional material.
* A [OGC API maps DOMAIN document in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-maps/1.0.0) or in [GitHub](standard/openapi/ogc-api-maps.yaml). It contains fragments that can be reference in api document instances or other domain document. It could become part of a future OGC API maps standard additional material.
* A [OGC API maps and tiles DOMAIN document in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-map-tiles/1.0.0) or in [GitHub](standard/openapi/ogc-api-map-tiles.yaml). It contains fragments that can be reference in api document instances or other domain document. It will be included by OGC API maps standard and tiles standard.
* A [OGC API tiles DOMAIN document in Swagger](https://api.swaggerhub.com/domains/UAB-CREAF/ogc-api-tiles/1.0.0) or in [GitHub](standard/openapi/ogc-api-tiles.yaml). It contains fragments that can be reference in api document instances or other domain document. It could become part of a future OGC API tiles standard additional material.

## Communication

Join the WMS mailing list

Most work on the specification takes place in [GitHub issues](https://github.com/opengeospatial/OGC-API-Map-Tiles/issues),
so browse there to get a good idea of what is happening, as well as past decisions.

## Contributing

The contributor understands that any contributions, if accepted by the OGC Membership (and eventually the ISO/TC 211), shall be incorporated into OGC and ISO/TC 211 Web Map Service and Web Map Tile Service standards documents and that all copyright and intellectual property shall be vested to the OGC.

The WMS Standards Working Group (SWG) is the group at OGC responsible for the stewardship of the standard, but is working to do as much work in public as possible.

* [Open issues](https://github.com/opengeospatial/OGC-API-Map-Tiles/issues)
* [Copy of License Language](https://raw.githubusercontent.com/opengeospatial/OGC-API-Map-Tiles/master/LICENSE)

Pull Requests from contributors are welcomed. However, please note that by sending a Pull Request or Commit to this GitHub repository, you are agreeing to the terms in the Observer Agreement https://portal.ogc.org/files/?artifact_id=92169
