# OGC API - Tiles

This GitHub repository contains the new revision of the [OGC](http://opengeospatial.org)'s Web Map Tile Service standards for requesting tiles (both vector tiles and maps tiles; and eventually coverage tiles) of geospatial information on the web. It is a complete rewrite of previous versions, focusing on a simple RESTful core specified as reusable [OpenAPI](http://openapis.org) components.

This is the CURRENT working version of this initiative (Old version work was one of the  engineering reports in Testbed-15 see the public version in http://docs.opengeospatial.org/per/19-069.html; or the GitHub version:  https://github.com/opengeospatial/T-15-D014-WMTS_draft_specification; if you are not a member or observer in Testbed15 you will get a 404)

IMPORTANT: Many examples of OpenAPI documents that are used as inspiration and test of this work is here:
https://app.swaggerhub.com/apis/UAB-CREAF

The OGC API - Maps and the OGC API - Tiles are related and should be considered together. Visit the [Quick guide](QuickGuide/README.md)

## Standards
After a while getting familiar and playing with the OpenAPI definition files (explained just below in the "Examples section"), we have finally started to write the standard. We have decided an aggressive path to modularization having 2 cores, one for tiles and another for maps that can be combined as needed. Several extension for tiles and maps will emerge in the process.

The standard is written using AsciiDoc using many files that might be difficult to trace. Please see the standard document as a long HTML page EASY TO READ FORMAT here: https://htmlpreview.github.io/?https://github.com/opengeospatial/OGC-API-Tiles/blob/master/core/standard/OAPI_Tiles.html

### Tiles
We have received several recommendations to separate the specifications into a core and some extensions. In March 2020 we decided to restructure the GitHub repository to separate the core and the extensions in different documents that might be elaborated at different speeds.

At this moment in time we are working on doing this separation by moving files around.

#### Core
For the moment we have focus out efforts on defining the "tile core" that you can find [here: clause_7_tile_core](standard/clause_7_tile_core.adoc).

The core is (https://htmlpreview.github.io/?https://raw.githubusercontent.com/opengeospatial/OGC-API-Tiles/master/core/standard/OAPI_Tiles.html):
* Only one collection
* Support for predefined Tile Matrix Set (in OGC 17-083r2)
  - No TileMatrixSet definition
* No featureInfo
* Can only retrieve one tile at a time
* Has no information about updates

#### Extensions
We foresee the following extensions (some of them can end into OGC standards and some might not)
* Other TileMatrixSets  (started in: [clause_7_tile_tms](extensions/tmxs/standard/clause_7_tile_tms.adoc), https://htmlpreview.github.io/?https://raw.githubusercontent.com/opengeospatial/OGC-API-Tiles/tree/master/extensions/tmxs/standard/OAPI_Tiles.html)
* Info (featureInfo) (started in: [clause_7_tile_info](extensions/info/standard/clause_7_tile_info.adoc), https://htmlpreview.github.io/?https://raw.githubusercontent.com/opengeospatial/OGC-API-Tiles/tree/master/extensions/info/standard/OAPI_Tiles.html)
* Root (one or more geospatial resources) (started in: [clause_7_tile_root](core/standard/clause_7_tile_root.adoc), https://htmlpreview.github.io/?https://raw.githubusercontent.com/opengeospatial/OGC-API-Tiles/tree/master/core/standard/OAPI_Tiles.html )
* Root Info (with feautureInfo) (pending)
* Multi-tile (retrieve a ZIP with many tiles) (started in: [clause_7_multitile](extensions/multitile/standard/clause_7_tile_collections.adoc), https://htmlpreview.github.io/?https://raw.githubusercontent.com/opengeospatial/OGC-API-Tiles/tree/master/extensions/multitile/standard/OAPI_Tiles.html )

## Using the standard

Those who want to just see the endpoints and responses can explore generic
OpenAPI definitions in this folder (please paste one of them in the Swagger Editor):

* OGC-API-Map-Tiles/standard/openapi/

## Examples
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
