# OGC API - Tiles

This GitHub repository contains the new revision of the [OGC](http://opengeospatial.org)'s Web Map Tile Service standards for requesting tiles (both vector tiles and maps tiles; and eventually coverage tiles) of geospatial information on the web. It is a complete rewrite of WMTS, focusing on a simple RESTful core specified as reusable [OpenAPI](http://openapis.org) components.

This is the CURRENT working version of this initiative (Old version work has been moved to the deliverables in Testbed-15 that contain the LAST VERSION of the materials. See: https://github.com/opengeospatial/T-15-D014-WMTS_draft_specification)

There is some level of overlap with the OGC API - Maps. OGC API - Tiles will be elaborated first and we will continue with this one.

It is difficult to maintain so many document README.md documents. I decided to remove all the content in this one. There is more (../README.md)[README materials here] (root README.md file).

## Use cases
This is the list of use cases that OGC Tiles should cover
* Retrieve a tile linked to a resource available as features or coverages
* Retrieve a tile linked to a resource that is not available in other formats
* Tiles that are in a tilematrixset that is well known
* Tiles that are in tilematrixset defined in the service
* Tiles from more than one geospatial resource (collections).
* Several tiles as a ZIP files (extension)
* ...

## Standards
The current approach to write is to create a building block that can be applied to resources. As a principle design a building block should be independent of the API general structure. This means that we will avoid any reference to OGC API Features or even to OGC API Common.

## Communication

Join the OGC API mailing list

Most work on the specification takes place in [GitHub issues](https://github.com/opengeospatial/OGC-API-Tiles/issues),
so browse there to get a good idea of what is happening, as well as past decisions.

## Contributing

The contributor understands that any contributions, if accepted by the OGC Membership (and eventually the ISO/TC 211), shall be incorporated into OGC and ISO/TC 211 Web Map Service and Web Map Tile Service standards documents and that all copyright and intellectual property shall be vested to the OGC.

The OGC API Standards Working Group (SWG) is the group at OGC responsible for the stewardship of the standard, but is working to do as much work in public as possible.

* [Open issues](https://github.com/opengeospatial/OGC-API-Map-Tiles/issues)
* [Copy of License Language](https://raw.githubusercontent.com/opengeospatial/OGC-API-Map-Tiles/master/LICENSE)
