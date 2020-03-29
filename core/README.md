# OGC API - Tiles

This GitHub repository contains the new revision of the [OGC](http://opengeospatial.org)'s Web Map Tile Service standards for requesting tiles (both vector tiles and maps tiles; and eventually coverage tiles) of geospatial information on the web. It is a complete rewrite of WMTS, focusing on a simple RESTful core specified as reusable [OpenAPI](http://openapis.org) components.

This is the CURRENT working version of this initiative (Old version work has been moved to the deliverables in Testbed-15 that contain the LAST VERSION of the materials. See: https://github.com/opengeospatial/T-15-D014-WMTS_draft_specification)

There is some level of overlap with the OGC API - Maps. OGC API - Tiles will be elaborated first and we will continue with this one.

## Use cases
This is the list of use cases that OGC Tiles should cover
* Retrieve a tile linked to a resource available as features or coverages
* Retrieve a tile linked to a resource that is not available in other formats
* Tiles that are in a tilematrixset that is well known
* Tiles that are in tilematrixset defined in the service
* Several tiles as a ZIP files
* Tiles from more than one geospatial resource.

## Standards
The current approach to write is to create a building block that can be applied to resources. As a principle design a building block should be independent of the API general structure. This means that we will avoid any reference to OGC API Features or even to OGC API Common.

The standard is written using ASCIIDOC using many files that might be difficult to trace. Please look for the PDF or HTML page EASY TO READ FORMAT: (https://htmlpreview.github.io/?https://github.com/opengeospatial/OGC-API-Map-Tiles/blob/master/standard/OAPI_MapsTiles.html)

### Tiles
#### Core document
##### Core class in the core
For the moment we have focus out efforts on defining the "tile core" that you can find [here: clause_7_tile_core](core/standard/clause_7_tile_core.adoc).

The core is:
* Only support for well known tilematrixsets.
* Only one geospatial resource (collection)
* No TileMatrixSet internal definition (only the eight TileMatrixSets defined in OGC 17-083r2 annex D)
* No featureInfo
* Can only retrieve one tile at a time
* No information about updates in tiles data

#### Second class in the core
* More than one geospatial resource (collections) (started in: [clause_7_tile_collections](core/standard/clause_7_tile_collections.adoc) )

#### Extension's documents
We foresee the following extensions (some of them can end into OGC standards and some might not)
* Other TileMatrixSets  (started in: [clause_7_tile_tms](extensions/tmxs/standard/clause_7_tile_tms.adoc) )
* Info (featureInfo) (started in: [clause_7_tile_info](extensions/info/standard/clause_7_tile_info.adoc) )
* Multi-tile (retrieve a ZIP with many tiles) (pending, necessary for the update workflow) (started in: [clause_7_tile_info](extensions/multitile/standard/clause_7_tile_cols_multitiles.adoc) )

#### How to do vector tiles service
The minimum set of modules to implement a vector tiles API is:
* OGC API Commons core
* OGC API Commons collections or OGC API Features core
* OGC API Tiles core

#### How to do map tiles service
Map tiles are tiles that are provided as rendered information. The minimum set of modules to implement a map tiles API is:
* OGC API Commons core
* OGC API Commons collections or OGC API Features core
* OGC API Maps core
* OGC API Tiles core

## Examples
WARNING: This section need to be updated.

Many examples of OpenAPI documents that are used as inspiration and test of this work is here:
https://app.swaggerhub.com/apis/UAB-CREAF

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
GET /.../.../tile/{styleId}/{tileMatrixSetId}/{tileMatrixId}/{tileRow}/{tileCol}
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

## Communication

Join the WMS mailing list

Most work on the specification takes place in [GitHub issues](https://github.com/opengeospatial/OGC-API-Tiles/issues),
so browse there to get a good idea of what is happening, as well as past decisions.

## Contributing

The contributor understands that any contributions, if accepted by the OGC Membership (and eventually the ISO/TC 211), shall be incorporated into OGC and ISO/TC 211 Web Map Service and Web Map Tile Service standards documents and that all copyright and intellectual property shall be vested to the OGC.

The WMS Standards Working Group (SWG) is the group at OGC responsible for the stewardship of the standard, but is working to do as much work in public as possible.

* [Open issues](https://github.com/opengeospatial/OGC-API-Map-Tiles/issues)
* [Copy of License Language](https://raw.githubusercontent.com/opengeospatial/OGC-API-Map-Tiles/master/LICENSE)
